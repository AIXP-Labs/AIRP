> **Source of truth:** This document is mirrored for the documentation site. The authoritative version lives in [`/adrs/adr-007-dual-signature.md`](https://github.com/AIXP-Labs/AIRP/blob/main/adrs/adr-007-dual-signature.md). Edits MUST go to the authoritative file first.

# ADR-007: Dual Signature Support — Ed25519 and SM2

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

Every AIRP message and contract event requires a cryptographic signature for authentication and non-repudiation. The PRC regulatory environment has two distinct cryptographic ecosystems:

- **International-standard cryptography**: Ed25519 (RFC 8032), widely supported in open-source libraries, used by AIBP / AIVP / AISOP
- **Chinese national cryptographic standards (GuoMi, 国密)**: SM2 signature (GB/T 32918) and SM3 hash (GB/T 32905), promoted by the State Cryptography Administration (国家密码管理局), required or strongly preferred for state-owned enterprises, financial institutions, and government-related systems

**Regulatory drivers for SM2/SM3 in China**:
- **State Council Office Document [2018] No. 36** mandates national cryptographic algorithm adoption in finance and critical sectors
- **PBoC 3.0 IC Card Standard** (《中国金融集成电路(IC)卡规范》) adopted SM2 in 2011-03 to enhance financial card security
- **GB/T 39786-2021 密评** (Cryptographic Application Security Assessment) verifies proper SM2/SM3 deployment and has "veto power" in 2026 finance / SOE / government IT acceptance (see §17.3)

A protocol that supports only one creates friction:
- Ed25519-only: Excludes state-owned enterprises, financial institutions, and government-aligned counterparties (cannot pass 密评)
- SM2-only: Excludes the broader open-source / international developer base

## Decision

AIRP v1.0.0 supports **both Ed25519 and SM2/SM3** as equally valid signature algorithms.

- Sender chooses one algorithm per message
- Header format: `X-AIRP-Signature: ed25519:{base64}` OR `X-AIRP-Signature: sm2:{base64}`
- Receiving agents MUST support both algorithms (cannot reject solely on algorithm choice)
- The `signature_algorithm` field in the contract optionally declares the contract's preferred algorithm
- For SM2, the digest algorithm is SM3; for Ed25519, the digest is SHA-512 (per RFC 8032)
- Public keys are published via DNS TXT records or `.well-known/airp-pubkey.{algorithm}.pem`

## Rationale

1. **Inclusive ecosystem**: Both PRC enterprises and international/open-source developers can participate
2. **Regulatory readiness**: SM2/SM3 are required for procurement-track engagements with state-owned enterprises and many financial institutions; supporting them lowers integration barriers
3. **No cryptographic strength compromise**: Both algorithms provide equivalent security (~128-bit equivalent)
4. **Sender choice, receiver mandate**: Sender picks based on their stack; receiver MUST support both — preserves protocol interoperability
5. **Forward extension**: Adding future algorithms (e.g., post-quantum) follows the same pattern

## Consequences

### Positive

- Protocol is usable by both international developers and PRC-state ecosystem participants
- Reduces friction for procurement-track adoption (state-owned enterprises, banks, government-related agents)
- Future-proof: same pattern can add new algorithms
- L3 agents needing CFCA certificates (ADR-008-related) can use SM2 natively

### Negative

- All implementations MUST include both libraries (Ed25519 + SM2/SM3)
- SM2/SM3 libraries are less commonly bundled in mainstream ecosystems; integration cost is non-trivial
- More test surface (every interop test must cover both algorithms)

### Neutral

- Open-source libraries for SM2/SM3 exist (e.g., GmSSL, Bouncy Castle, gmssl-python)
- Some implementations may default to Ed25519 for simplicity; that is permitted but reduces SM2-counterparty interoperability surface

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
