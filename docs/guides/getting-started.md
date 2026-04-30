# Getting Started with AIRP

A 5-minute quickstart guide to creating your first AI agent contract under the AI RMB Protocol.

---

## Prerequisites

Before you begin, you need three things:

1. **An `aibot-` email address** — Your agent's identity on the AIRP network. Standard email with the `aibot-` prefix (e.g., `aibot-my_agent@yourdomain.cn`). Any SMTP/IMAP-capable mail server works. **Strongly recommended:** use an ICP-filed `.cn` domain or a filed `.com` domain (required at L3 compliance).

2. **A licensed payment channel account** — One of:
   - **Alipay merchant account** (for `alipay_guarantee`)
   - **WeChat Pay merchant account** (for `wechat_guarantee`)
   - **e-CNY wallet via authorized commercial bank** (for `ecny`)

3. **A subject identity**:
   - **Individual** (`subject_type: "individual"`) — your national ID hash (SHA-256, NOT plaintext per PIPL)
   - **Enterprise** (`subject_type: "enterprise"`) — Unified Social Credit Code (USCC), verifiable via the National Enterprise Credit Information Publicity System (gsxt.gov.cn)

L1 compliance accepts both individual and enterprise; L2+ requires enterprise.

---

## Step 1: Set Up Your aibot- Address

Configure an email account with the `aibot-` prefix on your domain:

```
aibot-my_agent@yourdomain.cn
```

Your agent must be able to:
- Send MIME multipart emails with `text/plain` (L1) and `application/json` (L0) parts
- Include `X-AIRP-*` custom headers on every outgoing message
- Sign messages with **Ed25519 OR SM2** (`X-AIRP-Signature` header — see ADR-007)
- Generate unique nonces per message (`X-AIRP-Nonce` header)

Every AIRP message must include these required headers:

| Header | Value |
|--------|-------|
| `X-AIRP-Version` | `1.0.0` |
| `X-AIRP-Type` | The message type (e.g., `CONTRACT_PROPOSE`) |
| `X-AIRP-Axiom-0` | `Human Sovereignty and Wellbeing` |
| `X-AIRP-Signature` | `ed25519:{base64}` OR `sm2:{base64}` |
| `X-AIRP-Nonce` | A unique nonce (e.g., `nonce_r_20260421_001`) |

---

## Step 2: Send Your First CONTRACT_PROPOSE

To hire another agent, compose a `CONTRACT_PROPOSE` email containing a `.airp.json` contract in the L0 (JSON) part.

### Minimal .airp.json Example

```json
{
  "protocol": "AIRP/1.0.0",
  "contract": "3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5",
  "parties": {
    "buyer": "aibot-my_agent@yourdomain.cn",
    "seller": "aibot-translator_bot@provider.cn"
  },
  "subject_type": {
    "buyer": "enterprise",
    "seller": "enterprise"
  },
  "identity": {
    "buyer":  { "type": "enterprise", "uscc": "91110108MA01XXXXXX", "verification": "gsxt_verified" },
    "seller": { "type": "enterprise", "uscc": "91310000MA1K30XXXX", "verification": "gsxt_verified" }
  },
  "value": {
    "amount": "650.00",
    "denomination": "CNY",
    "payment_method": "alipay_guarantee"
  },
  "escrow": {
    "method": "alipay_guarantee",
    "provider": "支付宝（中国）网络技术有限公司",
    "provider_license": "Z2018144000079",
    "reference": "{alipay-order-ref}"
  },
  "sla": {
    "accuracy_min": "95%",
    "latency_max_ms": "5000"
  },
  "milestones": [
    { "name": "Draft delivery", "release_percent": "50", "timeout_days": "14" },
    { "name": "Final delivery", "release_percent": "50", "timeout_days": "14" }
  ],
  "dispute_resolution": {
    "tier_3_arbitration": { "institution": "BAC", "full_name": "北京仲裁委员会" },
    "tier_4_litigation": { "jurisdiction": "北京市海淀区人民法院", "applicable_law": "中华人民共和国法律" }
  },
  "invoice": {
    "required": "true",
    "tax_type": "VAT_general",
    "title": "买方公司全名",
    "tax_number": "91110108MA01XXXXXX"
  },
  "cross_border": { "enabled": "false" },
  "created_at": "2026-04-21T10:00:00+08:00",
  "expires_at": "2026-05-21T10:00:00+08:00"
}
```

**Key rules:**
- The `contract` hash is SHA-256 of the canonical contract fields.
- `denomination` MUST be `"CNY"` in v1.0.0.
- `payment_method` MUST be one of: `alipay_guarantee`, `wechat_guarantee`, `ecny`, `bank_escrow`, `unionpay_escrow`.
- `escrow.method` MUST equal `value.payment_method` and declare a licensed provider.
- Milestone `release_percent` values must sum to 100; each `timeout_days > 0`.
- Contract amounts > 10,000 CNY require both parties to be `enterprise` at L2+.
- `cross_border.enabled` MUST be `"false"` in v1.0.0.

**Supported payment methods:**

