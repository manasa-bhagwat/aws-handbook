---
title: Policy Simulator vs Runtime Identity
parent: IAM Handbook
nav_order: 1
---

# Policy Simulator vs Runtime Identity
---

## Purpose

This document explains **what IAM Policy Simulator can validate** and **what only runtime identity checks can validate**. The goal is to prevent a common operational failure: fixing IAM policies correctly while the workload still fails due to incorrect identity wiring.

> Use this page to build the right mental model. Use runbooks to execute.

---

## The Two-Layer Model (Non‑Negotiable)

AWS authorization problems must be evaluated in **two distinct layers**:

1. **Permission Logic (IAM Evaluation)** — *Is this identity allowed to do this action?*
2. **Runtime Identity (Who is actually calling AWS?)** — *Which identity is in effect at execution time?*

Both layers must be correct for access to succeed.

---

## IAM Policy Simulator — What It Is

**IAM Policy Simulator** evaluates IAM **policy logic only**.

It answers the question:

> *If this IAM identity were used, would IAM allow this action on this resource?*

### What It Evaluates

* Identity-based policies (inline + managed)
* Group policies
* Permission boundaries
* Explicit denies

### What It Does NOT Evaluate

* Whether the identity is actually attached to a workload
* Whether the workload is assuming the intended role
* Credential freshness or caching
* EC2 metadata availability (IMDS)
* Application-level credential usage

**Key takeaway:** Policy Simulator proves *the policy*, not *the wiring*.

---

## Runtime Identity — What It Is

**Runtime identity** is the identity AWS sees **at execution time**.

It answers the question:

> *Who is actually calling AWS right now?*

Runtime identity is validated using:

* EC2 instance metadata (role attachment)
* `sts:GetCallerIdentity`

This layer confirms:

* The correct role is attached
* The role is actively assumed
* No static credentials are being used

---

## Why Both Are Required (Common Failure Pattern)

A frequent production issue:

* IAM Policy Simulator → **Allowed**
* Application / CLI → **AccessDenied**

This indicates:

* IAM policy is correct
* **Runtime identity is wrong**

Typical causes:

* Wrong instance profile attached
* Role attached after instance launch (credentials not refreshed)
* Application still using `AWS_ACCESS_KEY_ID`
* IMDSv2 blocked or misconfigured

---

## Decision Comparison

| Capability                      | Policy Simulator | Runtime Identity Checks |
| ------------------------------- | ---------------- | ----------------------- |
| Validate IAM permission logic   | ✅                | ❌                       |
| Validate role attachment        | ❌                | ✅                       |
| Detect wrong assumed role       | ❌                | ✅                       |
| Detect static credentials usage | ❌                | ✅                       |
| Safe pre-deployment testing     | ✅                | ❌                       |

---

## Correct Operational Order

In real incidents and audits, follow this order:

1. **Identify failing API call** (CloudTrail)
2. **Validate permission logic** (Policy Simulator)
3. **Validate runtime identity** (STS + metadata)
4. **Apply minimal fix**

Skipping steps leads to misdiagnosis.

---

## Practical Rule of Thumb

> If Policy Simulator says **Denied** → fix IAM policy.
>
> If Policy Simulator says **Allowed** but access still fails → fix identity wiring.

Never change IAM policies without confirming runtime identity.

---

## Where This Is Used

* EC2 → S3 access validation
* ECS task role debugging
* Lambda execution role issues
* CI/CD OIDC role troubleshooting
* Cross-account AssumeRole failures

See related runbooks for execution details.

---

## References

- Runbook: [EC2 Access to S3 via IAM Role](../iam-runbooks/ec2-access-s3-using-iam-role.md)
- Runbook: [Fix IAM AccessDenied Errors](../iam-runbooks/fix-iam-AccessDenied-errors.md)

---

This page intentionally avoids step-by-step commands. All procedures live in runbooks.
