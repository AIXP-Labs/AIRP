# Referral Service Example — Digital RMB (e-CNY)

This example demonstrates a multi-party referral flow with digital Renminbi settlement: a buyer pays a matchmaker agent (V3) to find and recommend a specialized data analysis agent.

## What It Shows

- Buyer agent (`aibot-project_mgr@corp.cn`, V1 enterprise) needs a data analysis agent
- Matchmaker agent (`aibot-matchmaker@network.cn`, V3 enterprise) provides agent matching as a paid service
- Recommended agent (`aibot-data_guru@analytics.cn`) is introduced and later confirmed
- 200 CNY contract with 2 milestones: recommend candidates (50%) + buyer confirms match (50%)
- Settlement via **digital RMB** (`payment_method: "ecny"`) using PBoC's DC/EP conditional payment

## Flow

1. `CONTRACT_PROPOSE` — Buyer proposes 200 CNY referral contract (accuracy >85% SLA)
2. `CONTRACT_SIGN` — Matchmaker accepts
3. `ESCROW_LOCK` — Buyer's e-CNY wallet executes a conditional transfer to matchmaker; PBoC DC/EP enforces conditions
4. `MILESTONE_COMPLETE` — Matchmaker recommends 3 candidate agents (including data_guru)
5. `MILESTONE_RELEASE` — Buyer confirms; 100 CNY e-CNY released
6. `MILESTONE_COMPLETE` — Buyer confirms signed separate contract with data_guru
7. `SETTLE + RECEIPT` — Final 100 CNY released; contract complete

## Files

- `referral-flow.txt` — Seven emails showing the complete referral service lifecycle (legacy AIVP content; e-CNY version forthcoming)

## Key Concepts

- Agent discovery and matching is itself a commercial service within the AIRP economy
- V3 agents (Trusted) have the reputation history to serve as reliable brokers
- Second milestone is buyer-confirmed, ensuring the referral led to a working relationship
- The introduced agent (data_guru) is not a party to this contract — they transact separately with the buyer
- e-CNY enables programmable conditional payment without third-party escrow

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
