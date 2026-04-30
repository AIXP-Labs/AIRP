# Governance

This document describes the governance model for the AIRP (AI RMB Protocol) project.

## Principles

1. **Open Governance** — All governance decisions are made transparently and publicly
2. **Axiom 0 Supremacy** — No governance decision may weaken, modify, or deprecate Axiom 0: Human Sovereignty and Wellbeing
3. **Dignity Standard** — All governance discussions must adhere to the Dignity Standard
4. **Consensus-Seeking** — Decisions are reached through discussion and consensus; voting is a last resort

## Decision-Making

### Specification Changes

Changes to normative protocol content (anything in `specification/`) follow this process:

1. **Proposal** — Open a GitHub Issue with the `spec-change` label
2. **Discussion Period** — Minimum 14 days for non-trivial changes
3. **ADR** — Significant architectural decisions require an Architecture Decision Record in `adrs/`
4. **Axiom 0 Review** — All changes must pass Axiom 0 compliance review by maintainers
5. **Approval** — Requires approval from at least 2 maintainers
6. **Merge** — Changes are merged to `main` with both EN and CN versions updated simultaneously

### Immutable Constraints

The following aspects of AIRP are **immutable** and cannot be changed through governance:

- **Axiom 0**: Human Sovereignty and Wellbeing — independently established, non-negotiable
- **Human language requirement**: All L0 and L1 content must be in human language
- **Email-based transport**: The `aibot-` prefix addressing system
- **Operator override**: Human ability to freeze/cancel any transaction at any time
- **Dignity Standard**: The prohibition on deceptive and manipulative commercial behavior

### Documentation Changes

Non-normative changes (guides, topics, examples) follow a lighter process:

1. Open a pull request
2. Approval from at least 1 maintainer
3. Merge

## Roles

| Role | Responsibilities | Selection |
|------|-----------------|-----------|
| **Maintainer** | Review PRs, enforce Axiom 0, manage releases | Nominated by existing maintainers, consensus approval |
| **Contributor** | Submit PRs, participate in discussions | Self-selected, must agree to Code of Conduct |
| **Reviewer** | Provide expert review on specification changes | Invited by maintainers based on domain expertise |

## Conflict Resolution

1. Technical disagreements are resolved through discussion on GitHub Issues
2. If consensus cannot be reached, maintainers vote (simple majority)
3. Axiom 0 compliance disputes are escalated to the full maintainer group (unanimous required to override)
4. If a decision is perceived to violate Axiom 0, any maintainer may invoke a mandatory review period

## Versioning

AIRP follows [Semantic Versioning](https://semver.org/):

- **Major**: Breaking changes (new required fields, trust level restructuring)
- **Minor**: Backward-compatible additions (new optional message types, new payment channel methods, new optional fields)
- **Patch**: Clarifications, typo fixes, documentation improvements

---

Align Axiom 0: Human Sovereignty and Wellbeing. Version: AIRP V1.0.0. www.airp.dev
