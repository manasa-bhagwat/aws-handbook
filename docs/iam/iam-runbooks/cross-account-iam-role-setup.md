---
title: Cross-Account IAM Role Setup
parent: IAM Runbooks
nav_order: 1
---

# Cross-Account IAM Role Setup
---

## Objective

Enable controlled access between AWS accounts.

## Preconditions

- Access to both accounts
- STS permissions

## Inputs

- Source account ID
- Target account ID

## Steps

1. Create Role in target account
2. Add trust policy for source account
3. Attach permission policy
4. Assume role from source

## Validation

- `get-caller-identity` shows assumed role

## Rollback

- Remove trust relationship

## Edge Cases

- MFA required for role assumption

## Last Updated

2025-12-19