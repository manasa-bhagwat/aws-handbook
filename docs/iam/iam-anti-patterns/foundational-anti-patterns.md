---
title: Foundational Anti Patterns
parent: IAM Anti Patterns
nav_order: 1
---

# Foundational Anti Patterns
---

## Overview

These anti-patterns describe **common IAM mistakes** that lead to security risks, operational friction, and long-term maintenance issues.

They are included to improve detection and prevention.

---

## 2. Anti-Pattern 1: Using IAM Users for Applications

### Description

Applications authenticate to AWS using IAM user access keys.

### Why It Happens

- Simplicity
- Lack of familiarity with IAM roles
- Legacy examples or tutorials

### Impact / Failure Modes

- Long-lived credential exposure
- Manual key rotation
- Increased blast radius

### Correct Pattern (Fix)

Use IAM roles with temporary credentials for all applications and services.

---

## 3. Anti-Pattern 2: Attaching Policies Directly to Users

### Description

Permissions are assigned directly to IAM users.

### Why It Happens

- Small team sizes
- Ad-hoc permission grants

### Impact / Failure Modes

- Inconsistent permissions
- Difficult access reviews
- Permission drift

### Correct Pattern (Fix)

Attach policies to IAM groups and manage user access through group membership.

---

## 4. Anti-Pattern 3: Granting Broad Administrative Access

### Description

Users are granted full administrative permissions for convenience.

### Why It Happens

- Urgency
- Lack of defined roles
- Absence of guardrails

### Impact / Failure Modes

- Accidental destructive actions
- High blast radius
- Audit and compliance issues

### Correct Pattern (Fix)

Grant scoped permissions aligned with specific responsibilities.

---

## 5. Detection

Anti-patterns can be identified through:

- IAM permission reviews
- CloudTrail logs showing unexpected actions
- Configuration audits
- Code reviews detecting embedded credentials

---

## 6. How to Prevent

- Apply IAM guardrails consistently
- Use standardized runbooks
- Prefer role-based access patterns
- Educate teams on IAM fundamentals
- Use templates for common access scenarios

---

## 7. References

- AWS IAM Documentation
- AWS Security Best Practices