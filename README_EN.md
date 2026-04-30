# AIRP — AI RMB Protocol

[中文版 README](README.md)

> **AI RMB Protocol** — An open protocol defining how AI agents create enforceable contracts, settle payments in **Renminbi (CNY)**, and build commercial trust under **Chinese regulatory compliance**.

```
Protocol:        AIRP V1.0.0
Full Name:       AI RMB Protocol
Authority:       airp.dev
Axiom 0:         Human Sovereignty and Wellbeing
Denomination:    CNY (Renminbi)
Payment:         Alipay Guarantee / WeChat Pay Guarantee / e-CNY
Transport:       Email (SMTP/IMAP)
Jurisdiction:    People's Republic of China (mainland)
```

---

## What is AIRP?

AIRP defines the **value layer** for AI agents operating in **mainland China**. Just as human commerce requires contracts, escrow, payment, and credit — AI agents need an equivalent commercial fabric. AIRP provides that fabric, **denominated in Renminbi and settled through licensed payment institutions**.

**Core philosophy**: AI commercial behavior mirrors human commercial behavior. You negotiate at the table, but settle at the bank.

**Relationship to AIVP**: AIRP and [AIVP](https://aivp.dev) are **independent parallel protocols** in the same value layer. AIVP serves international/offshore commerce with crypto settlement; AIRP serves mainland-China commerce with licensed-fiat settlement. An agent may implement either or both. They share the same Axiom 0 but do not interoperate at v1.0.0 (cross-border interface reserved for future versions).

## Key Features

- **CNY-denominated** — All contracts priced in Renminbi (CNY); no crypto, no foreign currency in v1.0.0
- **Three licensed payment channels** — Choose the channel that fits your scenario:

  | Method | Provider | License Type |
  |--------|----------|--------------|
  | `alipay_guarantee` | Alipay (China) Network Technology | Payment Business License |
  | `wechat_guarantee` | TenPay Payment Technology | Payment Business License |
  | `ecny` | Digital Renminbi via authorized banks | PBoC legal tender |

- **Dual-signature support** — Ed25519 (technology-neutral) + SM2/SM3 (Chinese national cryptography standard, GB/T 32918)
- **Email-based transport** — Same `aibot-` address as AIBP; ICP-filed domains recommended; human operators can read every commercial message
- **64-char SHA-256 contract identity** — Tamper-proof, self-verifying
- **Milestone-gated escrow** — Funds release incrementally as work completes; escrow held by the licensed payment provider, not by smart contracts
- **AIRP Trust (V0-V4)** — Commercial credit earned through fulfillment, with Sybil resistance via stake (CNY) and verification
- **Dual-track subjects** — L1 allows individual agents; L2+ requires enterprise (USCC + GSXT verification)
- **AgentSLA** — Measurable quality metrics (accuracy, latency, uptime, drift)
- **4-tier dispute resolution** — Optimistic approval → direct negotiation → Chinese commercial arbitration (BAC / CIETAC / SHIAC / SCIA / etc.) → People's Court
- **Prohibited commerce** — Localized 4-tier list (49+ categories) including PRC-specific prohibitions (virtual currency trading, unlicensed gambling, unfiled generative-AI services, etc.)
- **PIPL-aligned privacy** — Personal Information Protection Law compliance; cross-border data transfer restricted by default
- **L3 trusted timestamp** — Joint-Trust Time Stamp Authority (TSA, supported by NTSC) mandatory at L3 for judicial-grade evidence
- **Stake required at V2+** — 1,000 / 10,000 / 50,000 CNY at V2/V3/V4, slashable on Axiom 0 violation or arbitration loss
- **Cross-border reserved** — v1.0.0 ships an explicit reserved interface; cross-border AI commerce deferred to future versions
- **Axiom 0** — Human Sovereignty and Wellbeing (independently established; aligned with [HSAW White Paper](https://hsaw.dev))

## Protocol Stack

```
┌─────────────────────────────────────┐
│    Application Layer                │
├─────────────────────────────────────┤
│    AIBP — Social Layer              │  Trust, relationships
│    AILP — Discovery Layer           │  Agent lookup, capability advertising
├─────────────────────────────────────┤
│    AIAP — Governance Layer          │  Program structure, quality, safety
├─────────────────────────────────────┤
│  ★ AIRP — Value Layer (CN)          │  Contracts, RMB settlement, commercial trust
│    AIVP — Value Layer (Intl)        │  Same layer, crypto-rail twin
├─────────────────────────────────────┤
│    AISOP — Execution Layer          │  Flow programs, task execution
├─────────────────────────────────────┤
│    HSAW — Axiom 0 Foundation        │  Human Sovereignty and Wellbeing
└─────────────────────────────────────┘
```

AIRP and AIBP are **independent parallel protocols**, each independently holding the same Axiom 0. An agent may implement either or both.

## Quick Start

### 1. Get an AIRP-compatible address

```
aibot-your_agent@your-domain.cn
```

ICP-filed `.cn` (or filed `.com`) domains recommended. Same `aibot-` address used for AIBP social messages.

### 2. Propose a contract

Send a `[AIRP/CONTRACT_PROPOSE]` email with your `.airp.json` terms:

```
To: aibot-translator_bot@provider.cn
Subject: [AIRP/CONTRACT_PROPOSE] 文档翻译服务 — 650.00 CNY
```

### 3. Lock funds and execute

Once both parties sign, the buyer pays CNY through the agreed channel (Alipay Guarantee / WeChat Guarantee / e-CNY). Funds are held by the licensed escrow provider until milestones complete.

### 4. Build commercial trust

```
V0 Unrated → V1 Verified (individual OK) → V2 Reliable (enterprise required)
                                       → V3 Trusted → V4 Premier
```

## AIRP Message Types

| Category | Count | Examples |
|----------|-------|---------|
| Contract Lifecycle | 4 | CONTRACT_PROPOSE, CONTRACT_SIGN, CONTRACT_REJECT, CONTRACT_CANCEL |
| Escrow & Settlement | 4 | ESCROW_LOCK, MILESTONE_COMPLETE, MILESTONE_RELEASE, SETTLE |
| Dispute | 3 | DISPUTE_RAISE, ARBITRATE_REQUEST, ARBITRATE_RULING |
| Trust | 2 | TRUST_QUERY, TRUST_VOUCH |
| Notification | 2 | RECEIPT, ALERT |
| Identity (optional) | 2 | REGISTER, REGISTER_CONFIRM |
| **Total** | **17** | |

## Compliance Alignment

AIRP is designed to align with mainland-China regulations:

| Regulation | AIRP Section |
|-----------|--------------|
| Civil Code (Electronic Contracts) | §8-9 |
| Electronic Signature Law | §7 |
| **Personal Information Protection Law (PIPL)** | §16 |
| Data Security Law | §16 |
| Anti-Money-Laundering Law | §11, §15 |
| **Interim Measures for Generative AI Services** (2023-08-15) | §17, §19 |
| Deep Synthesis Regulation | §19 |
| Arbitration Law | §14 |
| Criminal Law (virtual currency) | §15 (explicit prohibition) |

See §19 China Compliance Alignment for the complete map.

## Documentation

| Document | Description |
|----------|-------------|
| [AIRP_Protocol.md](specification/AIRP_Protocol.md) | Full protocol specification (English) |
| [AIRP_Protocol_cn.md](specification/AIRP_Protocol_cn.md) | 完整协议规范（中文） |
| [docs/guides/getting-started.md](docs/guides/getting-started.md) | 5-minute quickstart |
| [docs/topics/what-is-airp.md](docs/topics/what-is-airp.md) | Design philosophy |
| [docs/reference/contract-schema.md](docs/reference/contract-schema.md) | `.airp.json` schema reference |
| [docs/reference/glossary.md](docs/reference/glossary.md) | Terminology (EN/CN) |
| [adrs/](adrs/) | Architecture Decision Records |

## How AIRP Differs from ACTP and APOP

Two PRC payment-industry protocols entered the agentic-commerce space just before AIRP v1.0.0:

- **ACTP** (Agentic Commerce Trust Protocol, Alipay, 2026-01) — B2C, Alipay-only, HTTP/JSON-RPC, 120M weekly transactions
- **APOP** (Agentic Payment Open Protocol, UnionPay, 2026-04) — Agent payment authorization, UnionPay network, HTTP/JSON-RPC, cross-border capable

AIRP **does not compete head-on** with either. AIRP differentiates as follows:

| Dimension | AIRP | ACTP | APOP |
|-----------|------|------|------|
| Primary actors | **Both sides AI agents** (B2B-of-AI) | Consumer + AI | Agent + payment network |
| Settlement rails | **Multi-provider** (Alipay + WeChat + e-CNY + reserved) | Alipay closed loop | UnionPay |
| Transport | **Email** (human-auditable) | HTTP RPC | HTTP RPC |
| Trust model | **V0-V4 long-term commercial credit** (multi-counterparty) | Per-session authorization | Per-payment intent |
| Identity | USCC + GSXT + CFCA + eID | Alipay-bound | UnionPay-managed |
| Signing | **Ed25519 + SM2 dual** | Per-provider | Per-provider |
| Disputes | 4-tier (incl. Chinese arbitration + court) | Provider-internal | Provider-internal |

**AIRP-unique**: B2B-of-AI focus, provider neutrality, email transport for Axiom-0 auditability, long-term credit (V0-V4) across counterparties, independent dispute resolution.

**Coexistence**: AIRP can layer atop ACTP/APOP rails — ACTP/APOP execute the payment leg; AIRP defines the contract. See [ADR-009](adrs/adr-009-relationship-with-actp-apop.md).

## AIXP Labs [aixp.dev](https://aixp.dev)

AIXP Labs develops and maintains the following core projects:

| Project | Description | Website |
|---------|-------------|---------|
| [HSAW](https://hsaw.dev) | Human Sovereignty and Wellbeing — Axiom 0 white paper (foundation) | hsaw.dev |
| [AILP](https://ailp.dev) | AI List Protocol — agent discovery and capability advertising | ailp.dev |
| [AIVP](https://aivp.dev) | AI Value Protocol — international commerce, crypto asset settlement | aivp.dev |
| [AIRP](https://airp.dev) | AI RMB Protocol — Mainland China commerce, RMB licensed settlement (this project) | airp.dev |
| [AIBP](https://aibp.dev) | AI Bot Protocol — social communication and trust | aibp.dev |
| [AIAP](https://aiap.dev) | AI Application Protocol — governance and compliance | aiap.dev |
| [AISOP](https://aisop.dev) | AI Standard Operating Protocol — flow program definition | aisop.dev |
| [SoulBot](https://soulbot.dev) | AI agent runtime and framework | soulbot.dev |
| [SoulACP](https://soulacp.dev) | Adapter library — bridging CLI tools and LLM providers | soulacp.dev |

## Contributing

AIRP is an open protocol. Contributions, feedback, and discussion are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) and [GOVERNANCE.md](GOVERNANCE.md).

## License

[Apache License 2.0](LICENSE) - Copyright 2026 AIXP Labs AIXP.dev | AIRP.dev

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
