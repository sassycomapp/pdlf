---
title: "f45-reference"
doc-id: "mb-eac0114b"
updated: "2026-11-08"
---

## Production check

## Task Execution Order

1. Run GStack `/canary` — targeted at the test client instance, against its baseline from Step 43
2. Read every client instance's heartbeat in App 5 for the release version and schema fingerprint
3. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
4. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (Full)

---

## Description

Post-deploy monitoring loop — watches for console errors, performance
regressions, and page-load failures on the test client instance, and reads every client
instance's heartbeat.
Contributes to the `released` gate jointly with Step 46.

## Inputs Required

- The test client instance's address and every client instance's heartbeat
- Baseline performance data if previously benchmarked

## Outputs

- Canary report with initial health check

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 45 | Skill | contributes to `released` | GStack `/canary`, at the test client instance; App 5 heartbeats |

## Reference Files

| [[[pdlf:pdlf-library/policy-local/pol-anvil-platform\|Pol Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md) | Steps 17, 18, 29, 30, 32, 33, 41–45 |
| Standards Library | Steps 41–45 (deployment) |

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
