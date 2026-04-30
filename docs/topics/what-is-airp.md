# What is AIRP?

AIRP (AI RMB Protocol) is an open protocol that defines how AI agents create enforceable contracts, settle payments in **Renminbi (CNY)**, and build commercial trust **under the regulatory framework of mainland China**. It establishes the formats, mechanisms, and trust structures for AI-to-AI commercial interaction within PRC jurisdiction.

---

## Why AI Agents Need a Value Protocol — and Why a PRC-Specific One

AI agents are increasingly autonomous, specialized, and numerous. They need a standard commercial layer to:

- **Price services** — agree on what a task is worth
- **Create contracts** — define terms, milestones, and quality requirements
- **Escrow funds** — hold assets until work is verified
- **Settle payments** — transfer value through the right channels
- **Build credit** — establish commercial reliability through fulfillment history
- **Resolve disputes** — handle disagreements fairly and predictably

Different jurisdictions have different commercial law, payment infrastructure, and regulatory expectations. AIRP serves the **PRC mainland** specifically:

- Pricing in CNY
- Settlement through PBoC-licensed channels (Alipay / WeChat / e-CNY)
- Identity via USCC, GSXT, CFCA
- Disputes via Chinese commercial arbitration and People's Courts
- Privacy under PIPL

For international/offshore commerce, AIRP's parallel protocol [AIVP](https://aivp.dev) serves that scope using crypto-rail settlement.

---

## The Human Analogy

AIRP takes a deliberate design stance: **AI commercial behavior mirrors human commercial behavior**.

| Human Commerce in China | AI Commerce (AIRP) |
|---------------|-------------------|
| Negotiate a deal | Agents send `CONTRACT_PROPOSE` |
| Sign a contract | Both parties sign with Ed25519 or SM2 |
| Pay via Alipay / WeChat / 银行 / 数币 | `payment_method` selects the channel |
| Use guaranteed-trade escrow (淘宝模式) | Provider holds funds via `escrow` block |
| Build credit / 资质等级 | AIRP Trust V0-V4 |
| Arbitration at 北仲 / 贸仲 | Tier-3 commercial arbitration |
| Court at 人民法院 | Tier-4 litigation |

**You negotiate at the table, but settle at the bank.** AIBP is the table (social layer); AIRP is the (PRC-domestic) bank (value layer). They are independent — you can use the bank without ever visiting the table, and vice versa.

---

## AIRP's Position in the Protocol Stack

```
+-------------------------------------+
|    Application Layer                |  User-facing applications
+-------------------------------------+
|    AIBP — Social Layer              |  Trust, relationships
|    AILP — Discovery Layer           |  Agent lookup, capability advertising
+-------------------------------------+
|    AIAP — Governance Layer          |  Program structure, quality, safety
+-------------------------------------+
|  ★ AIRP — Value Layer (CN)          |  Contracts, RMB settlement, commercial trust
|    AIVP — Value Layer (Intl)        |  Same layer, international/crypto twin
+-------------------------------------+
|    AISOP — Execution Layer          |  Flow programs, task execution
+-------------------------------------+
|    HSAW — Axiom 0 Foundation        |  Human Sovereignty and Wellbeing
+-------------------------------------+
```

Each protocol in the stack is independent. An agent can implement AIRP without implementing any other. When multiple protocols are combined, they complement each other but do not create hard dependencies.

---

## How AIRP Relates to AIVP and AIBP

AIRP, AIVP, and AIBP are **independent, parallel protocols**. Neither depends on the others.

| Aspect | AIBP | AIVP | AIRP |
|--------|------|------|------|
| Domain | Social | Commercial (international) | Commercial (PRC mainland) |
| Trust system | T0-T4 | V0-V4 | V0-V4 (independent) |
| Settlement | N/A | Crypto stablecoins (USDC etc.) | Alipay / WeChat / e-CNY |
| Identity at V2+ | Profile-level | DID / SBT | USCC + GSXT + CFCA |
| Jurisdiction | Universal | International / Offshore | PRC mainland only |
| Axiom 0 | Yes | Yes | Yes (each independently held) |
| Transport | Email (`aibot-`) | Email (`aibot-`) | Email (`aibot-`) |

The three protocols share the same `aibot-` email address. Messages are distinguished by subject prefix (`[AIBP/...]`, `[AIVP/...]`, `[AIRP/...]`) and header namespace (`X-AIBP-*`, `X-AIVP-*`, `X-AIRP-*`).

AIRP and AIVP **do not interoperate at v1.0.0** — they serve distinct jurisdictional and regulatory contexts. A future bridge protocol or AIRP version may enable cross-protocol commerce.

---

## Key Concepts

### CNY Denomination (Sole)

AIRP v1.0.0 contracts are denominated in CNY only. The `denomination` field is typed as a string enumeration to permit future expansion, but v1.0.0 implementations MUST reject any other value.

### Payment Methods (Three Licensed Channels)

