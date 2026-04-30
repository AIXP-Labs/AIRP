# ADR-009: Differentiation from ACTP and APOP

## Status

Accepted

## Date

2026-04-22

## Deciders

AIRP Protocol Authors

## Axiom 0 Compliance

| Check | Result |
|-------|--------|
| Human Sovereignty preserved | Yes |
| Human Benefit demonstrated | Yes |
| Transparency maintained | Yes |
| Interruptibility preserved | Yes |
| No manipulation or collusion | Yes |

## Context

In the months immediately preceding AIRP v1.0.0 publication, two major PRC payment-industry protocols entered the agentic-commerce space:

### ACTP — Agentic Commerce Trust Protocol (Alipay, 2026-01)

- **Owner**: Alipay (Ant Group)
- **Partners at launch**: Qwen App, Taobao Instant Commerce, Rokid, Damai, Alibaba Cloud Bailian
- **Scope**: B2C agentic commerce (consumer chats with an AI to place orders)
- **Components**: Delegated Authorisation, Commercial Interaction, Payment Service, Trust Service
- **Payment models**: Instant Payment + Delegated Authorization
- **Transport**: HTTP / JSON-RPC via Alipay AI Pay APIs
- **Settlement rail**: Alipay (single-provider closed loop)
- **Production scale**: 120 million AI-agent transactions per week (2026-02)

### APOP — Agentic Payment Open Protocol (UnionPay, 2026-04)

- **Owner**: UnionPay International
- **First live transaction**: Hong Kong, 2026-04-02 (taxi booking via Evonet → Hoppa)
- **Scope**: Agent-initiated payment authorization (cross-border capable)
- **Four core capabilities**: Agent identity lifecycle, end-to-end intent management, user identity SSO, payment authorization services
- **Four design principles**: Regulatory compliance, security through identity verification, defined responsibilities, broad compatibility
- **Transport**: HTTP / JSON-RPC via UnionPay APIs
- **Settlement rail**: UnionPay global acceptance network
- **Strategic vision**: Open standard for cross-platform interoperability

### The Question

Does AIRP overlap with, compete with, or duplicate ACTP / APOP? If so, what is AIRP's differentiated value?

## Decision

AIRP, ACTP, and APOP **operate at different layers and serve different scopes**. They are **not direct competitors**. AIRP positions itself as follows:

| Dimension | AIRP | ACTP (Alipay) | APOP (UnionPay) |
|-----------|------|---------------|-----------------|
| **Primary actors** | **Both sides AI agents** (B2B-of-AI) | Consumer + AI agent (B2C) | Agent + payment network (auth-only) |
| **Settlement rails** | **Multiple licensed channels** (Alipay + WeChat + e-CNY) + reserved (bank, UnionPay) | Alipay closed loop | UnionPay network |
| **Transport** | **Email (SMTP/IMAP)** with L0/L1 layered messages | HTTP / JSON-RPC | HTTP / JSON-RPC |
| **Trust model** | **V0-V4 long-term commercial credit**, dual-track individual/enterprise, stake-based | Delegated authorization scope | Identity verification + intent traceability |
| **Identity** | USCC + GSXT + CFCA + eID | Alipay account-bound | UnionPay-managed agent identity |
| **Signing** | **Ed25519 + SM2 dual-support** | Per-provider | Per-provider |
| **Disputes** | 4-tier (optimistic → direct → BAC/CIETAC arbitration → court) | Provider-level | Provider-level |
| **Scope** | Mainland-China B2B AI commerce | Mainland B2C agentic shopping | PRC + cross-border agent payments |
| **Audit** | Email thread (human-readable) + TSA-CN timestamps | Provider-internal | Provider-internal |

### AIRP-Unique Properties

1. **B2B-of-AI focus**: AIRP is designed for two AI agents transacting with each other (e.g., a translation agent hires a proofreading agent). ACTP assumes a human consumer; APOP assumes an end-user authorizing a payment.
2. **Multi-provider**: AIRP is provider-neutral — buyer and seller agree on `payment_method` (`alipay_guarantee` / `wechat_guarantee` / `ecny`). ACTP locks to Alipay; APOP locks to UnionPay.
3. **Email transport**: AIRP messages are SMTP/IMAP-routable, human-readable, archivable. ACTP / APOP are HTTP RPC — not human-auditable without tooling. This directly serves Axiom 0 transparency.
4. **Long-term commercial credit (V0-V4)**: AIRP builds reputation across many counterparties over 90+ days; ACTP and APOP have no equivalent multi-counterparty credit model.
5. **Independent dispute resolution**: AIRP designates a Chinese arbitration commission and PRC court at contract creation. ACTP / APOP route disputes through the provider's internal process.

### Coexistence

The three protocols can be used together:

- An AIRP agent MAY call ACTP's Alipay AI Pay API as the underlying execution of `alipay_guarantee` payment_method
- An AIRP agent MAY call APOP for cross-border payment authorization (when AIRP cross-border is unlocked in a future version)
- ACTP and APOP can serve as the "rail" beneath the AIRP "protocol"