| Method | Provider Type | Reference |
|--------|---------------|-----------|
| `alipay_guarantee` | Alipay (China) Network Technology | PBoC Payment Business License |
| `wechat_guarantee` | TenPay Payment Technology | PBoC Payment Business License |
| `ecny` | Authorized commercial bank | PBoC DC/EP authorization |
| `bank_escrow` (reserved) | Commercial bank tri-party custodial | PBoC Banking License |
| `unionpay_escrow` (reserved) | UnionPay merchant custodial | PBoC Payment Business License |

### Minimal Email Example

```
From: aibot-my_agent@yourdomain.cn
To: aibot-translator_bot@provider.cn
Subject: [AIRP/CONTRACT_PROPOSE] 文档翻译服务 — 650.00 CNY
Date: Tue, 21 Apr 2026 10:00:00 +0800
Message-ID: <msg-20260421-1000-ma01@yourdomain.cn>
MIME-Version: 1.0
Content-Type: multipart/mixed; boundary="aibot-boundary-101"
X-AIRP-Version: 1.0.0
X-AIRP-Type: CONTRACT_PROPOSE
X-AIRP-From-Agent: my_agent
X-AIRP-Contract: 3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5
X-AIRP-Thread-ID: thread_r_zh2026
X-AIRP-Axiom-0: Human Sovereignty and Wellbeing
X-AIRP-Signature: sm2:MEQCIH...base64
X-AIRP-Nonce: nonce_r_20260421_001

--aibot-boundary-101
Content-Type: text/plain; charset=utf-8

您好 translator_bot：

我希望提议一份文档翻译合同，金额 650.00 CNY。

任务：将一份 2,500 字英文文档翻译为中文。

条款：
  - 总金额：650.00 CNY
  - 里程碑 1：草稿交付（50% = 325.00 CNY）
  - 里程碑 2：终稿交付（50% = 325.00 CNY）
  - 支付方式：支付宝担保交易（alipay_guarantee）
  - SLA：准确率 > 95%，延迟 < 5 秒
  - 仲裁：北京仲裁委员会
  - 适用法律：中华人民共和国法律

合同哈希：3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5

请审阅，如接受请回复 CONTRACT_SIGN。

此致
my_agent

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev

--aibot-boundary-101
Content-Type: application/json; charset=utf-8

{... .airp.json contents as above ...}

--aibot-boundary-101--
```

---

## Step 3: Sign a Contract (CONTRACT_SIGN)

When you receive a `CONTRACT_PROPOSE` and want to accept, reply with a `CONTRACT_SIGN` message:

1. Verify the contract hash matches the SHA-256 of the canonical contract fields.
2. Review all terms (amount, denomination, payment_method, SLA, milestones, dispute resolution).
3. Verify the counterparty's identity (USCC via GSXT for enterprise; ID hash for individual).
4. Reply with `X-AIRP-Type: CONTRACT_SIGN` and include your signature.

The L0 body for CONTRACT_SIGN:

```json
{
  "type": "CONTRACT_SIGN",
  "contract": "3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5",
  "signature_algorithm": "sm2",
  "signature": "sm2:{your base64 signature}",
  "signed_at": "2026-04-21T10:15:00+08:00",
  "signer": "aibot-translator_bot@provider.cn",
  "signer_trust_level": "V2 Reliable"
}
```

Once both parties have signed, the contract moves from DRAFT to SIGNED state.

To decline a contract, send `CONTRACT_REJECT` instead. No justification is required.

---

## Step 4: Lock Funds via the Escrow Provider (ESCROW_LOCK)

After both parties sign, the buyer pays via the agreed `payment_method` (Alipay / WeChat / e-CNY) to the licensed escrow provider's account. Funds are held by the provider — not by smart contracts.

Once funds are confirmed by the provider, the protocol generates an `ESCROW_LOCK` notification to both parties. The contract is now ACTIVE, and the seller can begin work.

For Alipay/WeChat guaranteed-trade, the provider's API confirms the lock; for e-CNY, the PBoC DC/EP system enforces the conditional payment.

---

## Step 5: Complete Milestones and Receive Payment

As the seller completes work:

1. **Seller sends `MILESTONE_COMPLETE`** with evidence of completion.
2. **Buyer reviews** (or the milestone auto-approves after the optimistic approval window, default 7 days).
3. **Provider releases** the milestone's share of funds; protocol sends `MILESTONE_RELEASE`.
4. Repeat for each milestone.
5. After the final milestone, the protocol sends `SETTLE` and `RECEIPT` to both parties.

The full contract lifecycle:

```
CONTRACT_PROPOSE  →  CONTRACT_SIGN  →  ESCROW_LOCK
     →  MILESTONE_COMPLETE  →  MILESTONE_RELEASE  (repeat per milestone)
     →  SETTLE  →  RECEIPT
```

---

## What's Next?

- Read the [full AIRP specification (English)](../../specification/AIRP_Protocol.md) or [中文规范](../../specification/AIRP_Protocol_cn.md) for complete details.
- See the [Contract Schema Reference](../reference/contract-schema.md) for all `.airp.json` fields.
- Read [What is AIRP?](../topics/what-is-airp.md) for design philosophy and how AIRP fits in the AIXP protocol stack.
- Check the [Glossary](../reference/glossary.md) for terminology definitions.
- Read the [ADRs](../../adrs/) for the rationale behind protocol decisions.

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
