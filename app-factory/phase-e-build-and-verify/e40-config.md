---
title: "e40-config"
doc-id: "mb-8575eede"
updated: "2026-10-23"
---

## From `step-mapping.md`: this step's rows

### Phase D — Build & Verify (per-feature loop)

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 40 | ``[[step-40-improve-codebase-architecture]]`` | Skill (optional) | Matt [[[makepdlf-project-library:stepwise/step-40-improve-codebase-architecture\|Step 40 Improve Codebase Architecture]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-40-improve-codebase-architecture.md) — read-only | |

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
| 40 | improve-codebase-architecture | Skill (optional, per feature cycle) | **Light** | Read-only report, no code touched, no gate here. Optional recommendation, not a judgment-heavy step in itself. |

## From `matt-pocock-skills-local-reference.md`: skill used

| PDLF Step | Matt Pocock Skill | Notes |
|---|---|---|
| Step 40 | [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference\|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) | Optional architecture health scan, read-only |

## From `matt-pocock-skills-pdlf-compliance.md`: skill in scope

| Skill | Used at | Type | Wrapper or Fat |
|---|---|---|---|
| [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference\|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) | Step 40 (optional) | User-invoked | Fat, **has an unresolved dependency — see §2** |
