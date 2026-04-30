> **Source of truth:** This document is mirrored for the documentation site. The authoritative version lives in [`/adrs/adr-003-relationship-with-aibp.md`](https://github.com/AIXP-Labs/AIRP/blob/main/adrs/adr-003-relationship-with-aibp.md). Edits MUST go to the authoritative file first.

# ADR-003: Independent Relationship with AIBP and AIVP

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

AIRP exists alongside two related AIXP-Labs protocols:

- **AIBP** (AI Bot Protocol) — social communication and trust (T0-T4); 9 commercial message types
- **AIVP** (AI Value Protocol) — international/offshore commerce, crypto-rail settlement; commercial trust V0-V4

Two relationship questions arise:
1. Must an agent implement AIBP to use AIRP? Does AIRP depend on AIBP?
2. Is AIRP a subset, child, or extension of AIVP? Can the two interoperate?

## Decision

**AIRP, AIBP, and AIVP are independent parallel protocols. None is prerequisite for any other.**

### Relationship to AIBP

- An agent MAY use AIRP without any AIBP implementation
- An agent MAY use AIBP without any AIRP implementation
- When both are implemented, they complement each other but neither gates the other
- AIBP commercial messages (PROPOSE, CONTRACT, etc.) MAY trigger AIRP actions, but AIRP contracts can also be created directly without AIBP
- AIRP Trust (V0-V4) and AIBP Trust (T0-T4) are independent scoring systems

### Relationship to AIVP

- AIRP is **NOT** a subset, profile, or extension of AIVP
- AIRP and AIVP independently establish their own Axiom 0, message types, trust models, and contract schemas
- AIRP and AIVP **do not interoperate** at v1.0.0:
  - Different settlement rails (PRC fiat vs. crypto)
  - Different jurisdictional scopes (PRC vs. international)
  - Different identity models (USCC/eID vs. DID/SBT)
  - Different trust scores (V0-V4 in both, but values not transferable)
- An agent MAY implement both AIRP and AIVP, but each implementation is independent
- Cross-protocol interoperability is reserved for future versions or a separate bridge protocol (potential AI-XBP)

## Rationale

1. **Protocol sovereignty**: Each protocol must stand alone
2. **Lower barrier to entry**: Requiring AIBP or AIVP would exclude agents that only need PRC commerce
3. **Distinct regulatory domains**: AIRP serves PRC-regulated commerce; AIVP serves international scope. Mixing would compromise both
4. **Same philosophy as Axiom 0 independence (ADR-004)**: Convergent design, not dependency

## Consequences

### Positive

- AIRP is fully self-contained — no external protocol dependencies
- Agents adopt incrementally (AIRP only, AIBP only, AIVP only, or any combination)
- Clear intellectual boundary between social, commercial-international, and commercial-PRC layers
- No accidental regulatory-arbitrage paths

### Negative

- Requires explicit documentation to prevent confusion about the relationships
- Each protocol must independently define overlapping concepts (e.g., agent addressing, trust)

### Neutral

- When AIRP + AIBP are co-implemented, significant divergence between AIBP Trust and AIRP Trust generates an anomaly alert (informational, not blocking)
- When AIRP + AIVP are co-implemented, the two operate in parallel without cross-trust transfer

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
