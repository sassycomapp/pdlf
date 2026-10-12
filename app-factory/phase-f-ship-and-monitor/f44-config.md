---
title: "f44-config"
doc-id: "mb-1edd98fd"
updated: "2026-10-12"
---

## From `step-mapping.md`: this step's rows

### Phase E — Ship & Monitor

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 44 | `[[step-44-promote-to-production]]` | Manual + GATE | Promote to Production | `production-released` |

### Phase E — Ship & Monitor: phase notes

**Note:** Steps 42, 42A, 43, and 44 are flagged for rebuild — see `ToDo.md` item 2. They
currently model a staging/production environment split that does not apply to this
platform (see `[[adr-no-staging-environment-five-app-isolation]]`). Listed here as
currently defined; not yet corrected.


Exit gates: `production-released` (Step 44), `released` (Step 46). For entry condition
and dependencies, see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

### Gate Summary

`build-verified` sits at Step 39 ([[[makepdlf-project-library:stepwise/step-39-triage|triage]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-39-triage.md)), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md) for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `production-released` | 44 |

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase F — Ship & Monitor (Steps 41–46)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 44 | Promote to Production | Manual + GATE | **Full** | GATE `production-released`. Commits the app to real users. Full BFT mandatory. |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `production-released` | 44 | Staging smoke test passed, same commit promoted to Production, databases confirmed separate. App is live. |
