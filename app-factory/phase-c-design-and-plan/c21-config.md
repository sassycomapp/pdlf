---
title: "c21-config"
doc-id: "mb-2cd6bb36"
updated: "2026-10-12"
---

## From `step-mapping.md`: this step's rows

### Phase B — Design & Plan

| Step | File | Type | Handler | Gate |
|---|---|---|---|---|
| 21 | `[[step-21-concept-sanity-audit]]` | Gate | OpenCode | `concept-locked` |

### Phase B — Design & Plan: phase notes

Exit gates: `concept-locked` (Step 21), `wireframes-approved` (Step 26). For entry
condition and dependencies, see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md).

### Gate Summary

`build-verified` sits at Step 39 ([[[makepdlf-project-library:stepwise/step-39-triage|triage]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-39-triage.md)), not Step 40 — architecture remediation (40,
40B) must complete and be retested (36, 37, 38) before the gate is evaluated, not after
(ADR: two-gate-extension). Note this table lists gates in phase order for readability;
it is not a sequence claim — see [[[makepdlf-project-library:stepwise/run-plan|Run Plan]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/run-plan.md) for the loop's actual internal order.

| Gate | After Step |
|---|---|
| `concept-locked` | 21 |

## From `bft-checkpoint-cheatsheet-v2.md`: BFT level

### Phase C — Design & Plan (Steps 17–28)

| Step | Name | Type | BFT | Rationale |
|---|---|---|---|---|
| 21 | Concept sanity audit | Gate (OpenCode) | **Full** | GATE `concept-locked`. Cross-references plan, CEO, Eng, domain model, DESIGN.md for contradictions. Scope freeze. |

## From `spec-gate-procedure.md`: gate

| Gate | After Step | What is Locked |
|---|---|---|
| `concept-locked` | 21 | Full concept coherence audit passed. Scope frozen. No new feature may be added without formally reopening this gate. |
