---
title: Basics
parent: IAM Cheatsheets
nav_order: 1
---

# Basics

---

## Core IAM Entities

- **IAM User**
    
    A named identity representing a human or system that can authenticate directly with AWS.
    
- **IAM Group**
    
    A logical collection of IAM users used to assign permissions collectively.
    
- **IAM Role**
    
    An AWS identity with permissions that can be assumed by trusted principals using temporary credentials.
    
- **IAM Policy**
    
    A JSON document that defines allowed or denied actions on specified AWS resources.
    

---

## Authentication vs Authorization

- **Authentication**
    
    Verifies the identity making the request.
    
- **Authorization**
    
    Determines whether the authenticated identity is permitted to perform the requested action.
    

---

## IAM Policy JSON Structure

Minimal structure of an IAM policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "service:Action",
      "Resource": "arn:aws:service:region:account-id:resource"
    }
  ]
}
```

Key fields:

- **Effect**: Allow or Deny
- **Action**: API operations
- **Resource**: Target AWS resources

---

## Identity-Based vs Resource-Based Policies

- **Identity-Based Policy**
    
    Attached to users, groups, or roles and defines what the identity can do.
    
- **Resource-Based Policy**
    
    Attached directly to a resource and defines which principals can access it.
    

---

## Common AWS Managed Policies

Frequently used managed policies:

- `AdministratorAccess`
- `ReadOnlyAccess`
- `PowerUserAccess`
- `AmazonS3ReadOnlyAccess`
- `AmazonEC2ReadOnlyAccess`

Managed policies are maintained by AWS and updated automatically.

---

## IAM Policy Evaluation Summary

- Explicit deny overrides allow
- At least one explicit allow is required
- Absence of allow results in denial

---

## Top 3 Beginner IAM Mistakes

1. Attaching policies directly to users instead of using groups
2. Using long-lived access keys for applications instead of IAM roles
3. Assuming permissions propagate immediately without verification

---

## Where to Check Permissions Quickly

- **IAM Console**
    - Users → Permissions
    - Groups → Permissions
    - Roles → Permissions
- **CloudTrail**
    - View denied API calls
    - Confirm which identity made the request

---

## IAM Scope Reminder

- IAM is a **global service**
- Permissions apply across all AWS regions

---

### Scope Note

This cheatsheet intentionally excludes:

- Policy conditions
- Permission boundaries
- Organization-level controls

