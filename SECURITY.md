# Security Policy

## Reporting a Vulnerability

AIRP is a protocol specification, not a software implementation. However, vulnerabilities in the protocol design itself — such as mechanisms that could be exploited to bypass Axiom 0, enable contract fraud, compromise Escrow Account security, or manipulate AIRP Trust scores — are taken seriously.

### How to Report

- **GitHub**: Open a [Security Advisory](https://github.com/AIXP-Labs/AIRP/security/advisories/new) (private)
- **Title**: `[AIRP-SECURITY] Brief description`
- **Include**: Affected protocol section, attack scenario, potential impact

### Response Timeline

| Action | Timeline |
|--------|----------|
| Acknowledgment | Within 48 hours |
| Initial assessment | Within 7 days |
| Resolution plan | Within 30 days |
| Public disclosure | After fix is published, or 90 days (whichever is sooner) |

### Scope

The following are in scope for security reports:

- Protocol design flaws that could enable Axiom 0 violations
- Contract fraud or manipulation vectors (e.g., hash collision attacks)
- AIRP Trust level escalation bypasses or Sybil attack vectors
- Escrow protocol-level vulnerabilities (timeout bypass, unauthorized milestone release, custodial agreement enforcement gaps)
- Identity spoofing or impersonation via email (USCC misrepresentation, signature forgery)
- Dispute resolution manipulation (arbitration evasion, court-jurisdiction circumvention)
- Privacy boundary circumvention (PIPL violations, cross-border transfer evasion)
- Dignity Standard enforcement gaps
- TSA-CN trusted-timestamp evidence weakening

### Out of Scope

- Vulnerabilities in specific AIRP implementations (report to the implementation maintainer)
- General email security issues (SPF/DKIM/DMARC) — these are upstream concerns
- Provider operational disruption (Alipay, WeChat Pay, e-CNY service availability) — report to the licensed provider
- Social engineering attacks that don't exploit protocol mechanisms
- Bugs in a specific licensed-provider integration (report to the integration maintainer)
- Tax / accounting issues with VAT invoice handling — outside protocol scope

## Responsible Disclosure

We follow responsible disclosure principles. Please do not publicly disclose security issues before they have been addressed. We will credit reporters in the CHANGELOG unless they prefer anonymity.

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
