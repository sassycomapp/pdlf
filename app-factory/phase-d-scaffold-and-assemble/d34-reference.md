---
title: "d34-reference"
doc-id: "mb-b9f09cb4"
updated: "2026-10-24"
---

## From `34-architectural-sanity-audit.md`

## Task Execution Order

1. Compare actual Anvil data tables schema against ADRs and domain model (every table/column traces to a locked decision)
2. Compare actual UI forms against approved screens and DESIGN.md
3. Compare actual scaffolding against scaffold-plan.md (every planned module/function exists, nothing extra improvised)
4. → Decision point: Any drift found? If yes, correct Anvil-side artifact or formally update plan/ADR per deviation mechanism
5. Produce short audit report — what was checked, findings, discrepancies, verdict
6. Save audit report to `<project-library>/pdlf/step-34-architecture-audit.md`
7. → GATE: Execute gate procedure per [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)
8. → GATE: `architecture-verified` — developer approval required to proceed before any code-writing begins
9. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
10. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft|spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) (Full — gate override)

---

## Description

Confirms the physical Anvil build matches the locked architecture before any
code-writing begins.

## Inputs Required

- Step 15/16 architecture and domain model (TDD cluster, GLOSSARY.md, ADRs)
- Step 21 concept audit report
- Pulled-to-local data tables schema (from 18)
- Pulled-to-local UI forms (from 30)
- Pulled-to-local scaffolding (from 33) against scaffold-plan.md (Step 31)

## Outputs

- Audit report saved to `<project-library>/pdlf/step-34-architecture-audit.md`
- GATE `architecture-verified` — full BFT, gate summary, developer approval required

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 34 | Gate (OpenCode-native) | **GATE** `architecture-verified` | OpenCode |

## Gate

| Gate | After Step | What is Locked |
|---|---|---|
| `architecture-verified` | 34 | Data tables, UI forms, and scaffolding confirmed to match the locked architecture. No code-writing begins without this gate passing. |

## Reference Files

| Legacy step ref | Steps 21 and 34 (pending rename) |

## Artifact Routing

| Sanity audit reports (21, 34) | `<project-library>/pdlf/step-21-concept-audit.md`, `step-34-architecture-audit.md` |

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
