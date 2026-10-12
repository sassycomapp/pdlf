---
title: "f46-reference"
doc-id: "mb-2630906c"
updated: "2026-10-12"
---

## From `46-learn-junction.md`

## Task Execution Order

1. Run `/retro` — retrospective report
2. Run `/learn` — capture learnings
3. Run `/context-save` — persist working state
4. Update ISA: fill Verification section, update Changelog
5. Update registry: `current_step: 46`, `last_gate: "released"`, `active: false`
6. → GATE: Execute gate procedure per [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)
7. → GATE: `released` (jointly with Step 45) — developer approval required to close the project cycle
8. GBrain sync + embed (learnings are now searchable for next project)
9. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
10. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) (Full — gate override)

---

## Description

Non-skippable retrospective and learning capture. Closes the cycle.

## Actions

1. `/retro` — retrospective report
2. `/learn` — capture learnings
3. `/context-save` — persist working state
4. Update ISA: fill Verification section, update Changelog
5. Update registry: `current_step: 46`, `last_gate: "released"`, `active: false`
6. GBrain sync + embed

## Outputs

- Retrospective report
- Captured learnings in GBrain
- ISA updated and verified
- GATE `released` — Full BFT (jointly with Step 45), gate summary, developer approval required

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 46 | LEARN | **GATE** `released` (jointly with 45) | OpenCode |

## LEARN Junction

The LEARN junction closes the project cycle. ISA update points: 26, 35, 38, 46.

## Reference Files

| [[[pdlf:pdlf-library/templates-local/isa-template-v2\|ISA Template v2]]](C:/pdlf/pdlf-library/templates-local/isa-template-v2.md) | Steps 26, 35, 38, 46 |

## Gate

| Gate | After Step | What is Locked |
|---|---|---|
| `released` | 45 + 46 | Production deployed, initial canary passed, LEARN complete, ISA Verification/Changelog updated. Cycle closed. |

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)
For gate procedure: [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
