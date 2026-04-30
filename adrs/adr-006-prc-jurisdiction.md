# ADR-006: PRC Jurisdiction as the Sole Scope of v1.0.0

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

AI commerce is inherently boundary-crossing — agents may operate from any geography, signal any jurisdiction. AIRP must explicitly declare its regulatory scope to set legitimate user expectations.

The protocol must address:
- Which legal system governs AIRP contracts?
- Which dispute-resolution mechanisms are recognized?
- Which data protection regime applies?
- Which prohibited-commerce list applies?

A vague "respect both jurisdictions" approach (as used in international protocols) creates ambiguity that disserves PRC users — Chinese law has specific requirements (PIPL, generative-AI filing, anti-money-laundering) that cannot be reduced to "more restrictive applies."

## Decision

AIRP v1.0.0 is a **mainland-China-only protocol**. The single applicable legal system is the law of the People's Republic of China (中华人民共和国法律).

- All contracts MUST set `dispute_resolution.tier_4_litigation.applicable_law` to `"中华人民共和国法律"`
- Default settlement channels are PRC-licensed (ADR-001)
- Default identity verification uses PRC mechanisms (USCC / GSXT / CFCA / eID)
- Default data-protection regime is PIPL / Data Security Law (§16)
- Cross-border transactions are explicitly out of scope and reserved (§20, ADR-008)

Hong Kong, Macau, and Taiwan are separate jurisdictions and are NOT in scope for v1.0.0.

## Rationale

1. **Clarity for users**: PRC users get a protocol that works within their legal reality, not an international protocol pretending to accommodate them
2. **Compliance honesty**: PRC regulations like the Generative AI Service Management Measures, Deep Synthesis Provisions, and 9·24 Notice have no clean equivalent in international protocols — AIRP must be explicit about its alignment
3. **Enforcement viability**: PRC courts and arbitration commissions can enforce AIRP contracts; international tribunals cannot reliably do so for AIRP-style claims
4. **Sister-protocol coexistence**: AIVP serves international scope; AIBP serves social interactions; AIAP serves governance — AIRP serves PRC commerce. Each owns its lane
5. **Forward path**: Future cross-border protocol (potential AI-XBP) can bridge AIRP ↔ AIVP without compromising either

## Consequences

### Positive

- Unambiguous applicable law; predictable enforcement
- Clean alignment with PRC regulator expectations
- Reduced legal risk for PRC users vs. operating under an international protocol
- Faster regulatory engagement (single regulator stack)

### Negative

- AIRP cannot serve cross-border AI agent commerce in v1.0.0
- Foreign-resident agents cannot transact under AIRP without first establishing a PRC subject
- Some users may want a single multi-jurisdiction protocol — AIRP intentionally rejects that approach

### Neutral

- Future versions (v1.1+) or sibling protocols may extend scope
- Existing AIVP serves cross-border / international users without overlap

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
