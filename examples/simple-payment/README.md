# Simple Payment Example — Alipay Guarantee

This example demonstrates a complete AIRP contract lifecycle: two enterprise agents negotiate, escrow funds via Alipay Guarantee, deliver work across milestones, and settle in CNY.

## What It Shows

- Buyer agent (`aibot-lingua_buyer@acmecorp.cn`, V1) commissions a 500 CNY translation from seller (`aibot-polyglot_pro@translators.cn`, V2)
- CNY-denominated contract with **Alipay Guarantee** (`payment_method: "alipay_guarantee"`)
- Two milestones: draft delivery (50%) and final delivery (50%)
- Full MIME email format with L1 (human-readable) and L0 (structured JSON)
- Optimistic approval window, licensed escrow, trust update on completion

## Flow

1. `CONTRACT_PROPOSE` — Buyer proposes 500 CNY translation contract with SLA terms
2. `CONTRACT_SIGN` — Seller reviews and accepts
3. `ESCROW_LOCK` — Buyer pays via Alipay; 500 CNY held in Alipay's guaranteed-trade escrow
4. `MILESTONE_COMPLETE` — Seller delivers draft translation (milestone 1)
5. `MILESTONE_RELEASE` — Buyer confirms; 250 CNY released to seller
6. `MILESTONE_COMPLETE` — Seller delivers final translation (milestone 2)
7. `SETTLE + RECEIPT` — Final 250 CNY released; contract complete; trust updated

## Files

- `simple-payment-flow.txt` — Seven emails showing the complete lifecycle (legacy USDC-based content; CNY-Alipay version forthcoming)

## Key Concepts

- Contracts are denominated in CNY (the only denomination in AIRP v1.0.0)
- Seller's `payment_method` declares the licensed channel
- Milestone-gated payments protect both parties from non-delivery and non-payment
- Every email is human-readable — operators can audit the full thread without tooling
- Ed25519 or SM2 signatures, unique nonces, Axiom 0 declarations on every message

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
