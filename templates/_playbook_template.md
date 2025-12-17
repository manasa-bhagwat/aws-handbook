# Playbook: <INCIDENT OR FAILURE TYPE>

## 1. Incident Description
Short definition of what broke.

## 2. Severity Classification
- SEV1 / SEV2 / SEV3 criteria

## 3. Symptoms
- What users see
- What logs show
- What metrics spike/drop

## 4. Immediate Actions (First 5 Minutes)
- Contain blast radius
- Stop any automated scaling or pipelines
- Stabilize environment

## 5. Diagnostic Workflow (Decision Tree)
### Step 1 → Check X
If YES → go to Step A
If NO → go to Step B

### Step 2 → Check Y
(Repeat)

## 6. Root Cause Areas to Investigate
- Permissions
- Networking
- Service limits
- Misconfigurations
- Upstream/downstream failures

## 7. Remediation Steps
- Short-term fix
- Long-term fix

## 8. Recovery Verification
- Metrics to validate
- Smoke test steps

## 9. Postmortem Notes
- What failed
- What was missed
- What should be automated

## 10. Last Updated
<timestamp>
