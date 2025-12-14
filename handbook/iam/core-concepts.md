# Core Concepts

## Overview
AWS Identity and Access Management(IAM) is the authentication and authorization system for AWS.

It defines who can access AWS, what actions they are allowed to perform and which AWS resources those actions apply to. 

IAM exists to enforce controlled access to cloud resources without embedding credentials or permissions directly into applications or infrastructure.

IAM operates globally across an AWS account and is evaluated every time an AWS API request is made.

---

# Core IAM Entities

### IAM User
An IAM user represents a human or system idetity that requires direct access to AWS.

An IAM user consists of:
- A unique name
- Authentication credentials (password and/or access keys)
- Assigned permission

**Why it Exists**
IAM users provide a way to identify individual actors and apply permissions ina a controlled manner.

---
### IAM Group

An IAM group is a collection of IAM users.

Groups do not authenticate or act independently. Permissions are assigned to the group and inherited by its members.

**Why it exists**
IAM groups simplify permission management by allowing access to be granted based on role or responsibility rather than per-user configuration.

---
### IAM Role
An IAM role is an AWS identity with a defined set of permissions that can be assumed by trusted principals.

Unlike users, roles:
- Do not have long-lived credentials.
- Provide temporary credentials whaen assumed.

**Why it exist**
IAM roles enable secure access for AWS services, applications and external identities without the use of permanent credentials.

---

### IAM Policy
An IAM policy is a permission document that defines allowed or denied actions on AWS resources.

Policies are written in JSON and consist of:
- Effect (Allow or Deny)
- Actions
- Resources

**Why it Exists**
Policies provide a structures and auditable way to express authorization rules.

---

### Authentication vs Authorization
**Authentication** verifies who the caller is.
Examples include:
- Signing in with a username and password.
- Using access keys to sign API requests.

IAM handles authentication before authorization is evaluated.

**Authorization** determines what the authenticated identity is allowed to do.

IAM authorization is based is based on evaluating applicable policies attatched to the identity and the target resource.

---

### Types of IAM Policies

**Identity-Based Policies**
Identity-based policies are attatched to:
- IAM users
- IAM groups
- IAM roles

They define what actions the identity is permitted to perform on which resources.

They provide direct control over what an identity can do within an AWS account.

**Resource-Based Policies**
Resource-based policies are attatched directly to AWS resources.

They define which principles are allowed to access the resources and under what conditions.

They enable resource owners to control access without modifying the caller's identity configuration.

---

### IAM Policy Evaluation Logic
When an AWS request is made, IAM evaluates permissions using the following logic:
1. All applicable policies are collected.
2. If any policy explicitly denies the request, the request is denied.
3. If at least one policy explicitly allows the request and no explicit deny exists, the request is allowed.
4. If no explicit allow is found, the request is denied by default.

**Key priciples:**
- Explicit deny always overrides allow.
- Lack of permission results in denial.

---

### Global Scope of IAM

IAM is a global service.
- Users, groups, roles, and policies are not tied to a specific region.
- IAM authorization applies consistently across all AWS regions.

**Why this matters**
A single identity configuration governs access to resources regardless of where those resources are deployed.

---

## Summary
IAM provides a centralized and consistent mechanism to:
- Identify principals
- Authenticate requests
- Authorize actions on AWS resources

It forms the foundation of security and access control in AWS and is evaluated for every API  request made within an account.

---

**Scope Note**
This handbook intentionally covers foundational IAM concepts only. 

Advanced authorization constructs and organisation-level controls are addressed separately.

---