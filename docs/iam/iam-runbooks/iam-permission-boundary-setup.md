---
title: Permission Boundary Setup
parent: IAM Runbooks
nav_order: 1
---

# Permission Boundary Setup
---

## Objective

Prevent privilege escalation by restricting maximum permissions.

## Preconditions

- IAM admin access

## Inputs

- Developer role/user

## Steps

1. Create permission boundary policy
2. Attach to IAM role/user
3. Test restricted actions

## Validation

- Escalation attempts denied

## Rollback

- Detach boundary

## Edge Cases

- Boundary misunderstood as permission grant

## Last Updated

2025-12-19