---
title: Secure AWS Root Account
parent: IAM Runbooks
nav_order: 1
---

# Secure AWS Root Account
---

## Objective

Harden the AWS root account to prevent account takeover, accidental misuse, and compliance violations. Root access is reduced to emergency-only usage.

## Preconditions

- Root user login access (email + password)
- Physical MFA device or authenticator app
- AWS Management Console access

## Inputs

- AWS Account ID
- Root email address

## Steps

1. Login to AWS Console as root user
    
    (Use root email, not IAM user)
    
2. Enable MFA on root account
    - Go to IAM → Dashboard
    - Enable MFA
    - Register virtual or hardware MFA
3. Remove root access keys
    - IAM → Security Credentials
    - Delete any existing access keys
4. Create Admin IAM Role
    - IAM → Roles → Create role
    - Trusted entity: AWS Account
    - Attach `AdministratorAccess`
    - Name: `account-admin`
5. Create Admin IAM User
    - IAM → Users → Create user
    - No policies directly attached
    - Enable console access + MFA
6. Allow user to assume admin role
    - Attach trust policy to role
    - Validate role switching

## Validation

- Root user shows **MFA enabled**
- Root user has **0 access keys**
- Admin IAM user can assume `account-admin`
- Daily operations performed without root

## Rollback Procedure

- Login as root
- Temporarily re-enable admin access if locked out
- Re-create emergency admin role if deleted
- Stop and escalate if root MFA device lost

## Edge Cases

- Lost MFA device → AWS Support recovery
- Organization SCPs blocking root changes

## Last Updated

2025-12-17