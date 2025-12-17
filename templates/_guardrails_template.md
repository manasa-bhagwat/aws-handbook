# Guardrails: <TOPIC NAME>

## 1. Purpose
Explain why these guardrails exist.
What risk, inconsistency, or operational hazard they prevent.

## 2. Scope
Define the services, accounts, environments, or teams this applies to.

## 3. Mandatory Guardrails (MUST)
List the absolute, non-negotiable rules.
Examples:
- MUST deploy subnets across 3 AZs.
- MUST encrypt storage with KMS.
- MUST use Multi-AZ for production databases.

## 4. Recommended Guardrails (SHOULD)
Best practices that aren’t strictly mandatory but strongly encouraged.

## 5. Prohibited Patterns (MUST NOT)
Rules that must never be broken.
Examples:
- MUST NOT deploy NAT Gateway in only 1 AZ.
- MUST NOT hardcode AZ identifiers.

## 6. Enforcement Mechanisms
How to enforce:
- SCPs
- IAM boundaries
- CI/CD validations
- Terraform policies (OPA/Conftest)

## 7. Example Compliant Implementation
Good example (architecture diagram or YAML snippet).

## 8. Example Non-Compliant Implementation
Bad example with explanation of risk.

## 9. Exceptions Process
When someone can break a guardrail and who approves it.

## 10. Version History
Track changes to guardrails over time.
