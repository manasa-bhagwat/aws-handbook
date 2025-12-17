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
4. Validate from EC2
    - `aws s3 ls s3://bucket-name`

## Validation
- No access keys on EC2
- S3 access succeeds

## Rollback
- Detach IAM role
- Remove policy

## 7. Edge Cases
- IMDSv2 enforcement
- Bucket policy conflicts

## 8. Last Updated
2025-12-17