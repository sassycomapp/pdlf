---
title: "d34-config"
doc-id: "mb-192abeee"
updated: "2026-10-12"
---

## From `step-mapping.md`: this step's rows

### Phase C — Scaffold & Assemble

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 34 | `[[step-34-architectural-sanity-audit]]` | Gate | OpenCode | `architecture-verified` |

### Phase C — Scaffold & Assemble: phase notes

Exit gate: `architecture-verified` (Step 34). For entry condition and dependencies, see
[[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

### Gate Summary

`build-verified` sits at Step 39 ([[[makepdlf-project-library:stepwise/step-39-triage|triage]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-39-triage.md)), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md) for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `architecture-verified` | 34 |

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase D — Scaffold & Assemble (Steps 29–34)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 34 | Architectural sanity audit | Gate (OpenCode) | **Full** | GATE `architecture-verified`. Confirms physical Anvil build matches locked architecture. |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `architecture-verified` | 34 | Data tables, UI forms, and scaffolding confirmed to match the locked architecture. No code-writing begins without this gate passing. |