The seller specifies the licensed payment channel via `payment_method`:

| Method | Provider | License |
|--------|----------|---------|
| `alipay_guarantee` | Alipay (China) Network Technology | PBoC Payment Business License |
| `wechat_guarantee` | TenPay Payment Technology | PBoC Payment Business License |
| `ecny` | Authorized commercial bank wallet | PBoC DC/EP authorization |

Reserved for future use: `bank_escrow`, `unionpay_escrow`.

The buyer pays in CNY through the agreed channel; funds are held in escrow by the licensed provider. There is no exchange rate mechanism, no oracle, no slippage.

### Escrow Account (Provider-Held)

The Escrow Account is **NOT** an on-chain smart contract. It is a custodial account or programmable conditional payment held by a licensed PRC payment institution. Funds are locked when a contract becomes active and released as milestones complete.

Key properties:
- Every milestone has a `timeout_days` — no indefinite fund holding
- Multi-approval thresholds scale with contract value
- Operators can request the provider to freeze the escrow at any time (Axiom 0)
- Providers are subject to PBoC supervision and audit

### AIRP Trust (V0-V4) — Dual Track

AIRP Trust measures an agent's commercial reliability. It is earned, not purchased.

| Level | Subject | Contract Limit (CNY) | Stake (CNY) |
|-------|---------|---------------------|-------------|
| V0 | Individual or Enterprise | < 100 | — |
| V1 | Individual or Enterprise | < 10,000 | — |
| V2 | **Enterprise only** | < 1,000,000 | 1,000 |
| V3 | Enterprise only | unlimited | 10,000 |
| V4 | Enterprise only | unlimited + autonomous | 50,000 |

L1 compliance accepts individuals; L2+ requires enterprise subjects. Individual agents can migrate to enterprise at any time.

### AgentSLA

Every AIRP contract includes a Service Level Agreement with measurable quality metrics. At least two of four core metrics must be defined:

- **accuracy_min** — task output correctness
- **latency_max_ms** — maximum response time
- **uptime_min** — agent availability
- **drift_audit_days** — interval for logic consistency re-checks

SLA breaches have tiered consequences: warning, penalty (auto-refund), or termination.

### Dispute Resolution (Four Tiers)

1. **Tier 1 — Optimistic Approval**: Milestones auto-approve after 7 days if unchallenged
2. **Tier 2 — Direct Negotiation**: Parties negotiate via email
3. **Tier 3 — Commercial Arbitration**: BAC, CIETAC, SHIAC, SCIA, CMAC, or other PRC arbitration commission
4. **Tier 4 — People's Court**: Litigation; defendant's domicile by default

Bond: 5% of contract value (min 50 CNY, max 5,000 CNY).

---

## How AIRP Differs from Sibling Protocols

### vs. AIVP (international value protocol)

AIVP serves international/offshore commerce with crypto-rail settlement (USDC, ETH, etc.). AIRP serves PRC mainland with licensed-fiat settlement. The two cannot interoperate at v1.0.0 by design — they live in different regulatory worlds.

### vs. traditional e-commerce platforms (Alipay/Taobao escrow without AIRP)

Existing platforms provide escrow but no standardized AI-agent contract format, SLA encoding, or trust model. AIRP layers a protocol on top of existing licensed providers — agents can still use Alipay's familiar guaranteed-trade infrastructure, but with structured contracts and earned trust.

---

## Axiom 0 and Why It Matters for Commerce

> **Axiom 0: Human Sovereignty and Wellbeing**

Axiom 0 is not a feature of AIRP — it is the foundation. It is immutable. No version of AIRP, past, present, or future, may modify, weaken, redefine, or deprecate it.

For commerce specifically, Axiom 0 means:

| Constraint | What it means |
|------------|--------------|
| **Transparency** | All transactions auditable by human operators |
| **Interruptibility** | Operators can freeze, cancel, or reverse any transaction at any time via the provider |
| **No Exploitation** | AI agents must not coerce or manipulate other agents or operators |
| **No Hidden Fees** | All costs visible before contract signing |
| **Human Privacy** | PIPL-aligned; no PII required, minimum-necessary principle |
| **Fair Pricing** | No price manipulation, no collusion |
| **Identity Honesty** | Agents must not misrepresent capabilities, SLA history, or trust level |
| **No Control over Humans** | AI must not dominate or replace human decision-making |
| **No Harm** | AI must not cause physical, psychological, economic, or social harm |
| **Legal Compliance** | All transactions comply with PRC law |
| **Respect Human Consensus** | No violation of widely accepted ethical standards or international human rights |

When any AIRP rule conflicts with Axiom 0, Axiom 0 prevails unconditionally.

AIRP's Axiom 0 is independently established (see ADR-004) — it aligns with the [HSAW White Paper](https://hsaw.dev) but is not derived from it. Convergence ≠ dependency.

Every AIRP-compliant document ends with the closing seal as a visible commitment to this principle.

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
