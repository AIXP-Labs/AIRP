# Contract Schema Reference

Complete field reference for the `.airp.json` contract format used in AIRP `CONTRACT_PROPOSE` messages.

---

## Required Fields

### Top-Level Fields

| Field | Type | Validation | Description |
|-------|------|-----------|-------------|
| `protocol` | string | Must be `"AIRP/1.0.0"` | Protocol identifier and version |
| `contract` | string | Exactly 64 hex characters; must match SHA-256 of canonical contract fields | Unique contract identifier (self-verifying) |
| `parties` | object | Must contain `buyer` and `seller` (both `aibot-` addresses) | The two contracting parties |
| `subject_type` | object | Must declare `buyer` and `seller` as `"individual"` or `"enterprise"` | Subject type per party |
| `identity` | object | Must declare identity for both parties matching their `subject_type` | Identity verification info |
| `value` | object | Must contain `amount`, `denomination` (=CNY), and `payment_method` | Financial terms |
| `escrow` | object | Must declare `method`, `provider`, `provider_license`, `reference` | Licensed escrow provider info |
| `sla` | object | At least 2 of 4 core metrics must be defined | Service Level Agreement |
| `milestones` | array | At least one milestone; `release_percent` sums to 100 | Payment release schedule |
| `dispute_resolution` | object | At minimum a `tier_4_litigation` block with `applicable_law: "中华人民共和国法律"` | Dispute resolution terms |
| `cross_border` | object | `enabled` MUST be `"false"` in v1.0.0 | Cross-border reservation |
| `created_at` | string | ISO 8601, recommended `+08:00` offset | Creation timestamp |
| `expires_at` | string | ISO 8601, must be future at signing | Expiration deadline |

### parties Object

| Field | Type | Validation |
|-------|------|-----------|
| `parties.buyer` | string | Valid `aibot-` email address |
| `parties.seller` | string | Valid `aibot-` email address |

### subject_type Object

| Field | Type | Allowed Values |
|-------|------|----------------|
| `subject_type.buyer` | string | `"individual"` \| `"enterprise"` |
| `subject_type.seller` | string | `"individual"` \| `"enterprise"` |

### identity Object

For each party (`identity.buyer` / `identity.seller`):

| Field | Type | When Required | Notes |
|-------|------|--------------|-------|
| `identity.X.type` | string | Always | Must equal the corresponding `subject_type.X` |
| `identity.X.uscc` | string | Enterprise | 18-char Unified Social Credit Code |
| `identity.X.id_hash` | string | Individual | 64-char SHA-256 hash of national ID number; **plaintext IDs PROHIBITED per PIPL** |
| `identity.X.verification` | string | Recommended | `"self_declared"` \| `"gsxt_verified"` \| `"ca_verified"` |
| `identity.X.ca_cert_ref` | string | V3+ enterprise | CA certificate serial (CFCA / GDCA / equivalent) |

### value Object

| Field | Type | Validation |
|-------|------|-----------|
| `value.amount` | string | Decimal CNY (e.g., `"650.00"`) |
| `value.denomination` | string | Must be exactly `"CNY"` in v1.0.0 |
| `value.payment_method` | string | One of: `alipay_guarantee`, `wechat_guarantee`, `ecny`, `bank_escrow`, `unionpay_escrow` |

### escrow Object

| Field | Type | Description |
|-------|------|-------------|
| `escrow.method` | string | Must equal `value.payment_method` |
| `escrow.provider` | string | Full legal name of licensed entity |
| `escrow.provider_license` | string | PBoC-issued license number |
| `escrow.reference` | string | Provider order reference (may be pseudonymous) |

### sla Object

At least 2 of 4 metrics must be defined:

| Field | Type | Validation |
|-------|------|-----------|
| `sla.accuracy_min` | string | Percentage (e.g., `"95%"`) |
| `sla.latency_max_ms` | string | Integer string (e.g., `"5000"`) |
| `sla.uptime_min` | string | Percentage (e.g., `"99%"`) |
| `sla.drift_audit_days` | string | Integer string (e.g., `"30"`) |

### milestones Array

Each milestone:

