---
title: "step-27-screen-production"
doc-id: "mb-0d50f323"
updated: "2026-10-10"
---
## Task Execution Order

1. → Decision point: This step is deferred. Skip unless explicitly requested by developer.
2. If active: Produce screen HTML from approved wireframe (Step 26)
3. Apply wireframe fidelity checklist
4. Apply screen standard compliance checklist
5. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
6. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full)

---

## Description

Screen HTML production from approved wireframes. This step is deferred for
projects not producing screens/wireframes.

## Inputs Required

- Approved wireframe from Step 26
- Project's screen-production standard document

## Outputs

- Screen HTML at `<project-library>/screens/{package}/{FormName}/`
- Wireframe fidelity checklist
- Screen standard compliance checklist

**Status:** Out of scope for current project. The procedure was documented in
`obsolete/screen-production-procedure.md` (deleted 2026-07-19, commit eb26565 — no longer on
disk anywhere, verified 2026-09-18); this step file is the surviving record of the procedure.

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 27 | OpenCode-native | | Screen Production |

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
