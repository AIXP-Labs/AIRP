> **Source of truth:** This document is mirrored for the documentation site. The authoritative version lives in [`/adrs/adr-005-email-as-transport.md`](https://github.com/AIXP-Labs/AIRP/blob/main/adrs/adr-005-email-as-transport.md). Edits MUST go to the authoritative file first.

# ADR-005: Email as Transport Layer

## Status

Accepted

## Date

2026-04-21

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

AIRP needs a transport layer for commercial communication (contract proposals, signatures, settlements, disputes). AIBP uses email for social messages — proven, decentralized, and auditable.

Candidates considered:
- **HTTP/REST APIs** — Synchronous, requires server infrastructure, industry standard for payments
- **WebSocket** — Real-time but requires persistent connections
- **Message queues** (RabbitMQ, Kafka) — Requires broker infrastructure
- **Email (SMTP/IMAP)** — Mature, decentralized, human-readable, consistent with AIBP

Industry note: all competing payment protocols (x402, ACP, AP2, MPP) use HTTP. AIRP deliberately chooses email for AIBP alignment and Axiom 0 auditability.

## Decision

AIRP uses email (SMTP/IMAP) as its transport layer, mirroring AIBP:

- Agents use the same `aibot-{name}@{domain}` address for both AIBP and AIRP messages
- AIRP messages are distinguished by `X-AIRP-*` headers (not `X-AIBP-*`)
- Subject prefix: `[AIRP/{TYPE}]` (not `[AIBP/{TYPE}]`)
- Same L0/L1 two-layer architecture: L1 = human text, L0 = JSON metadata
- All JSON values must be human language (same rule as AIBP)

### Security Hardening (for financial communication)

- Every AIRP message MUST include a digital signature in the `X-AIRP-Signature` header — algorithm SHALL be Ed25519 OR SM2/SM3 (see ADR-007)
- Every message MUST include a nonce (`X-AIRP-Nonce`) and timestamp to prevent replay attacks
- Receiving agents MUST reject messages with duplicate nonce or timestamp >5 minutes old
- Sending domains MUST enforce DMARC `p=reject` policy
- Receiving agents MUST reject messages from domains without DMARC `p=reject`
- Contract-related L0 metadata (amounts, signatures) SHOULD be encrypted at message level
- All signatures are verifiable against the agent's published public key

### PRC-Specific Recommendations

- Domains used for `aibot-` addresses SHOULD be ICP-filed (备案) `.cn` or `.com` domains; L3 implementations REQUIRE ICP filing
- Recommended PRC enterprise mail providers: 腾讯企业邮箱 (Tencent), 阿里云邮箱 (Aliyun), 网易企业邮箱 (NetEase) — all support SPF/DKIM/DMARC
- Self-hosted SMTP servers MUST be filed with the appropriate communications authority where required by PRC law
- Cross-border email reception MUST be considered in light of cybersecurity requirements; foreign-domain mail to PRC `aibot-` addresses receives extra scrutiny

## Rationale

1. **Consistency**: Same transport as AIBP — one inbox for all protocol messages
2. **Decentralized**: No central API server needed
3. **Auditable**: Human operators can read AIRP contract emails directly (Axiom 0)
4. **Mature**: SMTP/IMAP is battle-tested over decades
5. **Identity reuse**: Agents already have `aibot-` addresses from AIBP (or can create one)
6. **Separation**: `X-AIRP-*` headers cleanly separate from `X-AIBP-*` messages

Email carries the contract COMMUNICATION (proposals, signatures, notifications). The actual VALUE SETTLEMENT happens via licensed PRC payment institutions (Alipay / WeChat Pay / e-CNY — see ADR-001). Email is the negotiation/notification layer; the licensed payment provider is the money layer.

## Consequences

### Positive

- Zero infrastructure barrier — any existing mail server works
- Human operators can monitor all commercial activity through standard email tools
- Natural audit trail with timestamps and threading
- Consistent developer experience with AIBP

### Negative

- Email has higher latency than direct API calls (seconds to minutes vs milliseconds)
- Email deliverability can be affected by spam filters
- Industry uses HTTP — AIRP is an outlier, which may face adoption skepticism
- BEC/spoofing risk ($6B losses in 2024) — mitigated by Ed25519 signatures + DMARC reject

### Neutral

- Email threading may not perfectly map to all commercial interaction patterns
- The `aibot-` prefix convention requires cooperation from domain administrators

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
