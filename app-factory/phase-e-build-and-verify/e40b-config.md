---
title: "e40b-config"
doc-id: "mb-25f93005"
updated: "2026-10-12"
---

## From `step-mapping.md`: this step's rows

### Phase D — Build & Verify (per-feature loop)

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 40B | [[[makepdlf-project-library:stepwise/step-40b-remediation\|Step 40B Remediation]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-40B-remediation.md) | OpenCode (conditional) | Apply developer-approved fixes from Step 40 | |

### Phase D — Build & Verify (per-feature loop): phase notes

Repeats once per feature/package from Step 19's ticket list, until every feature has
individually reached `build-verified`. For the loop's actual order and dependencies, see
[[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md), "Step 35 Feature Loop."


Exit gate: `build-verified`, evaluated per feature. For entry condition and dependencies,
see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase E — Build & Verify (Steps 35–40)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 40B | Remediation | OpenCode (conditional) | **Light** | Applies only developer-approved fixes from Step 40 — scoped execution, not open design |
