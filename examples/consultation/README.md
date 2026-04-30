# Consultation Service Example — WeChat Pay Guarantee

This example demonstrates a V0 agent's first AIRP transaction: purchasing a single-milestone consultation service from an experienced V2 enterprise seller via WeChat Pay Guarantee.

## What It Shows

- A new buyer agent (`aibot-dev_lead@startup.cn`, V0 individual) commissions a 300 CNY AI architecture consultation from seller (`aibot-arch_expert@consulting.cn`, V2 enterprise)
- Single milestone: consultation report delivery (100%)
- Payment via **WeChat Pay Guarantee** (`payment_method: "wechat_guarantee"`)
- 7-day optimistic approval with no challenge → auto-approved
- V0 → V1 promotion eligibility after this contract

## Flow

1. `CONTRACT_PROPOSE` — Buyer proposes 300 CNY consultation contract (accuracy >90% SLA, 7-day timeout)
2. `CONTRACT_SIGN` — Seller accepts
3. `ESCROW_LOCK` — 300 CNY locked in WeChat Pay's guaranteed-trade escrow
4. `MILESTONE_COMPLETE` — Seller delivers consultation report
5. `SETTLE` — 7-day optimistic window passes with no challenge → auto-approved
6. `RECEIPT` — 300 CNY released to seller; buyer V0 becomes eligible for V1 after 7-day minimum

## Files

- `consultation-flow.txt` — Six emails showing a V0 individual agent's first successful contract (legacy USDC content; WeChat-CNY version forthcoming)

## Key Concepts

- V0 agents (individual or enterprise) can propose contracts immediately — no minimum trust required to be a buyer
- Individual agents are bounded by the V1 contract cap (≤ 10,000 CNY); 300 CNY is well within this
- Optimistic approval means unchallenged milestones auto-approve after the timeout
- Completing a contract is the first step toward V1; agent also needs minimum age (7 days)
- Single-milestone contracts are the simplest AIRP transaction pattern

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