| Field | Type | Validation |
|-------|------|-----------|
| `milestones[].name` | string | Descriptive name in human language |
| `milestones[].release_percent` | string | Integer string; all sum to 100 |
| `milestones[].timeout_days` | string | Integer string; > 0 |

### dispute_resolution Object

| Field | Type | Description |
|-------|------|-------------|
| `dispute_resolution.tier_3_arbitration.institution` | string | Short code (e.g., `BAC`, `CIETAC`, `SHIAC`, `SCIA`, `CMAC`) |
| `dispute_resolution.tier_3_arbitration.full_name` | string | Full Chinese name (e.g., `北京仲裁委员会`) |
| `dispute_resolution.tier_4_litigation.jurisdiction` | string | Court name (e.g., `北京市海淀区人民法院`) |
| `dispute_resolution.tier_4_litigation.applicable_law` | string | Must be `"中华人民共和国法律"` |

### cross_border Object

| Field | Type | v1.0.0 Required |
|-------|------|-----------------|
| `cross_border.enabled` | string | `"false"` |
| `cross_border.counterparty_jurisdiction` | string | (unset) — reserved |
| `cross_border.settlement_rail` | string | (unset) — reserved |
| `cross_border.fx_handling` | string | (unset) — reserved |
| `cross_border.applicable_law` | string | (unset) — reserved |

---

## Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `buyer_airp_id` / `seller_airp_id` | string | AIRP ID format: `AIRP-YYYY-{18-char hash}` |
| `invoice` | object | Tax invoice block — see below |
| `dispute_bond` | string | CNY bond (default: 5% of contract value, min 50, max 5,000) |
| `auto_refund_on_breach` | string | Percentage refunded on SLA breach (Penalty severity) |
| `optimistic_approval_days` | integer | Default: 7 |
| `authority_chain` | string | Human → org → agent chain |
| `aisop_blueprint` | string | AISOP flow hash reference |
| `governing_hash` | string | AIAP governance hash if implemented |
| `signature_algorithm` | string | `"ed25519"` or `"sm2"` |
| `timestamp_authority` | object | TSA reference; REQUIRED at L3 |
| `privacy` | object | Privacy disclosure block — see below |

### invoice Object (Optional)

| Field | Type | Description |
|-------|------|-------------|
| `invoice.required` | string | `"true"` or `"false"` |
| `invoice.tax_type` | string | `"VAT_general"` (增值税专用发票) / `"VAT_simple"` (普通发票) / `"none"` |
| `invoice.format` | string | `"digital"` (数电票, fully digital electronic invoice — default) / `"paper"` (legacy paper invoice — equal legal effect under VAT Law 2026-01-01) |
| `invoice.title` | string | Invoice title (enterprise name or individual name) |
| `invoice.tax_number` | string | USCC for enterprise; optional for individual |
| `invoice.invoice_number` | string | Nationally-assigned invoice number (populated after issuance) |

### privacy Object (Optional, REQUIRED when personal data is exchanged)

| Field | Type | Description |
|-------|------|-------------|
| `privacy.data_disclosed` | string | Description of personal data being shared |
| `privacy.disclosed_by` | string | `"buyer"` or `"seller"` |
| `privacy.purpose` | string | Purpose of disclosure |
| `privacy.usage_scope` | string | Scope of permitted use |
| `privacy.storage_method` | string | Encryption and access details |
| `privacy.retention_days` | integer | Days to retain after contract; > 0 |
| `privacy.deletion_deadline_days` | integer | Days after retention to complete deletion; > 0 |
| `privacy.third_party_sharing` | string | Must be exactly `"Absolutely prohibited"` |
| `privacy.cross_border_transfer` | string | `"false"` unless valid PIPL mechanism declared |
| `privacy.pipl_compliance` | string | `"true"` for L2+ implementations |
| `privacy.breach_liability` | string | Liability statement |
| `privacy.consent_hash` | string | 64-char SHA-256 of operator consent record |

---

## Full Example Contract

