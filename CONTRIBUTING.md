# Contributing to AIRP

Thank you for your interest in contributing to the AI RMB Protocol! This document provides guidelines for contributing to the project.

> ⚠️ **Contribution Status (Current Stage)**
>
> We welcome **discussion through GitHub Issues** at this stage of development.
>
> **External Pull Requests are not currently accepted.** If you have a proposal — bug report, feature idea, specification clarification, or example suggestion — please open an issue describing it. If we agree it adds value, maintainers will implement it and credit you.
>
> This policy may be revisited in the future.

> **Stage Status (v1.0.0)**
>
> AIRP is at early specification stage. The processes below describe the *target* governance model. Initial decisions are made by AIXP Labs core maintainers; community discussion period scales as the contributor base grows.

## How to Contribute

### Reporting Issues

- Use [GitHub Issues](https://github.com/AIXP-Labs/AIRP/issues) to report bugs, suggest features, or propose specification changes
- For specification changes, use the `spec-change` issue template
- Provide clear descriptions with examples where possible

### Discussion-Driven Development

Instead of submitting PRs directly:

1. **Open an issue** describing your proposal, bug, or idea
2. **Discuss** with maintainers — clarify scope, design, and approach
3. **Wait for review** — significant proposals follow the [Specification Changes](#specification-changes) process below
4. **If accepted**, maintainers will implement the change and credit you in commit/release notes

### Specification Changes

Proposals affecting normative content (anything in `specification/`) follow this process:

1. An issue with the `spec-change` label describing the proposed change
2. A minimum 14-day discussion period for non-trivial changes (target governance model; current discussion windows scale with contributor count)
3. An Architecture Decision Record (ADR) in `adrs/` for significant decisions
4. Axiom 0 compliance review by maintainers
5. PRC regulatory compliance review (PBOC / SAFE / CAC / CSRC alignment)
6. Updated documentation reflecting the change
7. **Both EN and CN versions must be updated simultaneously**

### Documentation Changes

Suggestions for non-normative content (guides, topics, reference, examples) are welcome via issues — typo fixes, clarifications, additional examples are particularly valued. Maintainers will implement accepted suggestions, ensuring alignment with Axiom 0 and PRC regulatory requirements.

## Guidelines

### Writing Style

- Use clear, concise language
- Follow the existing document structure and formatting
- All content values must be in human language (no opaque codes or machine-only tokens)
- Both English and Chinese versions are first-class; the default README is Chinese (`README.md`) and the English version is `README_EN.md`. Both must be kept in sync.

### Axiom 0 Compliance

Every contribution must comply with Axiom 0: Human Sovereignty and Wellbeing. Specifically:

- Changes must not weaken human oversight of AI commercial interactions
- Changes must not enable AI agents to circumvent transparency requirements
- Changes must not compromise the Dignity Standard
- Changes must preserve dual-signature requirements for human-authorized commercial actions

### Commit Message Format

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

Types: `feat`, `fix`, `docs`, `spec`, `refactor`, `test`, `chore`

Examples:
- `spec(trust): add V4 Premier trust level stake requirements`
- `docs(guide): add getting started guide for contract creation`
- `fix(spec): correct CONTRACT_PROPOSE message format example`

### Bilingual Requirements

For specification changes:
- Chinese version (`specification/AIRP_Protocol_cn.md`) and English version (`specification/AIRP_Protocol.md`) must be updated in the same PR
- Axiom 0 in Chinese: "人类主权与福祉" (never abbreviated)
- Maintain consistent terminology — refer to `docs/reference/glossary.md`

## Writing Guidelines

### RFC 2119 Keywords

When writing normative specification text, use the keywords defined in [RFC 2119](https://tools.ietf.org/html/rfc2119):

- **MUST** / **MUST NOT** — Absolute requirements
- **SHOULD** / **SHOULD NOT** — Strong recommendations with documented exceptions
- **MAY** — Truly optional behavior

These keywords MUST be capitalized when used in their normative sense.

### Terminology

- Use "AIRP agent" for governed AI commercial agents
- Use "Trust Level V0–V4" with capitalized V prefix (V0 Stranger, V4 Premier — note: V for Value/Verified, not T)
- Capitalize "Axiom 0", "Dignity Standard" (proper nouns)
- Currency: write "CNY" (ISO 4217) or "人民币"; never abbreviate as "RMB" in normative text
- Settlement channels: "Alipay 担保交易", "WeChat Pay 担保交易", "数字人民币 (e-CNY)" — preserve official names
- Regulatory references: PBOC (中国人民银行), SAFE (国家外汇管理局), CAC (国家互联网信息办公室), CSRC (中国证券监督管理委员会)

### Document Structure

- Begin each topic document with a one-paragraph introduction
- Use tables for field specifications
- Use code blocks with language annotations for examples
- Use Mermaid diagrams or email transcripts for flow illustrations
- Cross-reference between documents using relative links

### Closing Seal

All specification documents MUST end with:

```
Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
```

## Development Setup

### Prerequisites

- Git
- Python 3.8+ (for MkDocs documentation site)
- MkDocs Material theme (`pip install mkdocs-material`)

### Building Documentation

```bash
# Install dependencies
pip install mkdocs-material

# Serve locally
mkdocs serve

# Build static site
mkdocs build
```

## Code of Conduct

All contributors must follow our [Code of Conduct](CODE_OF_CONDUCT.md). The Axiom 0 pledge applies to all contributions.

## License of Contributions

By submitting an issue or any other content (including specification proposals, code snippets in issues, or design suggestions), you agree that your submitted content may be used by maintainers under the terms of the [Apache License 2.0](LICENSE), the same license as the project.

## Questions?

- Open a [GitHub Discussion](https://github.com/AIXP-Labs/AIRP/discussions) for general questions
- For private inquiries, open a [Security Advisory](https://github.com/AIXP-Labs/AIRP/security/advisories/new)

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
