---
title: "e39-config"
doc-id: "mb-a9424736"
updated: "2026-10-12"
---

## From `step-mapping.md`: this step's rows

### Phase D — Build & Verify (per-feature loop)

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 39 | `[[step-39-triage]]` | Skill + GATE | Matt [[[makepdlf-project-library:stepwise/step-39-triage\|triage]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-39-triage.md) | `build-verified` |

### Phase D — Build & Verify (per-feature loop): phase notes

Repeats once per feature/package from Step 19's ticket list, until every feature has
individually reached `build-verified`. For the loop's actual order and dependencies, see
[[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md), "Step 35 Feature Loop."


Exit gate: `build-verified`, evaluated per feature. For entry condition and dependencies,
see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

### Gate Summary

`build-verified` sits at Step 39 ([[[makepdlf-project-library:stepwise/step-39-triage|triage]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-39-triage.md)), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md) for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `build-verified` | 39 (per feature) |

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase E — Build & Verify (Steps 35–40)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 39 | triage | Skill + GATE | **Full** | Labels, comments, issue-tracker updates from Steps 37–38 findings. GATE `build-verified` fires here (moved from Step 40 — [[[pdlf:pdlf-library/adr-local/two-gate-extension]]](C:/pdlf/pdlf-library/adr-local/two-gate-extension.md)) — full BFT mandatory regardless of the table's usual Light assignment for triage-type work. |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `build-verified` | 39 | Build complete, architecture scan and any developer-approved remediation applied and retested, design review done, code review done, QA passed, triage complete for this feature cycle. Evaluated once per feature — the pipeline does not advance to Step 41 until every feature has individually passed this gate. Features are known-good baselines. |

## From `matt-pocock-skills-local-reference.md`: skill used

| PDLF Step | Matt Pocock Skill | Notes |
|---|---|---|
| Step 39 | `triage` | Processes findings from Steps 36–38, gate `build-verified` |

## From `matt-pocock-skills-pdlf-compliance.md`: skill in scope

| Skill | Used at | Type | Wrapper or Fat |
|---|---|---|---|
| `triage` | Step 39 | User-invoked | Fat, **has an unresolved dependency — see §2** |
