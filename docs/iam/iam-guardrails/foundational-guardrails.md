---
title: Foundational Guardrails
parent: IAM Guardrails
nav_order: 1
---

# Foundational Guardrails
---

## Purpose

These guardrails define **mandatory boundaries** for using AWS Identity and Access Management (IAM) safely and consistently.

They exist to prevent:

- Uncontrolled privilege escalation
- Credential sprawl
- Inconsistent access models
- Difficult-to-audit permission assignments

---

## Scope

These guardrails apply to:

- All IAM users
- All IAM roles
- All AWS services and applications within the account

They apply across:

- Development
- Staging
- Production environments

---

## Mandatory Guardrails (MUST)

The following rules are **non-negotiable**:

- IAM users **MUST** receive permissions through IAM groups.
- AWS services and applications **MUST** use IAM roles.
- Long-lived access keys **MUST NOT** be used by applications.
- Each IAM role **MUST** have a clearly defined purpose.
- Administrative permissions **MUST** be limited to explicitly approved users.

---

## Recommended Guardrails (SHOULD)

The following practices are strongly encouraged:

- MFA **SHOULD** be enabled for all human IAM users.
- IAM roles **SHOULD** be scoped to a single service or workload.
- AWS-managed policies **SHOULD** be preferred over custom policies at this level.
- IAM permissions **SHOULD** be reviewed periodically.

---

## Prohibited Patterns (MUST NOT)

The following patterns are explicitly disallowed:

- IAM users **MUST NOT** be used by applications or workloads.
- Access keys **MUST NOT** be embedded in source code or images.
- Broad administrative policies **MUST NOT** be used for routine tasks.
- Permissions **MUST NOT** be granted without a clear access requirement.

---

## Enforcement Mechanisms

These guardrails may be enforced through:

- IAM policy reviews
- Access audits
- CI/CD checks for credential usage
- Infrastructure-as-code validations
- Code review checklists

Advanced enforcement mechanisms (SCPs, permission boundaries) are intentionally out of scope at this level.


**Example Compliant pattern:**

- EC2 instance assumes an IAM role
- Role has AWS-managed S3 read-only policy
- No access keys stored on the instance

This provides temporary, auditable access aligned with AWS best practices.


**Example Non-compliant pattern:**

- Application uses hardcoded IAM user access keys
- User has broad permissions
- No clear ownership or rotation strategy

**Risk:**

- Credential leakage
- Unbounded access
- Difficult audit and revocation

---

## Exceptions Process

Exceptions to these guardrails:

- **MUST** be documented
- **MUST** include justification
- **SHOULD** be time-bound where possible
- **MUST** be approved by the owning team

---

## Version History

- v1.0 — Initial IAM guardrails defined