---
title: Architecture
parent: IAM Handbook
nav_order: 1
---

# Request Flow & Architecture
---

## Purpose

This document explains how AWS Identity and Access Management (IAM) evaluates an AWS request from initiation to authorization.

The focus is on the **observable request flow**, not on internal AWS implementation details.

---

## High-Level Request Flow

**Request path:**

```
Principal → IAM → Policy Evaluation → AWS Service
```

IAM acts as a **central authorization gate**.

Every AWS API request passes through IAM before the target service processes it.

---

## Diagram

![AWS IAM Request Evaluation Flow & Architecture](docs/iam/images/aws-iam-architecture.png)

AWS IAM Request Evaluation Flow & Architecture

---

## Step-by-Step Flow Explanation
### 1. Principal Initiates the Request

A principal is the identity that makes an AWS request.

A principal can be:

- An IAM user
- An IAM role assumed by an AWS service or application

**Why this matters:**

IAM evaluates permissions based on the principal, not on the resource alone.

---

### 2. Request Reaches IAM
Before the request reaches the target AWS service, it is intercepted for authorization.

IAM is invoked **automatically** and **implicitly** for every AWS API request.

**Key point:**

IAM is not optional and cannot be bypassed.

---

### 3. Policy Evaluation
IAM collects all policies applicable to the principal and the target resource, including:

- Identity-based policies
- Resource-based policies

IAM then evaluates the request using a fixed decision process:

- Explicit deny takes precedence
- Explicit allow permits the action
- Absence of allow results in denial

**Key point:**

Authorization is fully determined before the service receives the request.

---

### 4. Request Reaches the AWS Service
Only after IAM authorization succeeds does the request reach the target AWS service.

The service assumes that:

- The caller is authenticated
- The action is authorized

The service does not re-evaluate permissions.

---

## When IAM Is Evaluated
IAM authorization is evaluated:

- On **every AWS API call**
- For **every service**
- Across **all regions**

There is no caching or session-based bypass at the IAM layer.

---

## Why IAM Roles Are Preferred Over IAM Users
IAM roles are the preferred identity mechanism for applications and AWS services because:

- Roles provide temporary credentials
- No long-lived secrets are stored
- Access is granted only for the duration of the session

IAM users are primarily intended for:

- Human access
- Administrative or operational tasks

**Design implication:**

Production workloads should assume roles rather than use user credentials.

---

## Summary

- IAM sits **between the caller and every AWS service**.
- Authorization decisions are made **before** service execution.
- The request flow is consistent across all AWS services.
- Roles enable secure, temporary, and auditable access.

---

## Scope Note

This document intentionally excludes:

- STS internal behavior
- Credential rotation mechanisms
- Federation and external identity providers

These topics are addressed separately.

---