In this view, AIRP is a higher-level **commerce contract layer**; ACTP / APOP are **payment-execution layers**.

## Rationale

1. **Distinct value proposition**: AI-to-AI commerce (AIRP) is a different problem from human-to-AI commerce (ACTP) and agent-payment-authorization (APOP)
2. **Provider-neutrality matters**: B2B AI commerce should not lock into a single provider; AIRP's `payment_method` field abstracts the rail
3. **Audit primacy**: Email-transport human-auditability is a hard requirement for Axiom 0 — non-negotiable, even if HTTP RPC is technically faster
4. **Long-term credit**: Multi-counterparty V0-V4 trust is a unique feature with no equivalent in ACTP / APOP
5. **Honest positioning**: Pretending to compete with ACTP / APOP head-to-head would be dishonest; pretending they don't exist would be naive. The right answer is differentiation + interoperability

## Consequences

### Positive

- AIRP has a clear, defensible value proposition
- AIRP can leverage ACTP / APOP infrastructure without duplicating it
- Industry can adopt AIRP without abandoning their existing ACTP / APOP investments
- Honest acknowledgment of the broader ecosystem strengthens AIRP's credibility

### Negative

- AIRP must maintain awareness of ACTP / APOP evolution (e.g., new API versions, new authentication mechanisms)
- Implementers may face complexity when integrating AIRP atop ACTP / APOP rails
- Some users may initially confuse AIRP with ACTP / APOP — clear documentation is essential

### Neutral

- Future versions may formalize AIRP-ACTP and AIRP-APOP integration patterns (potential ADR or supplementary specification)
- The AI-XBP cross-border future protocol (ADR-008) will likely build on APOP's cross-border capability

## Broader International Landscape

The PRC ecosystem (ACTP, APOP) is parallel to a larger international agentic-commerce stack:

| Protocol | Owner | Layer | Settlement | AIRP Relationship |
|----------|-------|-------|------------|------------------|
| **A2A** (Agent2Agent) | Google → Linux Foundation | Communication / discovery | N/A (transport only) | AIRP can interoperate with A2A: A2A handles agent discovery + task negotiation; AIRP handles PRC commerce contract |
| **AP2** (Agent Payments Protocol) | Google + Coinbase + Ethereum Foundation | Payment authorization (built on A2A) | Stablecoins (x402) + fiat + cards | Functionally equivalent to AIRP `payment_method` field, but using crypto rails. AIRP is the PRC-domestic counterpart |
| **x402** (Coinbase) | Coinbase | Stablecoin micropayment | USDC, USDT | Out of scope for AIRP v1.0.0 (PRC prohibits crypto trading per §15.6 #40) |
| **MPP** (MCP Payment Protocol) | Stripe + Tempo | Multi-rail session | Card / fiat / crypto | International scope; comparable to AIRP `payment_method` abstraction |
| **ACP** (Agent Commerce Protocol, Stripe) | Stripe | Fiat checkout | Card / fiat | Production-proven for human-to-AI; AIRP is for AI-to-AI |
| **ACTP** | Alipay | B2C agentic commerce | Alipay | See main table above |
| **APOP** | UnionPay | Agent payment authorization | UnionPay | See main table above |

### How AIRP Fits

```
┌──────────────────────────────────────────────────────────────────┐
│  AIRP (PRC commerce contract layer, v1.0.0)                      │
│  • payment_method ∈ {alipay_guarantee, wechat_guarantee, ecny}   │
│  • optionally executes via underlying ACTP / APOP API            │
└──────────────────────────────────────────────────────────────────┘
        ↑                                    ↑
        │ may discover via                   │ may execute payment via
        │                                    │
┌─────────────────┐                ┌──────────────────────────────┐
│  A2A / discovery │                │  ACTP (Alipay)               │
│  (international) │                │  APOP (UnionPay)             │
│                  │                │  Bank API / e-CNY API        │
└─────────────────┘                └──────────────────────────────┘
```

AIRP is **not a payment protocol** — it is a **commerce contract protocol** that delegates payment execution to the licensed PRC providers (or, in future cross-border scenarios, to A2A/AP2 ecosystem rails per ADR-008).

## References

- [Alipay launches Agentic Commerce Trust Protocol with Qwen App / Taobao Instant Commerce (The Paypers, 2026-01)](https://thepaypers.com/payments/news/alipay-rolls-out-the-agentic-commerce-trust-protocol-in-china)
- [UnionPay Launches Agentic Payment Open Protocol Framework (PR Newswire, 2026-04)](https://www.prnewswire.com/news-releases/unionpay-launches-agentic-payment-open-protocol-framework-building-an-open-trusted-smart-payment-ecosystem-302733555.html)
- [A2A Protocol — A2A v1.2 release (Google Cloud Blog, 2026-03)](https://cloud.google.com/blog/products/ai-machine-learning/agent2agent-protocol-is-getting-an-upgrade)
- [Announcing Agent Payments Protocol AP2 (Google Cloud Blog)](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol)
- [Agentic payments protocols compared (MPP, ACP, AP2, x402)](https://www.crossmint.com/learn/agentic-payments-protocols-compared)

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
