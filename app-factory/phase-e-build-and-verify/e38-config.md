---
title: "e38-config"
doc-id: "mb-eaf9d4db"
updated: "2026-10-12"
---

## From `step-mapping.md`: this step's rows

### Phase D — Build & Verify (per-feature loop)

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 38 | `[[step-38-qa]]` | Skill | GStack [[[makepdlf-project-library:stepwise/step-38-qa\|/qa]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-38-qa.md) | |

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
| 38 | /qa | Skill | **Full** | Systematic QA testing + bug fixing — quality and regression decisions |
