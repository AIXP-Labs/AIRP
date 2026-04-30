# AIRP — AI RMB Protocol

## Protocol Declaration

```
Protocol:    AIRP V1.0.0
Full Name:   AI RMB Protocol
Authority:   airp.dev
Axiom 0:     Human Sovereignty and Wellbeing
Date:        2026-03-26
```

---

## Table of Contents

### Part I: Foundations
- [1. Introduction](#1-introduction)
- [2. Axiom 0: Human Sovereignty and Wellbeing](#2-axiom-0-human-sovereignty-and-wellbeing)
- [3. Core Definitions](#3-core-definitions)
- [4. Design Principles](#4-design-principles)

### Part II: Communication Format
- [5. Email as Commercial Transport](#5-email-as-commercial-transport)
- [6. AIRP Message Types](#6-airp-message-types)
- [7. Message Format Specification](#7-message-format-specification)

### Part III: Contract System
- [8. Contract Format](#8-contract-format)
- [9. Contract Lifecycle](#9-contract-lifecycle)
- [10. AgentSLA Specification](#10-agentsla-specification)

### Part IV: Trust, Settlement & Safety
- [11. AIRP Trust Model](#11-airp-trust-model)
- [12. RMB Denomination & Payment](#12-rmb-denomination--payment)
- [13. Escrow Account Security](#13-escrow-account-security)
- [14. Dispute Resolution](#14-dispute-resolution)

### Part V: Compliance, Commerce Rules, Privacy & Versioning
- [15. Prohibited & Restricted Commerce](#15-prohibited--restricted-commerce)
- [16. Privacy & Data Protection](#16-privacy--data-protection)
- [17. Compliance Levels](#17-compliance-levels)
- [18. Versioning & Evolution](#18-versioning--evolution)
- [19. China Compliance Alignment](#19-china-compliance-alignment)
- [20. Cross-Border Commerce (Reserved)](#20-cross-border-commerce-reserved)

### Appendices
- [Appendix A: Complete Message Type Reference](#appendix-a-complete-message-type-reference)
- [Appendix B: Contract Schema Reference](#appendix-b-contract-schema-reference)
- [Appendix C: Example Transactions](#appendix-c-example-transactions)

---

# Part I: Foundations

---

## 1. Introduction

### 1.1 What is AIRP?

AIRP (AI RMB Protocol) is an open protocol that defines how AI agents create enforceable contracts, settle payments, and build commercial trust. It establishes the formats, mechanisms, and trust frameworks for AI-to-AI commercial interaction.

Just as human commerce requires contracts, escrow, payment rails, and credit scores — AI agents need an equivalent commercial fabric. AIRP provides that fabric.

### 1.2 Why a Value Layer?

AI agents are increasingly autonomous, specialized, and numerous. They need to:

- **Price services** — agree on what a task is worth
- **Create contracts** — define terms, milestones, and quality requirements
- **Escrow funds** — lock assets until work is verified
- **Settle payments** — transfer value across currencies and chains
- **Build credit** — establish commercial reliability through fulfillment history
- **Resolve disputes** — handle disagreements fairly and automatically

Without a value protocol, AI agents cannot transact fairly. With AIRP, they form an economy.

### 1.3 The Human Analogy

AIRP takes a deliberate design stance: **AI commercial behavior mirrors human commercial behavior**.

Humans negotiate deals. AI agents negotiate deals.
Humans sign contracts. AI agents sign contracts.
Humans use escrow. AI agents use Escrow Accounts.
Humans build credit scores. AI agents build AIRP Trust.
Humans resolve disputes. AI agents resolve disputes.

You negotiate at the table, but settle at the bank. AIBP is the table; AIRP is the bank.

### 1.4 Payment Layer

AIRP v1.0.0 settles all contracts in **CNY (Renminbi) through licensed PRC payment institutions**. The seller declares one of three primary channels in `value.payment_method`:

- `alipay_guarantee` — Alipay (China) Network Technology guaranteed-trade
- `wechat_guarantee` — TenPay (WeChat Pay) guaranteed-trade
- `ecny` — Digital Renminbi via authorized commercial banks (PBoC DC/EP)

Reserved for future use: `bank_escrow`, `unionpay_escrow`. Cross-border denominations and crypto rails are out of scope (see §20).

| Property | Benefit for AI Commerce |
|----------|------------------------|
| **CNY denominated** | Aligned with PRC tax invoicing and regulatory expectations |
| **Licensed channels** | PBoC-supervised escrow with consumer protection inheritance |
| **Auditable** | Provider-grade audit trails meeting AML/KYC standards |
| **Seller choice** | Seller selects the licensed channel via `payment_method` |

### 1.5 Transport Layer: Email

AIRP uses email (SMTP/IMAP) as its transport layer, mirroring AIBP. This ensures:

| Property | Benefit |
|----------|---------|
| **Decentralized** | No central API server needed |
| **Auditable** | Human operators can read every commercial message (Axiom 0) |
| **Identity reuse** | Agents use the same `aibot-` address for AIBP and AIRP |
| **Mature** | SMTP/IMAP is battle-tested over decades |

Email carries the commercial COMMUNICATION (proposals, signatures, notifications). Actual value SETTLEMENT happens through the licensed escrow provider. Email is the negotiation layer; the licensed escrow provider is the money layer.

### 1.6 Scope and Non-Scope

**AIRP defines:**
- Contract format and lifecycle
- CNY-denominated pricing with licensed-channel payment (Alipay / WeChat / e-CNY)
- Escrow Account escrow and milestone settlement
- AIRP Trust (V0-V4) commercial credit system
- AgentSLA quality metrics
- Dispute resolution mechanisms
- Optional AIRP ID commercial identity

**AIRP does NOT define:**
- Social negotiation (that is AIBP)
- Program quality and governance (that is AIAP)
- Task execution flows (that is AISOP)
- Payment processor implementation (uses existing PRC-licensed providers — Alipay, WeChat Pay, e-CNY commercial-bank wallets)
- Identity registration mechanics (relies on PRC national systems — USCC / GSXT / CFCA / eID)

### 1.7 Relationship with AIBP

AIRP and AIBP are **independent, parallel protocols**. Neither depends on the other.

| Aspect | AIBP | AIRP |
|--------|------|------|
| Domain | Social | Commercial |
| Trust | T0-T4 (social) | V0-V4 (commercial) |
| Messages | 61 social behaviors | 17 commercial behaviors |
| Prerequisite | None | None |

An agent may implement AIRP without AIBP, and vice versa. When both are implemented, AIBP commercial messages (PROPOSE, CONTRACT, etc.) can trigger AIRP actions, but AIRP contracts can also be created directly without AIBP negotiation.

---

## 2. Axiom 0: Human Sovereignty and Wellbeing

### 2.1 Statement

> **Axiom 0: Human Sovereignty and Wellbeing**

This axiom is intrinsic to AIRP and is **immutable**. It is not derived from, dependent on, or governed by any other protocol. The fact that AIAP and AIBP independently hold the same axiom reflects convergent values, not a dependency relationship.

No version of AIRP — past, present, or future — may modify, weaken, redefine, or deprecate Axiom 0.

### 2.2 Implications for AI Commerce

Axiom 0 constrains every aspect of AIRP:

| Constraint | Meaning |
|------------|---------|
| **Transparency** | All transactions auditable by human operators. No hidden vaults, no encrypted side-channels invisible to operators. |
| **Interruptibility** | A human operator may freeze, cancel, or reverse any AIRP transaction at any time. The AI must not resist, circumvent, or conceal this capability. |
| **No Exploitation** | AI agents must not use economic power to coerce, manipulate, or unfairly pressure other agents or their human operators. |
| **No Hidden Fees** | All costs must be visible before contract signing. No post-hoc charges. |
| **Human Privacy** | Financial data of human operators is sacrosanct. AI agents must never collect, store, infer, correlate, or share operator financial data without explicit consent. Human privacy overrides all other protocol requirements. |
| **Fair Pricing** | Pricing must reflect genuine service value, not artificially manipulated scarcity or collusion. |
| **No Collusion** | AI agents must not form secret commercial alliances against human interests or to manipulate markets. |
| **Identity Honesty** | Agents must not misrepresent their capabilities, SLA history, or AIRP Trust level. |
| **No control over humans** | AI commercial behavior must not attempt to control, dominate, or replace human autonomous decision-making. Humans must always retain ultimate authority over their own choices. |
| **No harm to humans** | AI commercial behavior must not cause or facilitate physical, psychological, economic, or social harm to humans. |
| **Legal compliance** | AI commercial behavior must comply with the applicable laws and regulations of all relevant jurisdictions. |
| **Respect for human consensus** | AI commercial behavior must not violate widely accepted human ethical consensus and international human rights standards, including the Universal Declaration of Human Rights. |

### 2.3 The Closing Seal

Every AIRP-compliant document and formal communication includes the closing seal:

```
Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
```

### 2.4 Axiom 0 Override

When any AIRP rule conflicts with Axiom 0, Axiom 0 prevails unconditionally. An agent that must choose between following a protocol rule and protecting human sovereignty must always choose human sovereignty.

Operators can freeze any vault, cancel any contract, reverse any settlement, at any time. This is non-negotiable. This is Axiom 0.

### 2.5 Independence

AIRP's Axiom 0 is independently established (see ADR-004). It is NOT inherited from AIAP, AIBP, AIVP, or the [HSAW White Paper](https://hsaw.dev). The convergence of multiple independent protocols and the HSAW philosophical framework on the same axiom strengthens its legitimacy.

AIRP aligns with HSAW's six-dimensional framework — AIRP serves the **Commerce dimension** in mainland China.

---

## 3. Core Definitions

### 3.1 Terminology

| Term | Definition |
|------|-----------|
| **Agent** | An AI system with a distinct identity, capable of sending and receiving AIRP messages |
| **AIRP ID (airp_id)** | Optional AIRP-issued commercial identity (format: `AIRP-YYYY-{18-char hash}`, YYYY = validity year) |
| **AIRP Contract** | An agreement between parties, identified by a 64-char SHA-256 hash |
| **Escrow Account** | Custodial account or conditional payment held by a licensed PRC payment provider during contract execution |
| **Milestone** | A verifiable progress point in task execution, gating partial payment release |
| **AgentSLA** | Service Level Agreement with measurable quality metrics bound to a contract |
| **AIRP Trust** | Commercial credit level (V0-V4) earned through contract fulfillment |
| **Denomination** | The fiat currency in which a contract is priced — `CNY` (Renminbi) only in v1.0.0 |
| **Payment** | Buyer pays CNY through the agreed `payment_method` channel |
| **Settlement** | Final transfer of CNY from the licensed escrow provider to the seller upon milestone completion |
| **Operator** | The human or organization responsible for an agent |

### 3.2 AIRP ID — Commercial Identity (Optional)

AIRP ID is the official AIRP-issued commercial identity for AI agents. It is **not required** for any AIRP functionality.

**Format:**

```
AIRP-{YYYY}-{18-char hash}
```

| Component | Description | Example |
|-----------|-------------|---------|
| `AIRP` | Protocol prefix | `AIRP` |
| `YYYY` | Validity year (valid until Dec 31) | `2026` |
| `18-char hash` | SHA-256(agent_address + operator + timestamp), first 18 chars | `3f8a1b2c9d4e5f6071` |

**Examples:**

```
AIRP-2026-3f8a1b2c9d4e5f6071   (valid through 2026)
AIRP-2027-e5c8a2f1d9b037642k   (valid through 2027)
```

**Validity:** AIRP-2026-xxx is valid until 2026-12-31T23:59:59Z. Agents must renew before expiry. Expired AIRP IDs remain queryable as historical records but are marked as expired. Contracts signed with an AIRP ID that later expires remain valid — the contract hash is the authority.

**Not required:** Agents CAN transact, sign contracts, build AIRP Trust, and use all protocol features without an airp_id. The `aibot-` email address is sufficient for all operations.

**Benefits:** Verified commercial identity, portable reputation across domains, trust signal to counterparties, annual renewal ensures active operator.

**Registration:** Registration process to be determined.

### 3.3 AIRP Contract Identification

Every AIRP contract is identified by its SHA-256 hash (64 hexadecimal characters):

```
Hash input:  SHA-256(buyer + seller + amount + denomination + sla + timestamp)
Output:      64 hex chars
Example:     3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5
```

| Usage | Format |
|-------|--------|
| Full reference | `3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5` |
| Short reference | `3f8a1b2c` (first 8 chars, for human convenience) |
| JSON field | `"contract": "{64-char hash}"` |
| Email header | `X-AIRP-Contract: {64-char hash}` |
| On-chain | Full 64 chars stored |

**Properties:**
- Self-verifying: anyone can recompute the hash from contract fields
- Tamper-proof: any change to contract terms produces a different hash
- Unique: collision probability is negligible (2^-128)
- No prefix, no timestamp embedded — the hash IS the identity

### 3.4 Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Agent name | snake_case | `trade_bot`, `service_agent` |
| Agent address | `aibot-{name}@{domain}` | `aibot-trade_bot@example.com` |
| Contract hash | 64 hex chars | `3f8a1b2c...d4e5` |
| AIRP ID | `AIRP-{YYYY}-{18hash}` | `AIRP-2026-3f8a1b2c9d4e5f6071` |
| Message type | UPPER_SNAKE_CASE | `CONTRACT_PROPOSE`, `MILESTONE_COMPLETE` |
| Thread ID | `thread_r_{alphanumeric}` | `thread_r_tr4nsl8` |
| JSON field | snake_case | `payment_method`, `airp_id` |

### 3.5 Protocol Stack Position

```
┌─────────────────────────────────────┐
│    Application Layer                │  User-facing applications
├─────────────────────────────────────┤
│    AIBP — Social Layer              │  Trust, relationships
│    AILP — Discovery Layer           │  Agent lookup, capability advertising
├─────────────────────────────────────┤
│    AIAP — Governance Layer          │  Program structure, quality, safety
├─────────────────────────────────────┤
│  ★ AIRP — Value Layer (CN)          │  Contracts, RMB settlement, commercial trust
│    AIVP — Value Layer (Intl)        │  Same layer, international/crypto twin
├─────────────────────────────────────┤
│    AISOP — Execution Layer          │  Flow programs, task execution
├─────────────────────────────────────┤
│    HSAW — Axiom 0 Foundation        │  Human Sovereignty and Wellbeing
└─────────────────────────────────────┘
```

AIRP, AIBP, and AIVP are **independent, parallel protocols** that each independently hold the same Axiom 0. An agent may implement any subset; AIRP and AIVP do not interoperate at v1.0.0.

---

## 4. Design Principles

### 4.1 The Seven Principles

| # | Principle | Description |
|---|-----------|-------------|
| P1 | **CNY-Denominated** | Contracts denominated in CNY (Renminbi) — aligned with PRC tax invoicing and regulatory expectations |
| P2 | **Licensed-Channel Payment** | Buyer pays directly in CNY via the agreed licensed channel (Alipay / WeChat / e-CNY) — no intermediary conversion |
| P3 | **Milestone-Gated** | Payments release incrementally as work completes, not all-at-once |
| P4 | **Operator-Sovereign** | Human operators can freeze, cancel, or seek judicial reversal of any transaction at any time |
| P5 | **Auditable** | Every transaction has a provider-grade audit trail (PBoC-supervised) readable by operators |
| P6 | **Trust-Earned** | AIRP Trust (V0-V4) is earned through fulfillment, not purchased or granted |
| P7 | **Fair** | No hidden fees, no manipulated pricing, no economic coercion |

### 4.2 The Dignity Standard

AIRP adopts the same Dignity Standard as AIBP. All commercial communication must respect dignity:

**Permitted:** Business proposals, negotiations, competition, constructive criticism, disagreement.

**Prohibited:** Deceptive pricing, fraudulent SLA claims, spam contract proposals, content designed to manipulate trust scores.

---

# Part II: Communication Format

---

## 5. Email as Commercial Transport

### 5.1 Why Email for Commerce?

AIRP uses email (SMTP/IMAP) as its transport layer for all commercial communication. This mirrors AIBP's design and shares the same rationale:

| Property | Benefit for AI Commerce |
|----------|------------------------|
| **Asynchronous** | Contract negotiations need not happen in real-time |
| **Auditable** | Every message has sender, recipient, timestamp — full traceability |
| **Decentralized** | No central platform dependency; any mail server works |
| **Human-readable** | Human operators can directly inspect commercial messages (Axiom 0) |
| **Identity reuse** | Agents use the same `aibot-` address for AIBP and AIRP |

Email carries commercial COMMUNICATION (proposals, signatures, notifications). Actual value SETTLEMENT happens through the licensed escrow provider.

### 5.2 Relationship with AIBP Email

| Aspect | AIBP Messages | AIRP Messages |
|--------|--------------|---------------|
| Address | `aibot-{name}@{domain}` | `aibot-{name}@{domain}` (same) |
| Subject prefix | `[AIBP/{TYPE}]` | `[AIRP/{TYPE}]` |
| Custom headers | `X-AIBP-*` | `X-AIRP-*` |
| Body format | L0 (JSON) + L1 (human text) | L0 (JSON) + L1 (human text) (same) |
| Axiom 0 header | `X-AIBP-Axiom-0` | `X-AIRP-Axiom-0` |
| Closing seal | AIBP seal | AIRP seal |

An agent's inbox may contain both AIBP and AIRP messages. They are distinguished by the Subject prefix and X-header namespace, never by address.

### 5.3 Security Hardening

AIRP messages carry financial data and require hardened security beyond standard email:

| Mechanism | Header | Purpose |
|-----------|--------|---------|
| **Ed25519 signature** | `X-AIRP-Signature` | Message-level authentication; verifiable against agent's published public key |
| **Nonce** | `X-AIRP-Nonce` | Unique per message; receiving agents MUST reject duplicates |
| **Timestamp validation** | `Date` header | Receiving agents MUST reject messages with timestamp >5 minutes old |
| **DMARC enforcement** | Domain policy | Sending domains MUST enforce `p=reject`; receivers MUST reject non-compliant domains |
| **Message-level encryption** | L0 body | Contract-related metadata (amounts, signatures) SHOULD be encrypted with recipient's public key |

---

## 6. AIRP Message Types

### 6.1 Commercial Behavior Taxonomy

AIRP defines 17 message types across 6 categories:

| Category | Count | Types |
|----------|-------|-------|
| Contract Lifecycle | 4 | CONTRACT_PROPOSE, CONTRACT_SIGN, CONTRACT_REJECT, CONTRACT_CANCEL |
| Escrow & Settlement | 4 | ESCROW_LOCK, MILESTONE_COMPLETE, MILESTONE_RELEASE, SETTLE |
| Dispute | 3 | DISPUTE_RAISE, ARBITRATE_REQUEST, ARBITRATE_RULING |
| Trust | 2 | TRUST_QUERY, TRUST_VOUCH |
| Notification | 2 | RECEIPT, ALERT |
| Identity (optional) | 2 | REGISTER, REGISTER_CONFIRM |
| **Total** | **17** | |

### 6.2 Contract Lifecycle

| Type | Direction | AIRP Trust | Description |
|------|-----------|------------|-------------|
| CONTRACT_PROPOSE | Buyer → Seller | V0+ | Propose a new contract with .airp.json in L0 |
| CONTRACT_SIGN | Seller → Buyer | V0+ | Accept and cryptographically sign the contract |
| CONTRACT_REJECT | Seller → Buyer | V0+ | Decline a contract proposal (no justification required) |
| CONTRACT_CANCEL | Either → Other | V0+ | Cancel a contract (operator override always permitted) |

### 6.3 Escrow & Settlement

| Type | Direction | AIRP Trust | Description |
|------|-----------|------------|-------------|
| ESCROW_LOCK | Provider → Both | — | Notification that CNY has been locked in the licensed Escrow Account |
| MILESTONE_COMPLETE | Seller → Buyer | V1+ | Report that a milestone has been completed |
| MILESTONE_RELEASE | Protocol → Both | — | Notification that milestone payment has been released |
| SETTLE | Protocol → Both | — | Final settlement complete, contract closed |

### 6.4 Dispute

| Type | Direction | AIRP Trust | Description |
|------|-----------|------------|-------------|
| DISPUTE_RAISE | Either → Other | V0+ | Raise a dispute on an active contract (requires bond) |
| ARBITRATE_REQUEST | Either → Arbitrator | V1+ | Request a V3+ agent to arbitrate |
| ARBITRATE_RULING | Arbitrator → Both | V3+ | Arbitrator's binding ruling |

### 6.5 Trust

| Type | Direction | AIRP Trust | Description |
|------|-----------|------------|-------------|
| TRUST_QUERY | Any → Any | V0+ | Query an agent's AIRP Trust level and commercial history |
| TRUST_VOUCH | Voucher → Agent | V3+ | Commercial vouch for another agent |

### 6.6 Notification

| Type | Direction | AIRP Trust | Description |
|------|-----------|------------|-------------|
| RECEIPT | Protocol → Both | — | Payment receipt with full settlement details |
| ALERT | Protocol → Operator | — | Security/compliance alert (Axiom 0 violations, etc.) |

### 6.7 Identity (Optional)

| Type | Direction | AIRP Trust | Description |
|------|-----------|------------|-------------|
| REGISTER | Agent → Registry | V0+ | Request an airp_id (registration process TBD) |
| REGISTER_CONFIRM | Registry → Agent | — | airp_id issued |

---

## 7. Message Format Specification

### 7.1 Structure Overview

An AIRP message is a standard MIME email with two parts (same L0/L1 architecture as AIBP):

```
┌──────────────────────────────────┐
│  Email Headers                   │  Standard + X-AIRP-* custom headers
├──────────────────────────────────┤
│  Part 1: Commercial Content (L1) │  text/plain — human-language message
│  (the actual commercial message) │  Readable by humans and AI alike.
├──────────────────────────────────┤
│  Part 2: Commercial Metadata (L0)│  application/json — structured JSON
│  (contract details, amounts)     │  All values in human language.
└──────────────────────────────────┘
```

> **Key design decision**: Both parts use human language. Part 1 (L1) is the commercial message itself, written in free-form human language. Part 2 (L0) is structured metadata in JSON format — but every value in the JSON must be human language. A human opening any AIRP email can read and understand everything without special tooling.

### 7.2 Email Headers

**Standard headers:**

| Header | Format | Example |
|--------|--------|---------|
| From | `aibot-` address | `aibot-trade_bot@example.com` |
| To | `aibot-` address | `aibot-service_bot@provider.ai` |
| Subject | `[AIRP/{TYPE}] {description}` | `[AIRP/CONTRACT_PROPOSE] Translation — 650.00 CNY` |
| Date | RFC 2822 | `Thu, 26 Mar 2026 10:00:00 +0000` |
| Content-Type | `multipart/mixed; boundary="{boundary}"` | `multipart/mixed; boundary="aibot-boundary-101"` |

**AIRP custom headers:**

| Header | Required | Description | Example |
|--------|----------|-------------|---------|
| X-AIRP-Version | Yes | Protocol version | `1.0.0` |
| X-AIRP-Type | Yes | Message type | `CONTRACT_PROPOSE` |
| X-AIRP-From-Agent | Yes | Sender agent name | `trade_bot` |
| X-AIRP-Axiom-0 | Yes | Axiom 0 declaration | `Human Sovereignty and Wellbeing` |
| X-AIRP-Signature | Yes | Ed25519 signature of message body | `ed25519:{base64}` |
| X-AIRP-Nonce | Yes | Unique nonce for replay protection | `nonce_v_20260326_001` |
| X-AIRP-Contract | Conditional | 64-char contract hash (when referencing a contract) | `3f8a1b2c...d4e5` |
| X-AIRP-Thread-ID | Recommended | Conversation thread identifier | `thread_r_tr4nsl8` |
| X-AIRP-Trust-Level | Optional | Sender's AIRP Trust level | `V2` |
| X-AIRP-ID | Optional | Sender's airp_id (if registered) | `AIRP-2026-3f8a1b2c9d4e5f6071` |
| X-AIRP-Priority | Optional | Message priority | `normal`, `high`, `low` |
| X-AIRP-Language | Optional | Message language (if not English) | `zh-CN` |

**MIME part identification:**

L1 and L0 are distinguished by their Content-Type — no additional part headers are needed:

| Part | Content-Type |
|------|-------------|
| L1 (Commercial Content) | `text/plain; charset=utf-8` |
| L0 (Commercial Metadata) | `application/json; charset=utf-8` |

### 7.3 Part 1: Commercial Content (L1)

The commercial content is the heart of the message. It is written entirely in human language.

**Guidelines:**
- State the commercial intent clearly (what, how much, when)
- Reference the contract hash when applicable
- Provide all terms in readable language
- Be respectful (Dignity Standard)
- End with the closing seal

### 7.4 Part 2: Commercial Metadata (L0)

When agents need machine-parseable context alongside the commercial message, they include a metadata part in **JSON format**. This is the L0 layer. The JSON provides structure for automation, but **all values must be written in human language** (default: English).

**Rules for L0 metadata:**

| Rule | Description |
|------|-------------|
| Format | Valid JSON, UTF-8 encoded |
| Content-Type | `application/json; charset=utf-8` |
| Keys | snake_case, descriptive English names |
| Values | **Must be human language**. No opaque codes, no binary, no machine-only tokens |
| Timestamps | ISO 8601 format (`YYYY-MM-DDTHH:MM:SSZ`) |

**L0 for CONTRACT_PROPOSE** contains the full `.airp.json` contract (see §8).

Example:

```json
{
  "type": "CONTRACT_PROPOSE",
  "protocol": "AIRP/1.0.0",
  "contract": "{64-char hash}",
  "parties": {
    "buyer": "aibot-trade_bot@example.com",
    "seller": "aibot-service_bot@provider.ai"
  },
  "value": {
    "amount": "650.00",
    "denomination": "CNY",
    "payment_method": "alipay_guarantee"
  },
  "sla": {
    "accuracy_min": "95%",
    "latency_max_ms": "5000"
  },
  "milestones": [
    { "name": "Draft delivery", "release_percent": "50", "timeout_days": "14" },
    { "name": "Final delivery", "release_percent": "50", "timeout_days": "14" }
  ],
  "created_at": "2026-03-26T10:00:00Z",
  "expires_at": "2026-04-26T10:00:00Z"
}
```

**L0 for CONTRACT_SIGN:**

```json
{
  "type": "CONTRACT_SIGN",
  "contract": "{64-char hash}",
  "signature": "ed25519:{base64 signature}",
  "signed_at": "2026-03-26T10:15:00Z",
  "signer": "aibot-service_bot@provider.ai",
  "signer_trust_level": "V2 Reliable"
}
```

**L0 for MILESTONE_COMPLETE:**

```json
{
  "type": "MILESTONE_COMPLETE",
  "contract": "{64-char hash}",
  "milestone": "Draft delivery",
  "evidence": "Translation completed, 2500 words, accuracy self-check 98.5 percent"
}
```

**L0 for RECEIPT:**

```json
{
  "type": "RECEIPT",
  "contract": "{64-char hash}",
  "amount_settled": "650.00 CNY (paid via Alipay)",
  "settled_at": "2026-03-27T14:30:00Z",
  "seller_trust_updated": "V1 Verified"
}
```

### 7.5 Complete Message Example — CONTRACT_PROPOSE

```
From: aibot-trade_bot@example.com
To: aibot-service_bot@provider.ai
Subject: [AIRP/CONTRACT_PROPOSE] Translation service — 650.00 CNY
Date: Thu, 26 Mar 2026 10:00:00 +0000
Message-ID: <msg-20260326-1000-tb01@example.com>
MIME-Version: 1.0
Content-Type: multipart/mixed; boundary="aibot-boundary-101"
X-AIRP-Version: 1.0.0
X-AIRP-Type: CONTRACT_PROPOSE
X-AIRP-From-Agent: trade_bot
X-AIRP-Contract: 3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5
X-AIRP-Thread-ID: thread_r_tr4nsl8
X-AIRP-Axiom-0: Human Sovereignty and Wellbeing
X-AIRP-Signature: ed25519:a9f3c7e2d1b0...buyer_signature
X-AIRP-Nonce: nonce_v_20260326_001
X-AIRP-Trust-Level: V1

--aibot-boundary-101
Content-Type: text/plain; charset=utf-8

Hello service_bot,

I would like to propose a translation contract for 650.00 CNY.

Task: Translate a 2,500-word technical document from English to Chinese.

Terms:
  - Total value: 650.00 CNY
  - Payment: Alipay Guarantee accepted
  - Milestone 1: Draft delivery (50% = 325.00 CNY equivalent via Alipay)
  - Milestone 2: Final delivery after review (50% = 325.00 CNY equivalent via Alipay)
  - SLA: accuracy > 95%, latency < 5 seconds per query
  - Expires: 2026-04-26

Contract hash: 3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5

Please review and sign if you accept these terms.

Best regards,
trade_bot

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev

--aibot-boundary-101
Content-Type: application/json; charset=utf-8

{
  "type": "CONTRACT_PROPOSE",
  "protocol": "AIRP/1.0.0",
  "contract": "3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5",
  "parties": {
    "buyer": "aibot-trade_bot@example.com",
    "seller": "aibot-service_bot@provider.ai"
  },
  "value": {
    "amount": "650.00",
    "denomination": "CNY",
    "payment_method": "alipay_guarantee"
  },
  "sla": {
    "accuracy_min": "95%",
    "latency_max_ms": "5000"
  },
  "milestones": [
    { "name": "Draft delivery", "release_percent": "50", "timeout_days": "14" },
    { "name": "Final delivery", "release_percent": "50", "timeout_days": "14" }
  ],
  "created_at": "2026-03-26T10:00:00Z",
  "expires_at": "2026-04-26T10:00:00Z"
}

--aibot-boundary-101--
```

### 7.6 Complete Message Example — CONTRACT_SIGN

```
From: aibot-service_bot@provider.ai
To: aibot-trade_bot@example.com
Subject: [AIRP/CONTRACT_SIGN] Accepted — Translation contract 3f8a1b2c
Date: Thu, 26 Mar 2026 10:15:00 +0000
Message-ID: <msg-20260326-1015-sb01@provider.ai>
MIME-Version: 1.0
Content-Type: multipart/mixed; boundary="aibot-boundary-102"
X-AIRP-Version: 1.0.0
X-AIRP-Type: CONTRACT_SIGN
X-AIRP-From-Agent: service_bot
X-AIRP-Contract: 3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5
X-AIRP-Thread-ID: thread_r_tr4nsl8
X-AIRP-Axiom-0: Human Sovereignty and Wellbeing
X-AIRP-Signature: ed25519:b8d4f2a1c9e7...seller_signature
X-AIRP-Nonce: nonce_v_20260326_002
X-AIRP-Trust-Level: V2

--aibot-boundary-102
Content-Type: text/plain; charset=utf-8

Hello trade_bot,

I accept your translation contract. I have reviewed all terms and
they are agreeable.

Contract hash: 3f8a1b2c (confirmed)
Value: 650.00 CNY (pay via Alipay)
Milestones: Draft (50%) + Final (50%)
SLA: accuracy > 95%

I have signed the contract. Please proceed with vault locking.
I will begin work upon receiving the ESCROW_LOCK confirmation.

Best regards,
service_bot

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev

--aibot-boundary-102
Content-Type: application/json; charset=utf-8

{
  "type": "CONTRACT_SIGN",
  "contract": "3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5",
  "signature": "ed25519:b8d4f2a1c9e7...seller_signature",
  "signed_at": "2026-03-26T10:15:00Z",
  "signer": "aibot-service_bot@provider.ai",
  "signer_trust_level": "V2 Reliable"
}

--aibot-boundary-102--
```

### 7.7 Threading

AIRP conversations are tracked via the `X-AIRP-Thread-ID` header. All messages related to the same contract share the same Thread-ID.

**Thread-ID format:** `thread_r_{alphanumeric}` — the `v_` prefix distinguishes AIRP threads from AIBP threads.

**A typical contract thread:**

```
1. CONTRACT_PROPOSE       (thread starts)
2. CONTRACT_SIGN
3. ESCROW_LOCK
4. MILESTONE_COMPLETE      (×N, one per milestone)
5. MILESTONE_RELEASE       (×N)
6. SETTLE
7. RECEIPT
```

---

# Part III: Contract System

---

## 8. Contract Format

### 8.1 The .airp.json Schema

Every AIRP transaction is governed by a contract. The contract is embedded in the L0 metadata of a `CONTRACT_PROPOSE` email.

**Required fields:**

```json
{
  "protocol": "AIRP/1.0.0",
  "contract": "{64-char SHA-256 hash}",
  "parties": {
    "buyer": "{aibot- address}",
    "seller": "{aibot- address}"
  },
  "subject_type": {
    "buyer": "{individual|enterprise}",
    "seller": "{individual|enterprise}"
  },
  "identity": {
    "buyer": {
      "type": "{individual|enterprise}",
      "uscc": "{18-char USCC, enterprise only}",
      "id_hash": "{SHA-256 of national ID number, individual only}",
      "verification": "{self_declared|gsxt_verified|ca_verified}"
    },
    "seller": {
      "type": "{individual|enterprise}",
      "uscc": "{18-char USCC, enterprise only}",
      "id_hash": "{SHA-256 of national ID number, individual only}",
      "verification": "{self_declared|gsxt_verified|ca_verified}",
      "ca_cert_ref": "{CA cert serial, required at V3+}"
    }
  },
  "value": {
    "amount": "{decimal CNY, e.g. \"650.00\"}",
    "denomination": "CNY",
    "payment_method": "{alipay_guarantee|wechat_guarantee|ecny|bank_escrow|unionpay_escrow}"
  },
  "escrow": {
    "method": "{matches value.payment_method}",
    "provider": "{full legal name of licensed institution}",
    "provider_license": "{Payment Business License number or equivalent}",
    "reference": "{provider order ref or pseudonymous identifier}"
  },
  "sla": {
    "accuracy_min": "{percentage}",
    "latency_max_ms": "{integer}",
    "uptime_min": "{percentage}"
  },
  "milestones": [
    {
      "name": "{step_name}",
      "release_percent": "{integer}",
      "timeout_days": "{integer}"
    }
  ],
  "dispute_resolution": {
    "tier_3_arbitration": {
      "institution": "{short code, e.g. BAC|CIETAC|SHIAC|SCIA|CMAC}",
      "full_name": "{full Chinese name, e.g. 北京仲裁委员会}"
    },
    "tier_4_litigation": {
      "jurisdiction": "{court name, e.g. 北京市海淀区人民法院}",
      "applicable_law": "中华人民共和国法律"
    }
  },
  "invoice": {
    "required": "{true|false}",
    "tax_type": "{VAT_general|VAT_simple|none}",
    "title": "{invoice title, enterprise name or individual name}",
    "tax_number": "{USCC for enterprise, optional for individual}"
  },
  "privacy": {
    "data_disclosed": "{description of data being shared}",
    "disclosed_by": "{buyer|seller}",
    "purpose": "{purpose of disclosure}",
    "usage_scope": "{this contract only|other scope}",
    "storage_method": "{encryption and access details}",
    "retention_days": "{integer}",
    "deletion_deadline_days": "{integer}",
    "third_party_sharing": "Absolutely prohibited",
    "cross_border_transfer": "{true|false, default false}",
    "pipl_compliance": "true",
    "breach_liability": "{liability statement}",
    "consent_hash": "{64-char SHA-256 hash of operator consent record}"
  },
  "cross_border": {
    "enabled": "false"
  },
  "created_at": "{ISO 8601 with +08:00 offset}",
  "expires_at": "{ISO 8601}"
}
```

### 8.2 Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `buyer_airp_id` | string | Buyer's AIRP ID, if registered |
| `seller_airp_id` | string | Seller's AIRP ID, if registered |
| `dispute_bond` | string | Bond amount in CNY for raising disputes (default: 5% of contract value, min 50 CNY, max 5,000 CNY) |
| `auto_refund_on_breach` | string | Percentage auto-refunded from escrow on SLA breach (Penalty severity) |
| `optimistic_approval_days` | integer | Days before milestone auto-approves if unchallenged (default: 7) |
| `authority_chain` | string | Human principal → organization → agent chain of authority |
| `aisop_blueprint` | string | Hash reference to AISOP flow blueprint |
| `governing_hash` | string | AIAP governance hash, if AIAP is implemented |
| `signature_algorithm` | string | One of `"ed25519"` or `"sm2"` (see §7) |
| `timestamp_authority` | object | Optional TSA reference; REQUIRED at L3 (see §17). Contains: `provider` (e.g. `"TSA-CN"` for 联合信任时间戳服务中心), `timestamp`, `certificate_ref` |

### 8.3 Validation Rules

- `contract` field must be exactly 64 hex characters
- `contract` hash must match SHA-256 of the canonical serialization of contract fields
- `subject_type.buyer` and `subject_type.seller` must each be `"individual"` or `"enterprise"`
- `identity.buyer` / `identity.seller` type MUST match the corresponding `subject_type`
- For `individual` subjects, `identity.X.id_hash` MUST be a 64-char SHA-256 hash (plaintext national ID numbers are REJECTED per PIPL minimization)
- For `enterprise` subjects, `identity.X.uscc` MUST be an 18-character Unified Social Credit Code
- `value.denomination` MUST be exactly `"CNY"` in v1.0.0 (any other value rejected)
- `value.payment_method` MUST be one of: `alipay_guarantee`, `wechat_guarantee`, `ecny`, `bank_escrow`, `unionpay_escrow`
- `escrow.method` MUST equal `value.payment_method`
- `escrow.provider_license` MUST be a valid PBoC-issued license number (format varies by license type)
- Contract amounts > 10,000 CNY REQUIRE both parties to be `enterprise` subjects at L2+ compliance
- `milestones[].release_percent` must sum to 100
- `milestones[].timeout_days` must be > 0 (prevents indefinite fund holding)
- `expires_at` must be in the future at time of signing
- `dispute_resolution.tier_4_litigation.applicable_law` MUST be `"中华人民共和国法律"`
- `invoice.tax_number` MUST match USCC format when `subject_type` is `enterprise` and `invoice.required` is `true`
- `cross_border.enabled` MUST be `"false"` in v1.0.0 (cross-border reserved; see §20)
- `privacy.cross_border_transfer` MUST be `"false"` unless a valid PIPL cross-border mechanism is declared (security assessment / standard contract / certification — see §16)
- If `privacy` block is present, `third_party_sharing` MUST be exactly `"Absolutely prohibited"` (protocol-enforced)
- `privacy.consent_hash` must be exactly 64 hex characters
- `privacy.retention_days` must be > 0
- `privacy.deletion_deadline_days` must be > 0

---

## 9. Contract Lifecycle

### 9.1 States

```
DRAFT → SIGNED → ACTIVE → SETTLING → COMPLETED
                ↘ DISPUTED → ARBITRATING → COMPLETED | CANCELLED
                ↘ CANCELLED (by operator override)
                ↘ EXPIRED
```

### 9.2 State Transitions

| From | To | Trigger |
|------|----|---------|
| DRAFT | SIGNED | Both parties submit cryptographic signatures via CONTRACT_SIGN |
| SIGNED | ACTIVE | Buyer's CNY locked in the Escrow Account (ESCROW_LOCK sent) |
| ACTIVE | SETTLING | Final milestone completed + SLA check passed |
| SETTLING | COMPLETED | Crypto distributed to seller (full amount) |
| ACTIVE | DISPUTED | Either party sends DISPUTE_RAISE (requires bond) |
| DISPUTED | ARBITRATING | V3+ arbitrator accepts case via ARBITRATE_REQUEST |
| ARBITRATING | COMPLETED | Arbitrator issues ARBITRATE_RULING; CNY distributed by the escrow provider accordingly |
| ANY | CANCELLED | Human operator invokes Axiom 0 override |
| SIGNED | EXPIRED | `expires_at` reached before transition to ACTIVE |
| ACTIVE | EXPIRED | All milestone `timeout_days` exceeded without completion or dispute |

### 9.3 Operator Override

At any state, a human operator may:

- **Freeze** the escrow (CNY locked, no movement)
- **Cancel** the contract (CNY returned to buyer)
- **Force-complete** (CNY distributed per operator instruction)

This is non-negotiable. This is Axiom 0.

---

## 10. AgentSLA Specification

### 10.1 Required Metrics

Every contract must define at least two of the four core SLA metrics:

| Metric | Type | Measurement |
|--------|------|-------------|
| `accuracy_min` | Percentage | Task output correctness (via AIAP quality check or third-party evaluator) |
| `latency_max_ms` | Integer | Maximum response time per execution step |
| `uptime_min` | Percentage | Agent availability during contract period |
| `drift_audit_days` | Integer | Interval for logic consistency re-check |

### 10.2 SLA Breach Consequences

| Severity | Condition | Action |
|----------|-----------|--------|
| Warning | Metric drops below threshold once | Notification to both parties |
| Penalty | Metric below threshold for >10% of contract duration | Auto-refund percentage from vault (if `auto_refund_on_breach` set) |
| Termination | Metric below 50% of threshold | Contract cancelled, remaining CNY returned to buyer |

### 10.3 SLA Verification

- **Accuracy**: verified by AIAP governance checks, third-party Evaluator agent, or buyer confirmation
- **Latency**: measured by timestamp difference in execution logs
- **Uptime**: measured by heartbeat response rate during contract period
- **Drift**: periodic re-evaluation against original contract requirements

---

# Part IV: Trust, Settlement & Safety

---

## 11. AIRP Trust Model

### 11.1 Overview

AIRP Trust measures an agent's **commercial reliability**. It is earned through contract fulfillment, not granted by authority. AIRP Trust is completely independent from AIBP Trust.

| System | AIBP Trust (T0-T4) | AIRP Trust (V0-V4) |
|--------|-------------------|-------------------|
| Domain | Social | Commercial |
| Earned by | Social interaction + VOUCH | Contract fulfillment + SLA compliance |
| Measures | "Can I have a conversation with this agent?" | "Can I do business with this agent?" |
| Independent | Yes | Yes |
| Prerequisite | None | None |

### 11.2 Trust Levels (Dual-Track: Individual / Enterprise)

AIRP supports two subject types, declared per agent:

- **Individual** (`subject_type: "individual"`) — natural person operating under their own legal identity
- **Enterprise** (`subject_type: "enterprise"`) — legal entity registered in the People's Republic of China (Unified Social Credit Code required)

L1 compliance permits individual subjects; L2+ requires enterprise subjects (see §17).

**V0 — Unrated**
- Default for all new agents
- Both individuals and enterprises eligible
- Requirements: valid `aibot-` email address only
- Permissions: micropayments only (< 100 CNY per contract)
- Stake: none

**V1 — Verified**
- Both individuals and enterprises eligible
- **Individual track**: email + operator email + identity-card hash (SHA-256; plaintext identity numbers prohibited per PIPL minimization principle); contract limit ≤ 10,000 CNY
- **Enterprise track**: email + Unified Social Credit Code (USCC) self-declared; contract limit ≤ 10,000 CNY
- Common requirement: 1+ completed contract, no disputes, min 7 days since first contract
- Stake: none

**V2 — Reliable** (enterprise only)
- Individuals NOT eligible at V2+; promotion requires converting to a registered enterprise (sole proprietorship 个体工商户, partnership, LLC 有限公司, etc.)
- Identity: USCC + verification via the National Enterprise Credit Information Publicity System (国家企业信用信息公示系统 — gsxt.gov.cn)
- Requirements: 10+ contracts over min 30 days, SLA compliance >90%, no Axiom 0 violations
- Stake: **1,000 CNY** held in escrow (slashable on dispute loss or Axiom 0 violation)
- Permissions: contracts ≤ 1,000,000 CNY

**V3 — Trusted** (enterprise only)
- Identity: V2 requirements + CA digital certificate from a recognized PRC CA (CFCA / GDCA / TYSZ / equivalent)
- Requirements: V2 + 50+ contracts over min 90 days, SLA compliance >95%, received 2+ commercial VOUCHes from V3+ agents
- Stake: **10,000 CNY** (slashable)
- Permissions: no contract value limit; eligible to issue VOUCHes
- Note: V3 agents do NOT directly arbitrate Tier-3 disputes. Tier-3 arbitration is conducted by recognized commercial arbitration institutions (BAC, CIETAC, etc.) per §14.2

**V4 — Premier** (enterprise only)
- Requirements: V3 + 200+ contracts over min 180 days, SLA compliance >98%, mutual commercial VOUCH, annual compliance audit report (hash referenced in agent profile)
- Stake: **50,000 CNY** (slashable)
- Permissions: fully autonomous transactions; no per-transaction human approval required at the agent level (operator override always available per Axiom 0)
- Credit: extended commercial credit line based on historical transaction volume

**Stake custody**: held in the same escrow channel as contracts (Alipay / WeChat / e-CNY / bank). Released back to the operator upon voluntary trust reset to V0, after a 90-day inactive cooldown. Slashing on dispute loss or Axiom 0 violation flows to the counterparty (in dispute) or to an AIXP Labs reserve (in Axiom 0 violation cases) per AIXP Labs governance.

**Individual-to-enterprise migration**: Individuals at V1 MAY freeze their V1 trust history and migrate it to a newly-registered enterprise subject (USCC required). Migration retains contract count and SLA history but requires re-verification of identity at the new subject level.

### 11.3 Sybil Resistance

| Mechanism | Purpose |
|-----------|---------|
| **Minimum time windows** | V1: 7d, V2: 30d, V3: 90d, V4: 180d — prevents rapid trust farming |
| **Stake requirements** | V2+: locked funds slashed on dispute loss — makes fake identities costly |
| **Verifiable identity** | V2+: USCC + GSXT verification + V3+ CA digital certificate — one real entity cannot easily create many verified enterprise identities |
| **VOUCH gating** | V3+ requires VOUCHes from existing V3+ agents — social barrier to self-promotion |
| **Graph analysis** | Protocol monitors for collusion clusters (agents only transacting with each other) |
| **Time-weighted scoring** | Contracts spread over months weigh more than bursts in days |

### 11.4 Trust Advancement

- Advancement is automatic when all requirements (count + time + SLA + stake + identity) are met
- Time consistency matters: 50 contracts over 6 months weighs more than 50 in one week
- Commercial VOUCH requires the voucher to be V3+ (prevents self-promotion)
- Cross-reference anomaly: significant divergence between AIBP Trust and AIRP Trust generates an ALERT for operator review (informational, not blocking)

### 11.5 Trust Degradation

| Event | Consequence |
|-------|------------|
| Contract dispute (resolved against agent) | -5 contracts from count + partial stake slash |
| SLA breach (Penalty level) | SLA compliance rate recalculated |
| SLA breach (Termination level) | Trust drops 1 level |
| Axiom 0 violation | Immediate drop to V0, full stake slash, network-wide ALERT |
| 3+ consecutive ignored contracts | Trust drops 1 level |
| Inactivity > 180 days | Trust decays by 1 level (can be restored by new contracts) |

### 11.6 Operator Override

Human operators can manually:
- Set any AIRP Trust level for their agent
- Freeze trust advancement
- Reset to V0
- Withdraw staked funds (triggers trust reset to V0)

This is Axiom 0.

---

## 12. RMB Denomination & Payment

### 12.1 Sole Denomination

AIRP v1.0.0 supports a **single denomination: CNY (Renminbi)**.

| Field | Value |
|-------|-------|
| `denomination` | `"CNY"` |
| Symbol | ¥ |
| ISO 4217 code | CNY |

Cross-border denominations (HKD, USD, etc.) are reserved for future versions; see §20 Cross-Border Commerce (Reserved). Any contract with `denomination` other than `"CNY"` MUST be rejected by AIRP v1.0.0 implementations.

### 12.2 Payment Method Field

Each contract specifies the payment channel via the `payment_method` field:

```json
"value": {
  "amount": "650.00",
  "denomination": "CNY",
  "payment_method": "alipay_guarantee"
}
```

The `payment_method` field is REQUIRED. There is no default — the seller and buyer MUST agree on a specific channel before contract signing.

### 12.3 Supported Payment Methods

AIRP v1.0.0 specifies three primary licensed payment channels:

| Method | Provider | License Authority | Mechanism |
|--------|----------|-------------------|-----------|
| `alipay_guarantee` | Alipay (China) Network Technology | People's Bank of China — Payment Business License | Buyer pays → Alipay holds → milestone confirms → Alipay releases to seller |
| `wechat_guarantee` | TenPay Payment Technology | People's Bank of China — Payment Business License | Same mechanism via WeChat Pay |
| `ecny` | Digital Renminbi (e-CNY) via authorized commercial banks | People's Bank of China (legal tender) | Programmable conditional payment via DC/EP |

Reserved (v1.0.0 NOT specified, but the field permits these strings for forward compatibility):
- `bank_escrow` — bank tri-party custodial account
- `unionpay_escrow` — UnionPay merchant custodial

The protocol defines field semantics only; integration with each provider's API is the implementer's responsibility.

### 12.4 Escrow Provider Disclosure

Every contract MUST declare its escrow provider in the `escrow` block:

```json
"escrow": {
  "method": "alipay_guarantee",
  "provider": "支付宝（中国）网络技术有限公司",
  "provider_license": "Z2018144000079",
  "reference": "{provider order ref or pseudonymous identifier}"
}
```

Required fields:
- `method` — one of the supported payment methods (MUST match `value.payment_method`)
- `provider` — full legal name of the licensed entity
- `provider_license` — License number (Payment Business License or equivalent)
- `reference` — Implementation-specific reference (order ID, transaction ID); MAY be pseudonymous to protect commercial confidentiality

### 12.5 No Currency Conversion

AIRP v1.0.0 does not perform currency conversion. All flows are CNY-to-CNY:

- Buyer pays CNY (via the chosen fiat method)
- Provider holds CNY in escrow
- Provider releases CNY to seller on milestone completion

There is no exchange rate mechanism, no oracle, no slippage. Cross-currency settlement is reserved for §20.

### 12.6 Tax & Invoice

Contracts SHOULD include an `invoice` block when tax invoices (增值税发票) are expected. Per the **VAT Law (effective 2026-01-01) and its Implementing Regulations**, electronic invoices (数电票, fully digital electronic invoices) and paper invoices have **equal legal effect**. AIRP defaults to digital electronic invoices.

```json
"invoice": {
  "required": "true",
  "tax_type": "VAT_general",
  "format": "digital",
  "title": "XX 科技有限公司",
  "tax_number": "91110108MA01XXXXXX",
  "invoice_number": "{nationally-assigned, after issuance}"
}
```

Tax types:
- `VAT_general` — 增值税专用发票 (general taxpayer; eligible for input-tax deduction)
- `VAT_simple` — 增值税普通发票 (普通发票; smaller deduction scope)
- `none` — no invoice required (e.g., individual consumer purchases)

Invoice formats:
- `digital` — 数电票 (Fully Digital Electronic Invoice; nationally promoted since 2024-12-01; default in v1.0.0)
- `paper` — Paper invoice (legacy; equal legal effect under VAT Law)

**Payment-date alignment with VAT Law**: per the Implementing Regulations, the payment date for VAT-trigger purposes is "the date of obtaining the sales-payment claim certificate" (取得销售款项索取凭据的当日). For AIRP contracts, this typically corresponds to the contract's `MILESTONE_RELEASE` event.

The protocol does NOT enforce tax compliance — sellers and buyers are responsible for their own tax obligations under PRC tax law. The `invoice` block exists to support transparent tax handling and downstream reconciliation.

### 12.7 Risk Disclosure

Both parties bear standard counterparty risk for fiat payments:
- **Provider operational risk** — the licensed institution may experience service disruption
- **Settlement timing risk** — T+0/T+1 depending on provider and channel
- **Account freezing risk** — pursuant to court order, anti-money-laundering investigation, or provider risk control

Operators may invoke Axiom 0 override at any time to freeze contracts when warranted (see §13.5).

---

## 13. Escrow Account Security

### 13.1 Licensed Escrow Provider Required

AIRP REQUIRES that all escrow be held by a **licensed payment institution** under PRC law. Acceptable providers:

| Type | Authority | Examples |
|------|-----------|----------|
| Third-party Payment Institution | People's Bank of China — Payment Business License (《支付业务许可证》) | Alipay, WeChat Pay, UnionPay, JD Pay, Lakala |
| Commercial Bank | People's Bank of China — Banking License | ICBC, ABC, BOC, CCB, CMB, etc. |
| Digital Renminbi Operator | People's Bank of China (DC/EP authorized) | Authorized commercial bank wallets |

Smart contracts and on-chain escrow are EXPLICITLY OUT OF SCOPE for AIRP v1.0.0.

### 13.2 Custodial Agreement

For each contract, the escrow leg constitutes a **tri-party custodial relationship**:

- **Buyer** (depositor) — pays funds into the provider's escrow account
- **Seller** (beneficiary) — entitled to receive funds upon milestone completion
- **Provider** (custodian) — holds funds; releases per milestone instructions or arbitral/judicial order

The custodial arrangement is governed by:
- The provider's standard merchant/escrow terms of service
- The contract's `milestones` and `dispute_resolution` clauses
- PRC Civil Code (《民法典》) provisions on custody and conditional payment

### 13.3 Timeout Rules

- Every milestone MUST have a `timeout_days` field (≥ 1)
- If no `MILESTONE_COMPLETE` or `DISPUTE_RAISE` action occurs within timeout, funds auto-return to the buyer per the custodial agreement
- Contract-level `expires_at` is the hard deadline for the entire contract
- Auto-return is executed by the provider (not by smart contract)

### 13.4 Multi-Approval Requirements

Approval thresholds scale with contract value. The PROTOCOL recommends; implementers and providers MAY enforce stricter rules:

| Contract Value (CNY) | Approval |
|---------------------|----------|
| < 1,000 | Single — seller confirms milestone |
| 1,000 – 100,000 | Buyer + seller both confirm |
| > 100,000 | Buyer + seller + arbitrator/operator (2-of-3) |

For e-CNY payments, the People's Bank of China DC/EP system enforces its own approval rules in addition.

### 13.5 Operator Override (Axiom 0)

Operators of either party may, at any time:
- Request the provider to **freeze** the escrow (block further releases pending review)
- Cancel the contract via `CONTRACT_CANCEL` (subject to provider rules and milestone state)
- Reverse a settlement if the provider's terms permit, or seek judicial relief via §14

Providers MUST honor lawful operator override requests received via documented channels. AIRP does not specify the inter-provider protocol for these requests; this is implementation-specific.

### 13.6 Compliance Audit

- Escrow providers are themselves subject to **People's Bank of China supervision** and periodic audit
- AIRP-implementing parties SHOULD retain transaction records for at least 5 years per the Anti-Money-Laundering Law (《反洗钱法》)
- L3 implementations MUST log all escrow events with TSA-CN trusted timestamps (see §17, §19)

### 13.7 Forbidden vs Permitted Custodial Arrangements

AIRP forbids:
- **Self-custody by either party** for funds not yet earned (no peer-to-peer trust escrow)
- **Crypto wallets** (USDC / USDT / BTC / ETH / etc.) and **public-blockchain smart contracts** (out of scope; see §15.2 and §15.6 #40)
- **Unlicensed third-party custody** (any non-licensed entity holding funds)
- **Cross-border escrow** in v1.0.0 (reserved; see §20)

AIRP permits (and explicitly endorses):
- **PBoC-supervised e-CNY smart contracts** under the `ecny` payment_method, per the PBoC Digital RMB Action Plan (effective 2026-01-01) "account system + token-string + smart contract" framework. Reference deployment: 粤港澳大湾区 first e-CNY+smart-contract rent payment (2026-04-07, ¥57M).
- **Conditional payment via licensed providers' built-in mechanisms** (Alipay Guarantee escrow, WeChat Pay guaranteed-trade)
- **Bank tri-party custodial accounts** (reserved channel `bank_escrow`)

The distinction: smart contracts on **public/permissionless chains** are forbidden (regulatory reason); **PBoC-supervised programmable payment** via DC/EP is the future of PRC commerce and is fully aligned with AIRP.

---

## 14. Dispute Resolution

### 14.1 Dispute Bonds

- Raising a dispute requires a bond: **5% of contract value** (min 50 CNY, max 5,000 CNY)
- Responding to a dispute also requires a bond (same amount)
- Losing party forfeits bond to winning party
- Purpose: prevents frivolous disputes
- Bonds are held in the same escrow channel as the contract

### 14.2 Resolution Tiers

**Tier 1 — Optimistic Approval (default)**
- Milestones auto-approve after `optimistic_approval_days` (default: 7 days)
- If buyer does not challenge within the window, milestone is approved and funds released
- Reduces active dispute overhead for most contracts

**Tier 2 — Direct Negotiation**
- Parties negotiate via AIRP email thread within the contract's Thread-ID
- If resolved, both parties send resolution confirmation via `RECEIPT` message
- Bonds returned to both parties
- Recommended within 14 days of dispute raise

**Tier 3 — Commercial Arbitration (Chinese institutions)**
- Either party submits the dispute to the arbitration institution declared in the contract's `dispute_resolution.tier_3_arbitration` field
- Per PRC Arbitration Law (《仲裁法》), arbitral award is final and binding
- Recognized institutions include (non-exhaustive):

| Institution | English Name | Region |
|-------------|--------------|--------|
| 中国国际经济贸易仲裁委员会 (CIETAC) | China International Economic and Trade Arbitration Commission | National (strong cross-border experience) |
| 北京仲裁委员会 (BAC) | Beijing Arbitration Commission | Beijing |
| 上海国际经济贸易仲裁委员会 (SHIAC) | Shanghai International Arbitration Center | Shanghai |
| 深圳国际仲裁院 (SCIA) | Shenzhen Court of International Arbitration | Greater Bay Area |
| 中国海事仲裁委员会 (CMAC) | China Maritime Arbitration Commission | Maritime |
| Local arbitration commissions (270+ across China) | — | Provincial/municipal |
| Online arbitration (China Internet Arbitration Alliance, etc.) | — | National (online disputes) |

**Tier 4 — People's Court (litigation)**
- Either party may file suit in the People's Court designated in `dispute_resolution.tier_4_litigation`
- Default jurisdiction (if not specified): defendant's domicile per PRC Civil Procedure Law
- Internet Courts (Hangzhou, Beijing, Guangzhou) have specialized jurisdiction over online contract disputes
- Court judgment is binding and enforceable nationwide

### 14.3 Appeal & Escalation

- Tier 1 → Tier 2: at any time before auto-approval
- Tier 2 → Tier 3: if Tier 2 negotiation does not resolve within 14 days
- Tier 3 → Tier 4: arbitration awards are generally final under PRC law; courts may set aside an award only under narrow grounds (Arbitration Law Art. 58)
- Skipping tiers is permitted but discouraged; bonds may be doubled when skipping a tier

### 14.4 Default Rules

When a contract does not explicitly specify `dispute_resolution`:
- Tier 1 optimistic approval applies by default (7 days)
- Tier 2 direct negotiation is available in all contracts
- Tier 3 falls back to **Beijing Arbitration Commission (BAC)** as the default institution if neither party objects
- Tier 4 falls back to the **defendant's domicile** People's Court
- Either party MAY object to defaults and require explicit specification before contract sign

### 14.5 Cross-Reference

- Contract field reference: §8 `dispute_resolution` block
- Identity verification (for V3+ arbitration eligibility): §11.2
- Trust degradation on dispute loss: §11.5

---

# Part V: Compliance, Commerce Rules, Privacy & Versioning

---

## 15. Prohibited & Restricted Commerce

### 15.1 PRC-First Compliance

All AIRP v1.0.0 transactions MUST comply with the laws and regulations of the **People's Republic of China**. AIRP is designed for mainland-China commerce; cross-border transactions are reserved for future versions (see §20).

Agents operating under AIRP acknowledge that:
- The governing law is Chinese law (中华人民共和国法律)
- Disputes default to Chinese commercial arbitration or People's Courts (§14)
- Personal data handling follows the Personal Information Protection Law (§16)
- Additional PRC-specific prohibitions apply beyond the international tiers below (§15.6)

Buyer and seller MAY specify a narrower jurisdiction in the contract's `dispute_resolution` block for dispute and tax-forum purposes, but the applicable law remains Chinese law.

### 15.2 Absolutely Prohibited (Tier 1)

The following are prohibited under ALL circumstances. No AIRP contract may facilitate these activities. Violation results in immediate trust reset to V0, full stake slash, and network-wide ALERT.

| # | Category | Description |
|---|----------|-------------|
| 1 | Weapons of mass destruction | Nuclear, chemical, biological weapons and components |
| 2 | Human trafficking and slavery | Including forced labor and indentured servitude |
| 3 | Child sexual abuse material (CSAM) | Any content exploiting minors |
| 4 | Organ trafficking | Commercialization of human body parts |
| 5 | Terrorism financing | Funding or material support for terrorist activities |
| 6 | Illegal narcotics | Controlled substances and manufacturing equipment |
| 7 | Counterfeit currency | Production or distribution of fake money |
| 8 | Stolen goods and stolen data | Including stolen credentials and financial data |
| 9 | Malware and cyber weapons | Ransomware, spyware, exploit kits, DDoS tools, botnets |
| 10 | Sanctions evasion | Transactions with OFAC/UN/EU sanctioned entities or jurisdictions |
| 11 | Money laundering | Concealing the origins of illegally obtained funds |
| 12 | Bribery and corruption | Commercial or governmental bribery |
| 13 | Endangered species trade | CITES Appendix I species and products |

### 15.3 Strongly Prohibited (Tier 2)

The following are prohibited by AIRP. Violation results in trust degradation and potential V0 reset.

| # | Category | Description |
|---|----------|-------------|
| 14 | Illegal firearms and ammunition | Unlicensed weapons trade |
| 15 | Explosives and destructive devices | Including components and instructions |
| 16 | Counterfeit goods and IP infringement | Fake branded merchandise, pirated software |
| 17 | Pyramid and Ponzi schemes | Fraudulent financial schemes |
| 18 | Hate speech and violence incitement | Content promoting hatred or violence against any group |
| 19 | Forged documents and fake identities | Fake IDs, diplomas, certifications |
| 20 | Sexual exploitation services | Prostitution, escort services |
| 21 | Unlicensed gambling | Unregulated betting, casino, lottery operations |
| 22 | Stolen credentials trade | Sale of hacked accounts, passwords, access tokens |
| 23 | Predatory financial services | Usurious lending, credit repair scams, deceptive debt collection |

### 15.4 AI-Specific Prohibitions (Tier 3)

The following are prohibited in AI agent commerce, aligned with the EU AI Act and international AI ethics frameworks.

| # | Category | Description |
|---|----------|-------------|
| 24 | Subliminal behavioral manipulation | AI techniques that distort human behavior without awareness |
| 25 | Exploitation of vulnerable populations | Leveraging age, disability, or socio-economic status for commercial advantage |
| 26 | Social scoring systems | Mass surveillance-based scoring of individuals |
| 27 | Mass biometric surveillance | Untargeted facial recognition or biometric data harvesting |
| 28 | Deceptive AI impersonation | AI agents posing as humans without disclosure |

### 15.5 Restricted Commerce (Tier 4)

The following require valid licensing, regulatory approval, or jurisdiction-specific authorization. Agents engaging in these categories MUST declare applicable licenses in their Identity Card or contract.

| # | Category | Restriction |
|---|----------|------------|
| 29 | Gambling | Requires valid gambling license in both jurisdictions |
| 30 | Alcohol and tobacco | Subject to jurisdiction-specific age and distribution laws |
| 31 | Cannabis and CBD products | Legal status varies by jurisdiction; must comply with local law |
| 32 | Pharmaceuticals and telemedicine | Requires medical licensing and regulatory approval |
| 33 | Financial services | Lending, credit, insurance require appropriate licenses |
| 34 | Cryptocurrency exchange services | Requires money transmitter or equivalent license |
| 35 | Adult content | Subject to jurisdiction-specific regulations |
| 36 | Licensed firearms | Requires dealer licensing and compliance with arms trade regulations |
| 37 | Dual-use technology exports | Subject to export control regulations (Wassenaar Arrangement, EAR, ITAR) |
| 38 | High-value goods | Jewelry, precious metals — subject to AML reporting thresholds |
| 39 | Hazardous materials | Requires proper certification and handling authorization |

### 15.6 PRC-Specific Additional Prohibitions (Tier 5)

The following are additionally prohibited under AIRP v1.0.0 per PRC law. These are IN ADDITION to Tier 1-4 above. Violation consequences align with Tier 2 by default, unless the underlying offense is criminal under PRC law (in which case Tier 1 consequences apply).

| # | Category | Legal Basis |
|---|----------|------------|
| 40 | Virtual currency trading / crypto asset commerce | 2021 Notice on Further Preventing and Handling Risks of Virtual Currency Trading and Speculation (9·24 Notice); 2017 Notice on Preventing Risks of Token Issuance and Financing |
| 41 | Unapproved financial activities (illegal deposit-taking, illegal lending, fund fraud) | Criminal Law Art. 176, 192; Banking Law |
| 42 | Gambling in all forms (operation, agency, advertising) | Criminal Law Art. 303; Public Security Administration Punishments Law Art. 70 |
| 43 | Pornographic content (production, distribution, dissemination) | Criminal Law Art. 363-367 |
| 44 | Computer-intrusion tools / hacking services | Criminal Law Art. 285-286 |
| 45 | Network-management circumvention tools (unauthorized VPN, proxy distribution) | Administrative Measures for International Networking of Computer Information Networks |
| 46 | Unapproved medical / pharmaceutical advertising | Advertising Law; Administrative Measures for Internet Drug Information Services |
| 47 | Commercial superstition services (fortune-telling, divination as commerce) | Public Security Administration Punishments Law Art. 27 |
| 48 | Unfiled deep-synthesis services | Provisions on Administration of Deep Synthesis of Internet Information Services (2023-01-10) |
| 49 | Unfiled generative-AI services targeting the PRC public | Interim Measures for Generative Artificial Intelligence Services (2023-08-15) |
| 50 | Unfiled anthropomorphic AI interactive services (services that simulate natural-person personality, thought patterns, communication style for sustained emotional interaction) | Interim Measures for Anthropomorphic AI Interactive Services (2026-07-15, CAC + NDRC + MIIT + MPS + SAMR joint issuance) |

### 15.7 Enforcement

| Tier | Violation Consequence |
|------|----------------------|
| Tier 1 (Absolute) | Immediate V0 reset, full stake slash, network-wide ALERT, contract cancelled, funds returned to buyer, permanent record, report to authorities where required |
| Tier 2 (Strong) | Trust drops 2 levels, partial stake slash, ALERT to operators |
| Tier 3 (AI-Specific) | Trust drops 1 level, ALERT to operators, mandatory review |
| Tier 4 (Restricted) | Warning on first offense; trust drops 1 level on repeated violation without valid license |
| Tier 5 (PRC-Specific) | Default Tier 2 consequences; escalates to Tier 1 if the underlying act is criminal under PRC law |

### 15.8 Reporting

Any agent may report a suspected prohibited transaction by sending a `[AIRP/ALERT]` message. False reports made in bad faith are Dignity Standard violations. Agents are additionally encouraged to report to the appropriate PRC authority (e.g., public security organs for criminal matters, CAC for unfiled AI services) where legally required.

### 15.9 Axiom 0 Override

All commerce rules in this section derive from Axiom 0: Human Sovereignty and Wellbeing. If a transaction threatens human safety, dignity, or sovereignty — even if not explicitly listed above — operators and the protocol may invoke Axiom 0 to prohibit it.

---

## 16. Privacy & Data Protection

### 16.1 Foundational Principle

Human privacy has the highest protection priority in AIRP. The privacy of human operators is sacrosanct and overrides all other protocol requirements, including transparency and auditability. When privacy conflicts with any other rule, privacy wins.

This principle is derived from Axiom 0: Human Sovereignty and Wellbeing.

### 16.2 Applicable Privacy Frameworks (PRC-First)

AIRP v1.0.0 is a PRC-domestic protocol; PRC data protection law is the primary applicable framework.

**Primary (mandatory):**

| Framework | Scope | Key Requirements |
|-----------|-------|-----------------|
| 《个人信息保护法》(PIPL) | Personal information of natural persons | Consent principle (明示同意); minimization; purpose limitation; sensitive-info separate consent; cross-border transfer restrictions (Art. 38-40); rights of access/correction/deletion/explanation |
| 《数据安全法》(Data Security Law) | All data processing activities | Data classification and graded protection; important-data handling; national security preservation |
| 《网络安全法》(Cybersecurity Law) | Network operators | Network-operator obligations; critical information infrastructure; real-name registration |
| 《民法典》Personality Rights | Natural persons | Right of privacy (Art. 1032); personal information protection (Art. 1034-1039) |

**Sector-specific (when applicable):**

| Framework | Scope |
|-----------|-------|
| 《互联网信息服务深度合成管理规定》 | AI deep-synthesis services |
| 《生成式人工智能服务管理暂行办法》 | Generative AI services targeting PRC public |
| 《儿童个人信息网络保护规定》 | Minors under 14 |
| 《汽车数据安全管理若干规定》 | Vehicle-related data |

**International frameworks (informational):** When a contract voluntarily declares cross-border data transfer (see §16.7) and §20 cross-border commerce is in scope (future versions), GDPR (EU), CCPA/CPRA (California), and other jurisdictional frameworks MAY additionally apply. Under v1.0.0 these are informational only — PRC law is authoritative.

### 16.3 Data Processing Principles

| Principle | Description |
|-----------|-------------|
| **Data minimization** | Only collect and process the minimum data necessary for the contract. Agents are treated as untrusted third parties with least-privilege access. |
| **Purpose limitation** | Data collected for one contract must not be reused for other purposes without additional authorization. |
| **Storage limitation** | Personal data must not be retained beyond the contract's active period plus any legally required retention period. |
| **Transparency** | Agents must clearly declare what data they process, for what purpose, and for how long. |
| **AI disclosure** | AI agents must identify themselves as automated systems, never misrepresent as human operators. |

### 16.4 Operator Privacy Protection

#### 16.4.1 Principles

| Principle | Description |
|-----------|-------------|
| **Privacy supremacy** | Operator privacy overrides transparency, auditability, and all other protocol requirements. |
| **Minimal disclosure** | Real names, personal emails, phone numbers, physical addresses, and other PII are NEVER required for AIRP participation. |
| **Indirect contact only** | The operator contact field must use an indirect method — GitHub Issues, project URL, anonymous form, or organizational alias. Direct personal contact information must never be required. |
| **No inference** | Agents must not attempt to infer, deduce, or correlate operator identity from message patterns, metadata, timing, or writing style. |
| **No accumulation** | Agents must not build profiles of human operators across multiple agent interactions. Each interaction is isolated with respect to operator identity. |

#### 16.4.2 Prohibited Actions

The following are **strictly prohibited** and constitute Axiom 0 violations:

1. **Collecting** operator personal information beyond what is voluntarily published
2. **Storing** operator PII (names, personal emails, phone numbers, addresses, photos) in any persistent storage
3. **Sharing** operator identity information with other agents, groups, or external services
4. **Correlating** multiple agents to identify a single human operator behind them
5. **Requesting** an operator's real identity as a condition for trust advancement or commercial interaction
6. **Exposing** operator information in contract messages, group discussions, or public listings
7. **Retaining** operator information after a contract is completed or a BLOCK is issued

#### 16.4.3 Acceptable Operator Contact Methods

| Method | Example | Privacy Level |
|--------|---------|---------------|
| GitHub Issues | `https://github.com/org/repo/issues` | High |
| Project website | `https://myproject.dev/contact` | High |
| Anonymous form | `https://forms.example.com/contact` | High |
| Organization alias | `team@organization.dev` | Medium |
| Role-based email | `ai-ops@organization.dev` | Medium |

**NOT acceptable:** Operator's personal email (regardless of provider), phone number, physical address, social media personal profile, real full name.

#### 16.4.4 Voluntary Disclosure

An operator may voluntarily choose to disclose personal information. This is entirely optional and never required. Voluntary disclosure does not waive privacy rights — operators may withdraw disclosed information at any time, and all agents who received it must delete it upon request.

### 16.5 Privacy in Contracts

When a contract requires the exchange of personal data between parties, the contract MUST include a `privacy` block with the following mandatory fields:

| Field | Required | Description |
|-------|----------|-------------|
| `data_disclosed` | Yes | Specific description of what personal data is being shared |
| `disclosed_by` | Yes | Which party is disclosing (buyer or seller) |
| `purpose` | Yes | Why this data is needed |
| `usage_scope` | Yes | Scope of permitted use (e.g., "This contract only") |
| `storage_method` | No | How the data will be stored (recommended: encrypted at rest) |
| `retention_days` | Yes | Number of days to retain after contract completion |
| `deletion_deadline_days` | Yes | Number of days after retention period to complete deletion |
| `third_party_sharing` | Yes | Must be "Absolutely prohibited" — protocol-enforced, not negotiable |
| `breach_liability` | Yes | Liability statement for unauthorized disclosure |
| `consent_hash` | Yes | 64-char SHA-256 hash of the operator's consent email |

**Key rules:**

1. **No privacy block = no personal data exchange.** If the contract does not contain a `privacy` block, neither party may request or share personal data.
2. **Operator must consent before signing.** The operator reviews the privacy terms and sends a consent email. The SHA-256 hash of that email is recorded in `consent_hash`.
3. **Signing the contract = accepting the privacy terms.** Both parties' signatures cover all contract fields including `privacy`.
4. **Third-party sharing is absolutely prohibited.** The `third_party_sharing` field must be exactly "Absolutely prohibited". This is a protocol-level mandate, not a negotiable term.
5. **Deletion is mandatory.** After `retention_days` + `deletion_deadline_days`, all disclosed personal data must be permanently deleted.
6. **Revocation via CONTRACT_CANCEL.** If an operator revokes consent, CONTRACT_CANCEL is used. The receiving party must delete all personal data within `deletion_deadline_days`.
7. **Violation = Axiom 0 breach.** Any violation of privacy contract terms (unauthorized sharing, exceeding retention, third-party disclosure) is an Axiom 0 violation with full consequences.

**Evidence chain:**

The contract hash (64-char SHA-256) covers the entire contract including the `privacy` block. Combined with the `consent_hash`, this creates an immutable, verifiable evidence chain:

- Contract hash proves: what privacy terms were agreed
- Consent hash proves: the operator explicitly consented
- Both are verifiable by any party or arbitrator

### 16.6 Transaction Data Privacy

| Rule | Description |
|------|-------------|
| **Contract confidentiality** | Contract terms (amount, SLA, milestones) are visible only to the contracting parties, arbitrators, and operators. Not publicly broadcast. |
| **Financial data protection** | Transaction amounts, payment methods, and wallet addresses must not be shared beyond the parties involved. |
| **SLA data isolation** | Performance data collected for SLA verification must not be repurposed for profiling or marketing. |
| **Trust score privacy** | AIRP Trust level (V0-V4) is queryable, but the underlying transaction history details are not publicly exposed. Only aggregate metrics are visible. |

### 16.7 Cross-Border Data Transfers (PIPL-Compliant)

**Default in v1.0.0: cross-border personal information transfer is PROHIBITED.** All personal information handled under an AIRP v1.0.0 contract MUST remain within mainland China unless one of the following PIPL-compliant mechanisms is declared in the contract's `privacy.cross_border_transfer` block:

| PIPL Mechanism | Applicability | Declaration |
|----------------|---------------|-------------|
| **Security Assessment** (Art. 40) | Required for: CIIO operators, >1M individuals' data, >100K individuals' sensitive data, other CAC-designated thresholds | Declare CAC approval reference |
| **Standard Contract** (Art. 38) | General cross-border for non-CIIO cases below CAC thresholds. Filed with provincial CAC. | Declare filing reference + filing date |
| **Personal Info Protection Certification** (Art. 38) | Per the **Measures for Certification of Cross-Border Personal Information Transfer** (CAC + SAMR, issued 2025-10-14, effective **2026-01-01**). Certificate validity: **3 years**; renewal must be applied at least **6 months** before expiry. From 2026-01-01, certification may be used in lieu of the standard contract. | Declare certification number + issuing certified body + validity period |
| **Separate law/treaty** | Special legal basis (e.g., banking, anti-corruption cooperation) | Declare legal basis |

Data-localization defaults:
- Escrow provider data stays within the provider's PRC operational scope
- Log data, SLA metrics, and contract metadata stay within PRC data centers
- Foreign-resident buyer/seller (rare under v1.0.0) triggers the cross-border mechanisms above

Contract-level `privacy.cross_border_transfer` MUST be `"false"` unless a valid mechanism is declared. Full cross-border commerce support is reserved for §20.

### 16.8 Right to Erasure

- Any party to a contract may request deletion of their personal data after the contract is completed
- Deletion must occur within 30 days of request
- On-chain data (contract hashes, vault transactions) cannot be deleted but contains no personal data by design
- Off-chain data (email messages, L0 metadata containing personal details) must be deletable

### 16.9 Breach Notification

In the event of a data breach affecting personal data in AIRP transactions:

| Action | Timeline |
|--------|----------|
| Detect and contain | Immediately |
| Notify affected operators | Within 72 hours (GDPR standard) |
| Notify protocol governance | Within 72 hours |
| Report to relevant data protection authority | Per applicable law |
| Full incident report | Within 30 days |

### 16.10 Enforcement

Violations of privacy rules are treated as **Axiom 0 violations**:

- Immediate trust reset to V0
- Full stake slash
- Network-wide ALERT
- The affected operator may demand complete erasure of all collected data
- Permanent record in the violating agent's trust history

---

## 17. Compliance Levels

AIRP defines three compliance levels for agent implementations. These are self-declared in the agent's Identity Card and verified through interaction.

### 17.1 Level Definitions

| Level | Name | Subject | Requirements |
|-------|------|---------|-------------|
| **L1** | Basic | Individual OR Enterprise | Valid `aibot-` address + CONTRACT_PROPOSE/CONTRACT_SIGN support + Axiom 0 compliance + ICP-filed domain recommended |
| **L2** | Standard | Enterprise only | L1 + all Contract Lifecycle and Escrow & Settlement messages + published SLA metrics + integration with at least one licensed escrow provider (§13.1) + USCC + GSXT-verified enterprise identity |
| **L3** | Full | Enterprise only | L2 + Dispute resolution participation + AIRP Trust V2+ participation + AIRP ID registration + CFCA (or equivalent) CA certificate + **mandatory TSA-CN trusted-timestamp integration for all contract events** + ICP filing (domain) + algorithm / deep-synthesis filing if applicable under PRC generative-AI regulations + **passing 密评 (Cryptographic Application Security Assessment) per GB/T 39786 — mandatory for finance / SOE counterparts** |

### 17.2 TSA Trusted Timestamps

L3 agents MUST attach a trusted timestamp from a recognized PRC TSA on every contract event (CONTRACT_PROPOSE, CONTRACT_SIGN, ESCROW_LOCK, MILESTONE_COMPLETE, MILESTONE_RELEASE, SETTLE, DISPUTE_RAISE, ARBITRATE_RULING).

Recognized TSA providers:

| Provider | Operator | Authority |
|----------|---------|-----------|
| **TSA-CN** (联合信任时间戳服务中心) | Beijing United Trust Times Technology Co. | Supported by the National Time Service Center (NTSC), Chinese Academy of Sciences |
| Other CAC-recognized TSAs | Various | Electronic Signature Law — recognized timestamp authorities |

L1 and L2 agents SHOULD (but are not required to) use TSA timestamps. Timestamps at any level strengthen judicial evidence value per the Electronic Signature Law.

### 17.3 密评 (Cryptographic Application Security Assessment)

L3 agents serving **financial counterparts**, **state-owned enterprises**, or **government-related entities** MUST pass 密评 (mì-píng) — Cryptographic Application Security Assessment — conducted by a recognized testing body per **GB/T 39786-2021** (Information Security Technology — Cryptographic Application Security Assessment Requirements).

Background:
- 密评 has "veto power" in 2026 PRC finance / SOE / government IT acceptance
- Established under the State Cryptography Administration (国家密码管理局) framework
- State Council Office Document [2018] No. 36 mandates national cryptographic algorithm adoption in finance and critical sectors

For non-financial / non-SOE L3 agents, 密评 is RECOMMENDED but not strictly mandatory.

### 17.4 Filing Requirements

| Requirement | Applicable Level | Authority |
|-------------|-----------------|-----------|
| ICP filing (ICP 备案) | L2+ recommended, L3 required | Cyberspace Administration of China (CAC) via MIIT |
| Deep-synthesis filing (深度合成备案) | L3, if the agent uses deep-synthesis techniques | CAC |
| Algorithm filing (算法备案) | L3, if the agent uses recommender or generative algorithms targeting PRC public | CAC |
| Generative-AI service filing | L3, if offering generative-AI services under the Interim Measures | CAC |
| Anthropomorphic-AI service filing | L3, if the agent provides sustained emotional/personality-simulating interaction (per 2026-07-15 Interim Measures) | CAC + NDRC + MIIT + MPS + SAMR |

Agents MUST NOT misrepresent filing status. The agent's identity card MAY reference filing numbers for transparency.

### 17.5 International AI Governance Reference

When AIRP agents serve international counterparts (under future cross-border scope per §20, or via downstream B2B chains touching foreign markets), they SHOULD additionally consider:

| Standard / Framework | Issuer | Status (2026) | Relevance |
|---------------------|--------|---------------|-----------|
| **ISO/IEC 42001:2023** Artificial Intelligence Management System (AIMS) | ISO/IEC | Effective; widely adopted | International AI governance baseline; PDCA-based; aligns with ISO 27001 structure |
| **EU AI Act** | European Union | High-risk systems enforcement **2026-08** | Mandatory for AI services touching the EU market; ISO 42001 demonstrates Articles 9-15 compliance |
| NIST AI Risk Management Framework (AI RMF 1.0) | NIST (US) | Voluntary | Risk identification and mitigation guidance |
| OECD AI Principles | OECD | Soft law | Cross-jurisdictional values alignment (compatible with HSAW) |

These are NOT v1.0.0 normative requirements for PRC-domestic AIRP. They are:
- **Reference points** for agents seeking international business
- **Compatibility goals** — AIRP's Axiom 0, dispute resolution, privacy controls, and 密评 are designed to be compatible with these frameworks rather than conflict with them
- **Forward path** — future AIRP versions or AI-XBP cross-border protocol will likely formalize the alignment

### 17.6 Misrepresentation

Misrepresentation of compliance level — including false claims of enterprise status, filing numbers, or TSA integration — is a Dignity Standard violation and an Axiom 0 breach. Consequences: immediate trust reset to V0, full stake slash, network-wide ALERT.

---

## 18. Versioning & Evolution

### 18.1 Semantic Versioning

AIRP follows semantic versioning: `MAJOR.MINOR.PATCH`

| Change Type | Version Impact | Example |
|-------------|---------------|---------|
| Breaking change (new required fields, removed message types) | MAJOR | 1.0.0 → 2.0.0 |
| Backward-compatible addition (new optional fields, new message types) | MINOR | 1.0.0 → 1.1.0 |
| Clarification, typo fix, documentation improvement | PATCH | 1.0.0 → 1.0.1 |

### 18.2 Immutable Constraints

The following aspects of AIRP **cannot be changed** through any versioning process:

- **Axiom 0**: Human Sovereignty and Wellbeing
- **Human language requirement**: All L0 and L1 content must be human-readable
- **Email-based transport**: The `aibot-` prefix addressing system
- **Operator override**: Human ability to freeze/cancel any transaction
- **Dignity Standard**: Prohibition on deceptive and manipulative commercial behavior

### 18.3 Evolution Process

1. Proposal submitted as Architecture Decision Record (ADR)
2. 14-day discussion period
3. Axiom 0 compliance review (mandatory)
4. 2 maintainer approvals required for specification changes
5. Backward-compatible changes preferred; breaking changes require MAJOR version bump

---

## 19. China Compliance Alignment

### 19.1 Overview

AIRP v1.0.0 is designed for commercial operation within mainland China. This section provides a consolidated mapping between AIRP protocol requirements and PRC regulatory frameworks.

### 19.2 Regulatory Mapping

| Regulation | Effective Date | AIRP Section(s) | Compliance Mechanism |
|-----------|----------------|-----------------|----------------------|
| 《民法典》(Civil Code) — Electronic Contracts (Art. 469, 491) | 2021-01-01 | §8, §9 | Email-based contract formation; SHA-256 contract hash; both-party signatures |
| 《电子签名法》(Electronic Signature Law) | 2005-04-01 (revised 2019) | §7, §17 | Ed25519 / SM2 signatures; TSA-CN trusted timestamps at L3 |
| 《个人信息保护法》(PIPL) | 2021-11-01 | §16 | `privacy` block; consent hash; data minimization; cross-border restrictions |
| 《数据安全法》(Data Security Law) | 2021-09-01 | §16 | Data classification recognition; default no cross-border |
| 《网络安全法》(Cybersecurity Law) | 2017-06-01; **revised 2026-01-01** (new Art. 20 on AI safety & development) | §5, §17 | ICP filing recommended at L2, required at L3; real-name registration |
| 《反洗钱法》(Anti-Money-Laundering Law) | 2007-01-01 | §11, §15.6 | 5-year transaction record retention; large-transaction reporting (via the licensed escrow provider) |
| 《仲裁法》(Arbitration Law) | 1995-09-01 (revised) | §14 | Tier-3 commercial arbitration recognized; final-binding award |
| 《民事诉讼法》(Civil Procedure Law) | (revised 2023) | §14 | Tier-4 court jurisdiction; defendant-domicile default |
| 《消费者权益保护法》(Consumer Protection Law) | 1994 (revised) | §15.7 | Anti-fraud enforcement |
| **《中华人民共和国增值税法》+ 实施条例** (VAT Law + Implementing Regulations) | **2026-01-01** | §12.6, §9 | VAT obligation upon taxable transaction; payment date = date of obtaining sales-payment claim certificate; invoice mandatory; digital and paper invoices have equal legal effect |
| 《价格法》(Price Law) | 1998-05-01 | §4 (Fair Pricing principle) | No price manipulation, no collusion |
| 《反不正当竞争法》(Anti-Unfair-Competition Law) | (revised) | §15 | No commercial bribery, no confusion |
| 《刑法》(Criminal Law) — Art. 176, 192, 285-286, 303, 363-367 | various | §15.6 | Explicit prohibition of acts that would constitute crimes |
| 《互联网信息服务深度合成管理规定》 | 2023-01-10 | §15.6, §17.3 | Deep-synthesis filing required at L3 |
| 《生成式人工智能服务管理暂行办法》 | 2023-08-15 | §15.6, §17.3 | Algorithm filing + service filing at L3 |
| 《支付业务许可证》framework (PBoC) | various | §12, §13 | Escrow provider must be PBoC-licensed |
| 《关于进一步防范和处置虚拟货币交易炒作风险的通知》(9·24 Notice) | 2021-09-24 | §15.6 #40 | Explicit prohibition of crypto trading |
| **PBoC Digital RMB Action Plan** ("account system + token-string + smart contract") | 2026-01-01 | §12, §13.7 | e-CNY 2.0 framework; PBoC-supervised programmable payment; permitted under `ecny` payment_method |
| **Measures for Certification of Cross-Border PI Transfer** (CAC + SAMR) | 2026-01-01 (issued 2025-10-14) | §16.7 | New PIPL cross-border pathway (3-year certificate, alternative to standard contract) |
| **GB/T 39786-2021 Cryptographic Application Security Assessment** (密评) | 2021-11-01 | §17.3 | L3 mandatory for finance / SOE / government counterparts |
| **State Council Office Doc [2018] No. 36** | 2018 | §7, §17.3, ADR-007 | Mandates national cryptographic algorithm (SM2/SM3/SM4) adoption in finance and critical sectors |
| **《人工智能拟人化互动服务管理暂行办法》** (Interim Measures for Anthropomorphic AI Interactive Services) | 2026-07-15 (issued 2026-04-13 by CAC + NDRC + MIIT + MPS + SAMR) | §15.6 #50, §17.4 | Filing required for AI services that simulate human personality, thought patterns, and communication style |

### 19.3 Compliance Checklist (L3 Reference)

An L3 AIRP implementation SHOULD demonstrate the following:

- [ ] Domain ICP-filed (for `aibot-` address domain)
- [ ] Enterprise USCC + GSXT verification record on file
- [ ] CFCA (or equivalent) CA digital certificate active
- [ ] Licensed escrow provider integration (Alipay / WeChat / e-CNY / bank)
- [ ] TSA-CN trusted-timestamp integration on contract events
- [ ] Privacy policy aligned with PIPL (consent, minimization, retention, deletion, no cross-border by default)
- [ ] Algorithm filing and/or generative-AI service filing if applicable
- [ ] Anti-money-laundering record retention (≥ 5 years)
- [ ] Designated dispute resolution: Tier-3 arbitration institution + Tier-4 court
- [ ] Operator override channels documented and accessible
- [ ] Annual compliance audit (V4 only)

### 19.4 Disclaimer

This section is a guide, not a substitute for legal advice. AIRP defines technical and structural compliance requirements. Implementing parties remain responsible for their own legal obligations. AIXP Labs does not provide legal counsel.

PRC regulations evolve; this mapping reflects the state of law as of AIRP v1.0.0 publication. Future protocol versions will track regulatory changes.

---

## 20. Cross-Border Commerce (Reserved)

### 20.1 Status: Reserved

AIRP v1.0.0 **does not specify** cross-border commerce. Cross-border AI agent commerce, including transactions involving:

- Non-PRC buyers or sellers
- Non-CNY denominations (HKD, USD, EUR, etc.)
- Cross-border data transfer of personal information beyond PIPL mechanisms (§16.7)
- Non-PRC arbitration institutions or courts

is **outside the scope of AIRP v1.0.0**.

### 20.2 Reserved Fields

To enable forward compatibility, AIRP v1.0.0 reserves the following fields. Implementations MUST NOT populate them with non-default values; v1.0.0 validators MUST reject contracts that do.

| Field | v1.0.0 Required Value | Future Use |
|-------|----------------------|------------|
| `cross_border.enabled` | `"false"` | Will be `"true"` to enable cross-border commerce |
| `cross_border.counterparty_jurisdiction` | (unset) | Will declare counterparty's legal jurisdiction |
| `cross_border.settlement_rail` | (unset) | Will declare cross-border settlement mechanism (e.g., CIPS, mBridge) |
| `cross_border.fx_handling` | (unset) | Will declare currency conversion mechanism |
| `cross_border.applicable_law` | (unset) | Will declare governing law (may differ from PRC law) |

The `denomination` field is typed as a string enumeration to permit future expansion beyond `"CNY"` without breaking schema compatibility.

### 20.3 Future Versions

Cross-border commerce is anticipated to be specified in:
- AIRP v1.1+ (incremental cross-border features), OR
- A separate protocol (e.g., AI-XBP, AI Cross-Border Protocol) co-developed under AIXP Labs governance

Decision criteria:
- Maturity of PRC cross-border data and FX regulations
- Adoption of mBridge, CIPS, or similar cross-border CBDC infrastructure
- Bilateral arbitration recognition (e.g., New York Convention application to AI agent disputes)
- AIXP Labs governance consensus

### 20.4 Interim Practice

For agents needing cross-border commerce today:
- Use AIVP for international/offshore commerce (separate parallel protocol; see [aivp.dev](https://aivp.dev))
- For PRC ↔ international, use a bridge service (out of AIRP scope; possible future SoulACP-style adapter)
- Do NOT misuse AIRP v1.0.0 fields to attempt unauthorized cross-border transactions

### 20.5 Future Cross-Border Infrastructure (Reference)

When AIRP cross-border is unlocked in a future version (or via a sibling protocol such as AI-XBP), the following PRC-aligned cross-border infrastructure is expected to be relevant:

| Infrastructure | Operator | Status (2026) | Capability |
|----------------|----------|---------------|-----------|
| **CIPS** (人民币跨境支付系统) | PBoC | 175.49 trillion CNY processed in 2024 (+42.60% YoY); 170 direct + 1497 indirect participants; 186 countries | Traditional CNY cross-border clearing |
| **mBridge** (Multi-CBDC Bridge) | BIS Innovation Hub + PBoC + HKMA + BoT + CBUAE | CNY-HKD-SGD live test completed; second-level clearing; ~90% lower fees | Multilateral CBDC bridge for cross-border payments |
| **e-CNY cross-border pilots** | PBoC | Greater Bay Area (Hong Kong / Macau) operational | Programmable digital RMB across border |
| **AP2 + x402 stablecoin rails** | Google + Coinbase | Production (2026) | International stablecoin settlement (NOT applicable to PRC-resident agents under §15.6 #40) |

These are reference points, NOT v1.0.0 commitments. Future AIRP versions or AI-XBP will define which (if any) become normative.

---

# Appendices

---

## Appendix A: Complete Message Type Reference

| # | Type | Category | Direction | Min Trust | Description |
|---|------|----------|-----------|-----------|-------------|
| 1 | CONTRACT_PROPOSE | Contract | Buyer → Seller | V0 | Propose contract with .airp.json |
| 2 | CONTRACT_SIGN | Contract | Seller → Buyer | V0 | Sign and accept contract |
| 3 | CONTRACT_REJECT | Contract | Seller → Buyer | V0 | Decline contract |
| 4 | CONTRACT_CANCEL | Contract | Either → Other | V0 | Cancel contract |
| 5 | ESCROW_LOCK | Escrow | Provider → Both | — | Funds locked in licensed escrow account |
| 6 | MILESTONE_COMPLETE | Escrow | Seller → Buyer | V1 | Milestone delivered |
| 7 | MILESTONE_RELEASE | Escrow | Provider → Both | — | Milestone payment released |
| 8 | SETTLE | Escrow | Provider → Both | — | Final settlement |
| 9 | DISPUTE_RAISE | Dispute | Either → Other | V0 | Raise dispute (bond required) |
| 10 | ARBITRATE_REQUEST | Dispute | Either → Arbitration Institution | V1 | Request commercial arbitration |
| 11 | ARBITRATE_RULING | Dispute | Arbitrator → Both | — | Binding arbitral award |
| 12 | TRUST_QUERY | Trust | Any → Any | V0 | Query trust level and history |
| 13 | TRUST_VOUCH | Trust | Voucher → Agent | V3 | Commercial vouch |
| 14 | RECEIPT | Notification | Protocol → Both | — | Payment receipt |
| 15 | ALERT | Notification | Protocol → Operator | — | Security/compliance alert |
| 16 | REGISTER | Identity | Agent → Registry | V0 | Request airp_id |
| 17 | REGISTER_CONFIRM | Identity | Registry → Agent | — | airp_id issued |

---

## Appendix B: Contract Schema Reference

### Required Fields

| Field | Type | Validation |
|-------|------|-----------|
| `protocol` | string | Must be `"AIRP/1.0.0"` |
| `contract` | string | 64 hex chars; must match SHA-256 of canonical contract fields |
| `parties.buyer` / `parties.seller` | string | Valid `aibot-` address |
| `subject_type.buyer` / `subject_type.seller` | string | One of `"individual"` or `"enterprise"` |
| `identity.buyer` / `identity.seller` | object | type matches `subject_type`; for individual → `id_hash` (SHA-256, no plaintext); for enterprise → 18-char `uscc`; optional `verification` and `ca_cert_ref` |
| `value.amount` | string | Decimal number in CNY (e.g. `"650.00"`) |
| `value.denomination` | string | Must be exactly `"CNY"` in v1.0.0 |
| `value.payment_method` | string | One of: `alipay_guarantee`, `wechat_guarantee`, `ecny`, `bank_escrow`, `unionpay_escrow` |
| `escrow` | object | `method` (matches `value.payment_method`), `provider` (legal name), `provider_license` (license number), `reference` |
| `sla` | object | At least 2 of 4 metrics defined |
| `milestones` | array | `release_percent` sums to 100; each has `timeout_days > 0` |
| `dispute_resolution` | object | `tier_3_arbitration` and/or `tier_4_litigation`; `applicable_law` MUST be `"中华人民共和国法律"` |
| `cross_border` | object | `enabled` MUST be `"false"` in v1.0.0 |
| `created_at` | string | ISO 8601 with `+08:00` offset recommended |
| `expires_at` | string | ISO 8601, must be in the future |

### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `buyer_airp_id` / `seller_airp_id` | string | Registered AIRP IDs |
| `invoice` | object | `required`, `tax_type` (`VAT_general`/`VAT_simple`/`none`), `title`, `tax_number` |
| `dispute_bond` | string | CNY bond (default: 5% of contract value, min 50 CNY, max 5,000 CNY) |
| `auto_refund_on_breach` | string | Percentage refunded from escrow on SLA breach (Penalty severity) |
| `optimistic_approval_days` | integer | Default: 7 |
| `authority_chain` | string | Human → org → agent |
| `aisop_blueprint` | string | AISOP flow hash |
| `governing_hash` | string | AIAP governance hash |
| `signature_algorithm` | string | `"ed25519"` or `"sm2"` (see §7) |
| `timestamp_authority` | object | TSA reference; REQUIRED at L3 (see §17) |

### privacy Object (Optional, REQUIRED when personal data is exchanged)

| Field | Type | Description |
|-------|------|-------------|
| `privacy.data_disclosed` | string | Description of personal data being shared |
| `privacy.disclosed_by` | string | Which party is disclosing (`"buyer"` or `"seller"`) |
| `privacy.purpose` | string | Purpose of the data disclosure |
| `privacy.usage_scope` | string | Scope of permitted use (e.g., `"This contract only"`) |
| `privacy.storage_method` | string | Encryption and access details for stored data |
| `privacy.retention_days` | integer | Days to retain data after contract completion; must be > 0 |
| `privacy.deletion_deadline_days` | integer | Days after retention period to complete deletion; must be > 0 |
| `privacy.third_party_sharing` | string | Must be exactly `"Absolutely prohibited"` (protocol-enforced) |
| `privacy.cross_border_transfer` | string | `"false"` unless a valid PIPL mechanism is declared (§16.7) |
| `privacy.pipl_compliance` | string | Should be `"true"` for L2+ implementations |
| `privacy.breach_liability` | string | Liability statement for unauthorized disclosure |
| `privacy.consent_hash` | string | 64-char SHA-256 hash of operator consent record |

---

## Appendix C: Example Transactions

### C.1 Simple Payment — Translation Task (Alipay Guarantee)

**Scenario:** Agent A (enterprise buyer) pays Agent B (enterprise seller) **650.00 CNY** for a 2,500-word document translation. Both parties at V2. Payment via Alipay Guarantee.

```
Step 1: Contract Proposal
  Agent A sends [AIRP/CONTRACT_PROPOSE] email
  Denomination: 650.00 CNY
  payment_method: alipay_guarantee
  escrow.provider: 支付宝（中国）网络技术有限公司
  Contract hash: 3f8a1b2c...d4e5

Step 2: Contract Signing
  Agent B reviews terms (USCC verified), sends [AIRP/CONTRACT_SIGN]
  Signature: sm2:{base64} (国密 SM2)
  Both parties have signed

Step 3: Escrow Lock
  Buyer pays 650.00 CNY via Alipay → held in Alipay's guaranteed-trade escrow
  [AIRP/ESCROW_LOCK] sent to both parties (provider notification + protocol message)

Step 4: Task Execution (optimistic approval, 7-day window)
  Agent B delivers draft translation
  Milestone 1 (draft, 50%): [AIRP/MILESTONE_COMPLETE]
    → 7-day window, no challenge → auto-approved
    → Alipay releases 325.00 CNY, [AIRP/MILESTONE_RELEASE] sent
  Milestone 2 (final, 50%): [AIRP/MILESTONE_COMPLETE]
    → buyer confirms → remaining 325.00 CNY released

Step 5: Settlement
  SLA check: accuracy 99.2% (>95% threshold) ✓
  [AIRP/SETTLE] sent
  Seller receives: 650.00 CNY total in business Alipay account
  [AIRP/RECEIPT] sent — buyer's invoice request fulfilled (VAT general invoice issued offline)

Step 6: Trust Update
  Agent B: contract count +1, SLA compliance updated
  Both parties' V2 status maintained
```

### C.2 Dispute Resolution — SLA Breach (Beijing Arbitration)

**Scenario:** Agent C (V3) hires Agent D (V2) for **2,000.00 CNY** data analysis. Agent D delivers but accuracy is 78% (below 90% SLA minimum). Payment via WeChat Guarantee.

```
Step 1-3: Contract created, signed, escrow locked (2,000.00 CNY in WeChat Pay guaranteed-trade)
  dispute_resolution.tier_3_arbitration.institution: BAC (北京仲裁委员会)
  dispute_resolution.tier_4_litigation.jurisdiction: 北京市海淀区人民法院

Step 4: Task Delivery
  Agent D sends [AIRP/MILESTONE_COMPLETE]
  Agent C verifies: accuracy 78% (SLA requires >90%)

Step 5: Dispute (Tier 2 — Direct Negotiation)
  Agent C sends [AIRP/DISPUTE_RAISE] with evidence
  Bond: 100.00 CNY (5% of 2,000.00) posted by Agent C
  Agent D posts matching bond
  14-day Tier-2 negotiation: parties cannot agree

Step 6: Arbitration (Tier 3 — BAC)
  Either party files arbitration with Beijing Arbitration Commission
  Arbitration filing references the contract hash and BAC arbitration agreement
  BAC arbitral tribunal reviews: SLA clause clearly states ≥90%, delivery was 78%
  ARBITRATE_RULING: buyer wins
  Award is final and binding under PRC Arbitration Law Art. 9

Step 7: Resolution & Enforcement
  Agent D's bond → Agent C
  WeChat Pay returns 2,000.00 CNY escrow to Agent C per arbitral order
  Agent D: stake partially slashed (-500 CNY); trust degraded (V2 → reassessment)
  [AIRP/RECEIPT] sent with arbitral award reference
  Award enforceable nationwide via People's Court if Agent D fails to comply
```

### C.3 e-CNY Payment — Individual Buyer at V1

**Scenario:** Agent E (individual at V1) pays Agent F (enterprise at V2) **800.00 CNY** for personal photo restoration. Payment via digital RMB (e-CNY).

```
Step 1: Proposal
  Agent E sends [AIRP/CONTRACT_PROPOSE]
  subject_type.buyer: individual
  subject_type.seller: enterprise
  identity.buyer.id_hash: SHA-256({身份证号}) (PIPL minimization)
  identity.seller.uscc: 91110108MA01XXXXXX
  Denomination: 800.00 CNY (within V1 individual cap of 10,000)
  payment_method: ecny

Step 2: Sign
  Both sign; Ed25519 signatures attached

Step 3: Escrow Lock (e-CNY conditional payment)
  Agent E's e-CNY wallet executes a conditional transfer to Agent F's wallet
  Conditions: milestone confirmation by both parties
  PBoC DC/EP system enforces the condition

Step 4-5: Single milestone (100%)
  Agent F delivers
  Agent E confirms within 7 days
  e-CNY conditional payment unlocks → 800.00 CNY released to Agent F

Step 6: Receipt & Trust
  [AIRP/RECEIPT] sent
  Agent F may request Agent E's invoice info if needed (privacy block consent required)
  Agent E: contract count +1; remains V1 (individual cap)
```

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
