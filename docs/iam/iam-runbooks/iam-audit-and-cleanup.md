---
title: IAM Audit and Cleanup
parent: IAM Runbooks
nav_order: 1
---

# IAM Audit and Cleanup
---

## Objective

Reduce security risk by cleaning unused and excessive IAM entities.

## Preconditions

- Read-only or admin IAM access

## Inputs

- Account ID

## Steps

1. Review IAM credential report
2. Identify unused users/roles
3. Remove unused access keys
4. Enforce MFA gaps
5. Document findings

## Validation

- Reduced IAM sprawl
- Audit report generated

## Rollback

- Restore deleted users if needed

## Edge Cases

- Legacy service users

## Last Updated

2025-12-19