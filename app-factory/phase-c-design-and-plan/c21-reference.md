---
title: "c21-reference"
doc-id: "mb-06a9bf5e"
updated: "2026-10-24"
---

## From `21-concept-sanity-audit.md`

## Task Execution Order

1. Read all Phase B+C inputs: spec (Step 13), CEO review (Step 14), Eng review (Step 15), GLOSSARY.md + ADRs (Step 16), DESIGN.md (Step 20)
2. Cross-reference each document pair for contradictions
3. Produce short audit report — what was checked, findings, discrepancies, verdict
4. Save audit report to `<project-library>/pdlf/step-21-concept-audit.md`
5. → GATE: Execute gate procedure per [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)
6. → GATE: `concept-locked` — developer approval required. From this point forward, no new feature may be added without formal gate reopening.
7. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
8. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft|spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) (Full — gate override)

---

## Description

Cross-references all Phase B+C outputs for consistency. Hard scope freeze —
after this gate, no new feature may be added without formal gate reopening.

## Inputs Required

- Step 13 spec at `<project-library>/output-matt-skills/step-13-spec.md` — also available as GitHub issue #<number> on project repo
- Step 14 CEO plan + review report at `<project-library>/output-gstack/step-14-ceo-plan.md`
- Step 15 Eng review (TDD cluster)
- Step 16 GLOSSARY.md + ADRs
- Step 20 DESIGN.md

## Outputs

- Audit report saved to `<project-library>/pdlf/step-21-concept-audit.md`
- GATE `concept-locked` — full BFT, gate summary, developer approval required

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 21 | Gate (OpenCode-native) | **GATE** `concept-locked` | OpenCode |

## Gate

| Gate | After Step | What is Locked |
|---|---|---|
| `concept-locked` | 21 | Full concept coherence audit passed. Scope frozen. No new feature may be added without formally reopening this gate. |

## Reference Files

| Legacy step ref | Steps 21 and 34 (pending rename) |

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)
For gate procedure: [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