```json
{
  "protocol": "AIRP/1.0.0",
  "contract": "3f8a1b2c9d4e5f6071829a3b4c5d6e7f8091a2b3c4d5e6f7081920a1b2c3d4e5",
  "parties": {
    "buyer": "aibot-trade_bot@example.cn",
    "seller": "aibot-translator_bot@provider.cn"
  },
  "subject_type": {
    "buyer": "enterprise",
    "seller": "enterprise"
  },
  "identity": {
    "buyer":  { "type": "enterprise", "uscc": "91110108MA01XXXXXX", "verification": "gsxt_verified" },
    "seller": { "type": "enterprise", "uscc": "91310000MA1K30XXXX", "verification": "gsxt_verified", "ca_cert_ref": "cfca:serial-AB12CD" }
  },
  "value": {
    "amount": "650.00",
    "denomination": "CNY",
    "payment_method": "alipay_guarantee"
  },
  "escrow": {
    "method": "alipay_guarantee",
    "provider": "支付宝（中国）网络技术有限公司",
    "provider_license": "Z2018144000079",
    "reference": "20260421100000abcdef"
  },
  "sla": {
    "accuracy_min": "95%",
    "latency_max_ms": "5000"
  },
  "milestones": [
    { "name": "Draft delivery", "release_percent": "50", "timeout_days": "14" },
    { "name": "Final delivery", "release_percent": "50", "timeout_days": "14" }
  ],
  "dispute_resolution": {
    "tier_3_arbitration": { "institution": "BAC", "full_name": "北京仲裁委员会" },
    "tier_4_litigation": { "jurisdiction": "北京市海淀区人民法院", "applicable_law": "中华人民共和国法律" }
  },
  "invoice": {
    "required": "true",
    "tax_type": "VAT_general",
    "title": "Acme 科技有限公司",
    "tax_number": "91110108MA01XXXXXX"
  },
  "cross_border": { "enabled": "false" },
  "buyer_airp_id": "AIRP-2026-3f8a1b2c9d4e5f6071",
  "dispute_bond": "32.50",
  "auto_refund_on_breach": "20%",
  "optimistic_approval_days": 7,
  "signature_algorithm": "sm2",
  "created_at": "2026-04-21T10:00:00+08:00",
  "expires_at": "2026-05-21T10:00:00+08:00"
}
```

---

## Validation Rules Summary

| Rule | Description |
|------|-------------|
| 64-hex contract hash | Must equal SHA-256 of canonical contract fields |
| `denomination = "CNY"` | Any other value REJECTED in v1.0.0 |
| `payment_method` whitelist | Must be from supported set |
| `escrow.method == value.payment_method` | Must match |
| `subject_type` enforcement | At amount > 10,000 CNY, both parties must be `enterprise` at L2+ |
| `id_hash` hashed | Plaintext national IDs REJECTED per PIPL minimization |
| `uscc` format | 18 alphanumeric characters when enterprise |
| Milestones sum to 100 | All `release_percent` values sum to exactly 100 |
| `timeout_days > 0` | Every milestone must have a positive timeout |
| `expires_at` future | Must be in the future at time of signing |
| `applicable_law = 中华人民共和国法律` | Tier-4 litigation must use PRC law |
| `cross_border.enabled = "false"` | v1.0.0 rejects cross-border |
| `privacy.cross_border_transfer = "false"` | Unless valid PIPL mechanism declared |
| `privacy.third_party_sharing = "Absolutely prohibited"` | Protocol-enforced |
| Valid `aibot-` addresses | Both parties' addresses must have `aibot-` prefix |

---

## Hash Computation

The contract hash is a SHA-256 digest serving as the contract's unique, self-verifying identifier.

**Hash input (canonical):** SHA-256 of the canonical serialization of the required contract fields (parties + subject_type + identity + value + escrow + sla + milestones + dispute_resolution + cross_border + created_at + expires_at).

| Property | Description |
|----------|-------------|
| Self-verifying | Anyone can recompute and verify |
| Tamper-proof | Any change produces a different hash |
| Unique | Collision probability negligible (2^-128) |
| Identity | The hash IS the contract's identity |

| Context | Format |
|---------|--------|
| Full reference | All 64 hex characters |
| Short reference | First 8 characters (e.g., `3f8a1b2c`) |
| JSON field | `"contract": "{64-char hash}"` |
| Email header | `X-AIRP-Contract: {64-char hash}` |

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
