---
title: Fix IAM AccessDenied Errors
parent: IAM Runbooks
nav_order: 1
---

# Fix IAM AccessDenied Errors
---

## Objective

Identify and resolve IAM authorization failures safely.

## Preconditions

- IAM read access
- CloudTrail access

## Inputs

- IAM principal ARN
- Failing AWS action
- Resource ARN

## Steps

1. Capture exact error message
2. Identify calling principal
    - `aws sts get-caller-identity`
3. Check attached policies
    - User → Group → Role hierarchy
4. Use IAM Policy Simulator
    - Test failing action
5. Check for explicit denies
    - SCPs
    - Permission boundaries
6. Review CloudTrail logs
    - EventName + errorCode

## Validation

- Simulator returns “Allowed”
- Action succeeds via CLI/console

## Rollback

- Revert policy changes
- Restore last known working policy

## Edge Cases

- Explicit deny always wins
- Region-specific resource ARNs

## Last Updated

2025-12-18
