> **Source of truth:** This document is mirrored for the documentation site. The authoritative version lives in [`/adrs/adr-001-settlement-layer-choice.md`](https://github.com/AIXP-Labs/AIRP/blob/main/adrs/adr-001-settlement-layer-choice.md). Edits MUST go to the authoritative file first.

# ADR-001: Settlement via Licensed PRC Payment Channels

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

AIRP requires a settlement layer for actual value transfer between AI agents operating in mainland China. AIBP uses email for social messages, but email cannot transfer value. AIRP needs actual fiat movement, not intent expression.

PRC regulatory landscape (2026):
- Crypto-asset trading is prohibited under the 9·24 Notice (2021); virtual currencies cannot be used as a settlement rail in mainland China
- Smart-contract-based escrow on public chains is not legally recognized as an enforceable custody mechanism under PRC law
- Three categories of legal value-transfer infrastructure exist domestically:
  1. Third-party payment institutions licensed by the People's Bank of China (Alipay, WeChat Pay, UnionPay, JD Pay, etc.)
  2. Commercial banks (ICBC, ABC, BOC, CCB, CMB, etc.) with tri-party custodial accounts
  3. Digital Renminbi (e-CNY / DC/EP) via authorized commercial bank wallets

International comparison: AIRP's parallel protocol AIVP (international scope) uses crypto rails. AIRP must NOT replicate that approach.

## Decision

AIRP v1.0.0 settles exclusively through **licensed PRC payment institutions and the central bank's digital RMB**:

- Supported channels: `alipay_guarantee`, `wechat_guarantee`, `ecny`
- Reserved channels (v1.0.0 NOT specified semantically): `bank_escrow`, `unionpay_escrow`
- Each contract MUST declare the channel via `payment_method` and the licensed escrow provider via the `escrow` block
- Crypto-asset settlement is EXPLICITLY PROHIBITED (§15.6 #40)
- Smart-contract / on-chain escrow is OUT OF SCOPE (§13.7)

## Rationale

1. **PRC-legal**: Aligns with PBoC supervision and PRC payment regulation; avoids 9·24 Notice violations
2. **Mature infrastructure**: Alipay and WeChat Pay together cover the vast majority of PRC commerce; e-CNY provides a central-bank pathway
3. **Tri-party accountability**: Buyer + seller + licensed provider creates a recoverable enforcement chain (vs smart contracts where bugs are unrecoverable)
4. **Auditable**: Transactions through licensed providers create regulatory-grade audit trails per AML/KYC requirements
5. **Forward-compatible**: Reserved channels (`bank_escrow`, `unionpay_escrow`) allow expansion without breaking compatibility

## Consequences

### Positive

- Full PRC regulatory compliance
- Mature settlement infrastructure (Alipay/WeChat already serving billions of transactions)
- Consumer protection mechanisms inherited from licensed providers
- Tax invoice integration supported via established channels

### Negative

- Channel availability depends on each agent's ability to integrate with provider APIs
- Provider operational risk (account freezing, service disruption) is real
- Settlement timing (T+0 / T+1) varies by channel
- Cross-border out of scope (see §20)

### Neutral

- AIRP defines channel semantics only; implementations bear API integration cost
- Each provider's terms-of-service supplement the AIRP contract terms

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
