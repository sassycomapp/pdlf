---
title: "step-28-screen-to-png"
doc-id: "mb-2b556853"
updated: "2026-10-10"
---
## Task Execution Order

1. → Decision point: This step is deferred. Skip unless explicitly requested by developer.
2. If active: Convert screen HTML from Step 27 to PNG
3. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
4. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (None)

---

## Description

Converts screen HTML to PNG via an external rendering tool. Deferred alongside
Step 27.

## Outputs

- Screen PNG in same folder as Step 27

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 28 | External tool | | Screen → PNG conversion |

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
