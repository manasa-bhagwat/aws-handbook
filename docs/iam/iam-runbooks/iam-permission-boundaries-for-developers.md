---
title: Permission Boundaries for Developers
parent: IAM Runbooks
nav_order: 1
---

# Permission Boundaries for Developers
---

## Purpose

Prevent **privilege escalation** by developers while still allowing them to create and manage IAM roles within a controlled blast radius.

This runbook enforces a hard ceiling on permissions using **IAM Permission Boundaries**.

---

## When to Use

* Developers are allowed to create or modify IAM roles
* Platform teams want self-service without admin risk
* Audit finding: *Potential privilege escalation via IAM*
* Shared or multi-team AWS accounts

---

## Scope

* Applies to IAM users or roles used by developers
* Applies to role creation and modification actions
* Does **not** replace least-privilege policies; it constrains them

---

## Preconditions

* Administrative access to IAM
* Clear definition of maximum allowed developer permissions
* Agreement on what developers must **never** be able to do

---

## Design Principle (Non-Negotiable)

> A permission boundary defines the **maximum permissions** an identity can ever have, regardless of what permissions it tries to attach.

Even if a developer attaches `AdministratorAccess`, the boundary still applies.

---

## Step 1 — Define the Permission Boundary Policy

Create a managed policy that represents the **absolute upper limit** of developer permissions.

### Example: Developer Permission Boundary

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:*",
        "s3:*",
        "logs:*",
        "cloudwatch:*"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Deny",
      "Action": [
        "iam:*",
        "organizations:*",
        "account:*"
      ],
      "Resource": "*"
    }
  ]
}
```

**Key Properties**

* Explicit deny for IAM and account-level services
* Allows service usage but blocks identity control

Save as: `DeveloperPermissionBoundary`

---

## Step 2 — Attach Boundary to Developer Identity

Attach the permission boundary to:

* Developer IAM role (recommended)
* Or developer IAM users (legacy setups)

### Important

The boundary must be attached **at identity creation time** or enforced via process.

---

## Step 3 — Allow Developers to Create Roles (Safely)

Attach an IAM policy to the developer identity allowing role creation **only when the boundary is applied**.

### Example Condition-Enforced Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iam:CreateRole",
        "iam:AttachRolePolicy",
        "iam:PutRolePolicy"
      ],
      "Resource": "arn:aws:iam::*:role/dev-*",
      "Condition": {
        "StringEquals": {
          "iam:PermissionsBoundary": "arn:aws:iam::<account-id>:policy/DeveloperPermissionBoundary"
        }
      }
    }
  ]
}
```

This ensures:

* Roles **cannot be created** without the boundary
* Developers cannot bypass the guardrail

---

## Step 4 — Validate Using Policy Simulator

### Simulate Allowed Scenario

* Identity: Developer role
* Action: `iam:CreateRole`
* Boundary applied

Expected: **Allowed**

### Simulate Escalation Attempt

* Attach `AdministratorAccess` to a role under boundary

Expected: **Denied** for IAM actions

---

## Step 5 — Runtime Validation

Confirm developer-created role permissions:

```bash
aws sts get-caller-identity
```

Attempt restricted action:

```bash
aws iam list-users
```

Expected result: **AccessDenied**

---

## Troubleshooting

| Symptom                                   | Likely Cause             | Resolution                 |
| ----------------------------------------- | ------------------------ | -------------------------- |
| Developer can create admin role           | Boundary not attached    | Enforce boundary condition |
| AccessDenied on valid service             | Boundary too restrictive | Adjust allow list          |
| Simulator shows allowed but runtime fails | Wrong identity assumed   | Validate STS identity      |

---

## Security Notes

* Permission boundaries do **not** grant permissions
* They only restrict what permissions can be granted
* Explicit deny in boundary always wins

---

## Anti-Patterns (Do Not Do This)

* Allowing `iam:*` in boundaries
* Using boundaries instead of least privilege
* Relying on naming conventions without conditions

---

## Key Principle

> Least privilege defines what is allowed.
> Permission boundaries define what is **never allowed**.

Both are required for safe developer self-service.

---

## Related Documentation

- Handbook: [Policy Simulator vs Runtime Identity](../iam-handbook/policy-simulator-vs-runtime-identity.md)
- Runbook: [Fix IAM AccessDenied Errors](../iam-runbooks/fix-iam-AccessDenied-errors.md)

## Last Updated

2025-12-18