---
title: EC2 Access S3 Using IAM Role
parent: IAM Runbooks
nav_order: 1
---

# EC2 Access S3 Using IAM Role
---

## Objective
Grant EC2 access to S3 without static credentials.

## Preconditions
- EC2 instance running
- Admin IAM access

## Inputs
- EC2 instance ID
- S3 bucket name

## Steps
1. Create IAM Role
    - Trusted entity: EC2
2. Attach S3 Read Policy
    - Restrict to specific bucket
3. Attach Role to EC2
    - Instance → Modify IAM role

## Validation

1. **Confirm no static credentials**
    - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` **not present** on EC2
2. **Confirm role attachment**
    
    ```bash
    curl http://169.254.169.254/latest/meta-data/iam/info
    ```
    
    - Expected: correct IAM role ARN
3. **Confirm runtime identity**
    
    ```bash
    aws sts get-caller-identity
    ```
    
    - Expected: `assumed-role/<role-name>/<instance-id>`
4. **Confirm S3 access**
    
    ```bash
    aws s3ls s3://<bucket-name>
    ```
    
    - Expected: command succeeds
5. **Confirm permission logic (IAM)**
    - IAM Policy Simulator shows **Allowed** for required S3 actions

## Rollback
- Detach IAM role
- Remove policy

## Edge Cases
- IMDSv2 enforcement
- Bucket policy conflicts

## Last Updated
2025-12-18