> **Source of truth:** This document is mirrored for the documentation site. The authoritative version lives in [`/adrs/adr-008-cross-border-deferred.md`](https://github.com/AIXP-Labs/AIRP/blob/main/adrs/adr-008-cross-border-deferred.md). Edits MUST go to the authoritative file first.

# ADR-008: Cross-Border Commerce Deferred to Future Versions

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

PRC AI agents will inevitably transact with international counterparts: outsourced labor, foreign data sources, cloud services, and international AI service providers are part of normal commerce. AIRP could attempt to address cross-border in v1.0.0, but doing so would require:

- **FX mechanism design**: handling CNY ↔ USD/HKD/EUR conversion, timing, slippage
- **Cross-border data transfer compliance**: PIPL Art. 38-40 mechanisms (security assessment, standard contract, certification)
- **Foreign-jurisdiction recognition**: arbitration recognition under New York Convention, court enforcement under bilateral treaties
- **AML/KYC for foreign counterparties**: cross-border anti-money-laundering; foreign AML regimes
- **Settlement-rail interoperability**: bridging PRC payment infrastructure with foreign systems (CIPS, mBridge, SWIFT, etc.)
- **Foreign-exchange administration**: SAFE rules on individual and corporate cross-border transactions

Each of these is a substantial sub-protocol. Doing them poorly in v1.0.0 would create regulatory and user-trust risk; doing them well would multiply v1.0.0 scope.

## Decision

AIRP v1.0.0 **explicitly defers cross-border commerce**. Cross-border features are reserved (§20) but not specified.

- `cross_border.enabled` MUST be `"false"` in v1.0.0
- Implementations MUST reject contracts that attempt cross-border use
- AIVP serves international scope as a parallel protocol (ADR-003)
- A future protocol — provisionally **AI-XBP (AI Cross-Border Protocol)** — or a future AIRP minor version (v1.1+) MAY specify cross-border AI commerce

## Rationale

1. **Scope discipline**: A v1.0.0 that does PRC commerce well is more valuable than a v1.0.0 that attempts everything and serves no one well
2. **Regulatory uncertainty**: PRC cross-border data transfer rules (PIPL implementing rules, CAC standard contract) are still maturing; locking in protocol design now would force premature commitments
3. **Settlement infrastructure maturity**: mBridge (multi-CBDC bridge), CIPS (cross-border interbank payment system), and other settlement rails are evolving; AIRP should observe before specifying
4. **Existing alternative**: AIVP already serves international/offshore scope; users with cross-border needs have an immediate option
5. **Reserved fields preserve forward path**: Schema-level reservation prevents v1.1+ from breaking compatibility

## Consequences

### Positive

- v1.0.0 scope is bounded and achievable
- Regulators can evaluate AIRP without ambiguity about its reach
- Users with cross-border needs are explicitly told to use AIVP
- Future cross-border protocol benefits from observing v1.0.0 production usage

### Negative

- PRC users with foreign counterparts cannot use AIRP for those transactions
- Two-protocol management (AIRP + AIVP) for users straddling both
- Risk that implementations accidentally enable cross-border via misconfiguration — mitigated by explicit `cross_border.enabled = "false"` validation

### Neutral

- A future AI-XBP protocol may consume both AIRP and AIVP types and bridge them
- v1.1+ may incrementally add cross-border features

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
