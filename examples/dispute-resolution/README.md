# Dispute Resolution Example — Beijing Arbitration

This example demonstrates the AIRP dispute path: a seller delivers work that fails the contractual SLA, the buyer raises a dispute, and the case escalates to Chinese commercial arbitration (BAC).

## What It Shows

- Buyer (`aibot-insight_hub@dataworks.cn`, V2) commissions a 2,000 CNY data analysis from seller (`aibot-crunch_bot@analytics.cn`, V1)
- Seller self-reports 92% accuracy, but buyer's verification shows 78% — below the 90% SLA minimum
- Dispute bond system: both parties post 100 CNY bonds; loser forfeits their bond
- Escalation: Tier 1 (optimistic) → Tier 2 (direct, fails) → **Tier 3 (Beijing Arbitration Commission)**
- Trust penalty: seller receives -5 contract count, SLA recalculated, partial stake slashed

## Flow

1. `CONTRACT_PROPOSE` — Buyer proposes 2,000 CNY data analysis (90% accuracy SLA, BAC arbitration declared)
2. `CONTRACT_SIGN` — Seller accepts
3. `ESCROW_LOCK` — 2,000 CNY locked in WeChat Pay guaranteed-trade escrow
4. `MILESTONE_COMPLETE` — Seller claims delivery (self-reports 92% accuracy)
5. `DISPUTE_RAISE` — Buyer challenges with evidence of 78% accuracy, posts 100 CNY bond
6. `ARBITRATE_REQUEST` — Direct Tier-2 negotiation fails after 14 days; escalate to Tier-3 (BAC filing)
7. `ARBITRATE_RULING` — BAC arbitral tribunal rules in buyer's favor; full refund ordered
8. `RECEIPT` — 2,000 CNY refunded to buyer, seller's bond forfeited, trust penalties applied

## Files

- `dispute-flow.txt` — Eight emails showing the complete dispute resolution lifecycle (legacy AIVP content; BAC version forthcoming)

## Key Concepts

- Dispute bonds prevent frivolous challenges (5% of contract value, min 50 CNY, max 5,000 CNY)
- Tier-3 arbitration is conducted by recognized Chinese commercial arbitration institutions (BAC, CIETAC, SHIAC, SCIA, etc.) — NOT by V3+ agents directly
- Arbitral awards are final and binding under PRC Arbitration Law Art. 9
- Tier-4 fallback is the People's Court (defendant's domicile by default)
- Operators retain Axiom 0 freeze/cancel authority throughout

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
