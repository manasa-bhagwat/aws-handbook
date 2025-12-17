---
title: Architecture
parent: IAM Policies
nav_order: 1
---
# IAM Usage Basics
--- 

## Purpose

This policy defines baseline rules for using AWS Identity and Access Management (IAM) to ensure consistent, secure, and maintainable access control within an AWS account.

The policy aims to reduce misconfiguration risk and operational overhead.

---

## Scope

This policy applies to:

- All IAM users
- All IAM roles
- All AWS services operating within the account

This policy does not cover organization-level governance.

---

## Policy Statements

### 1. User Access Management

- IAM users **MUST** be assigned permissions through IAM groups.
- Policies **MUST NOT** be attached directly to individual IAM users.

**Rationale:**

Group-based permission management ensures consistency and simplifies access reviews.

---

### 2. Service and Application Access

- AWS services and applications **MUST** use IAM roles for access.
- Long-lived access keys **MUST NOT** be used by applications or workloads.

**Rationale:**

IAM roles provide temporary credentials and reduce exposure of permanent secrets.

---

### 3. Credential Handling

- Access keys **MUST NOT** be embedded in source code, configuration files, or images.
- Access keys **MUST** be rotated or removed when no longer required.

**Rationale:**

Static credentials increase the risk of unintended disclosure.

---

### 4. Administrative Access

- Administrative permissions **SHOULD** be limited to a minimal set of users.
- Broad administrative policies **SHOULD NOT** be assigned for routine tasks.

**Rationale:**

Limiting administrative access reduces blast radius in case of misuse or compromise.

---

### 5. Multi-Factor Authentication (MFA)

- MFA **SHOULD** be enabled for all human IAM users.
- MFA **MUST** be enabled for users with administrative permissions.

**Rationale:**

MFA adds an additional control layer for sensitive operations.

---

## Compliance and Enforcement

Compliance with this policy may be enforced through:

- IAM permission reviews
- Access audits
- Automated checks in CI/CD pipelines

Non-compliant configurations should be remediated promptly.

---

## Exceptions

Exceptions to this policy:

- **MUST** be documented
- **MUST** include justification
- **SHOULD** be time-bound where possible

Example structure:

```yaml
Exception:
- Policy: IAM Usage Basics
- Reason: Legacy tool requires static credentials
- Owner: Platform team
- Review date: YYYY-MM-DD
```

---

## Review and Maintenance

- This policy **SHOULD** be reviewed periodically
- Updates **MUST** reflect changes in access patterns or security requirements

---

## Scope Note

This policy intentionally excludes:

- Service Control Policies (SCPs)
- Permission boundaries
- Federation and external identity providers

---
