# ADR-002: Single CNY Denomination

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

AIRP needs a pricing denomination for contracts. The protocol scope is mainland-China commerce.

Key considerations:
- Multi-currency denomination introduces FX mechanisms, oracles, and complexity that mainland-China commerce does not need
- Cross-border transactions are explicitly out of scope for v1.0.0 (see §20)
- Tax invoicing in China is CNY-only per PRC tax law
- Bank settlement, e-CNY, Alipay, WeChat Pay all settle in CNY natively
- Forward compatibility is required for future cross-border versions

Candidates considered: CNY-only with reserved field, multi-currency from day one, custom unit.

## Decision

AIRP v1.0.0 supports a **single denomination: CNY (Renminbi)**.

- `value.denomination` MUST be exactly `"CNY"` in v1.0.0
- The field is typed as a string enumeration (not a fixed value) to permit future expansion
- Implementations MUST reject contracts with any other denomination
- Cross-border denominations (HKD, USD, EUR, etc.) are reserved for §20 cross-border future scope

## Rationale

1. **Scope alignment**: Mainland-China commerce is CNY-native
2. **No FX complexity**: Eliminates oracles, slippage, depeg risk
3. **Tax-aligned**: Matches PRC VAT invoice requirements
4. **Settlement-aligned**: All three supported channels (Alipay/WeChat/e-CNY) settle in CNY
5. **Simplest correct**: Avoids over-engineering for unsupported use cases
6. **Forward-compatible**: String enum allows v1.1+ to add HKD or other currencies without breaking schema

## Consequences

### Positive

- Maximally simple value model
- No oracle dependency
- No depeg or FX risk
- Direct mapping to all PRC settlement channels
- No conflict with PRC FX administration rules

### Negative

- Cannot serve cross-border commerce in v1.0.0 (intentional)
- Foreign-resident buyers/sellers cannot transact under v1.0.0 (intentional)
- Hong Kong / Macau / Taiwan separate jurisdictions are out of scope (intentional)

### Neutral

- Future versions or sibling protocols (AI-XBP) may extend the denomination set
- AIVP serves international/offshore commerce as a parallel protocol

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
