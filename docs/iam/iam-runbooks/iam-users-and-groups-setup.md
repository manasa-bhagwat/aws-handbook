---
title: IAM Users and Groups Setup
parent: IAM Runbooks
nav_order: 1
---

# IAM Users and Groups Setup
---

## Objective

Create human identities using IAM groups and enforce least privilege with MFA.

## Preconditions

- Admin role access
- IAM permissions to create users/groups

## Inputs

- Usernames
- Required access level (admin/dev/readonly)

## Steps

1. Create IAM Groups
    - `admins` → AdministratorAccess
    - `developers` → Custom limited policy
    - `readonly` → ReadOnlyAccess
2. Create IAM User
    - Console + programmatic access (if needed)
    - No policies directly attached
3. Assign User to Group
    - Attach group membership only
4. Enforce MFA
    - Enable virtual MFA
    - Communicate MFA setup steps securely

## Validation

- User permissions inherited only from group
- MFA enforced before privileged access
- No inline user policies exist

## Rollback

- Remove user from group
- Disable user login
- Delete user if unused

## Edge Cases

- Shared users (disallowed)
- Forgotten MFA reset

## Last Updated

2025-12-18