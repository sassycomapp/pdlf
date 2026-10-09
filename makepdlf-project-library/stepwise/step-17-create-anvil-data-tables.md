---
title: "step-17-create-anvil-data-tables"
doc-id: "mb-38d4d62e"
updated: "2026-10-09"
---
## Task Execution Order

1. Developer: Build data tables/schema in the Anvil IDE per the ADRs and authoritative schema
2. Follow execution sequence in [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
3. Apply BFT per [[[pdlf:makepdlf-project-library/specifications-local/spec-bft]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level (Light)

---

## Description

Developer builds the actual data tables/schema in the Anvil IDE, matching the
ADRs and authoritative schema from Steps 15–16.

## Inputs Required

- ADRs + CONTEXT.md from Step 16
- Authoritative schema from Step 15's TDD cluster

## Outputs

- Live data tables in the Anvil IDE (not local files)

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 17 | Manual | | Developer, in Anvil IDE |

## Reference Files

| [[[pdlf:makepdlf-project-library/policy-local/pol-anvil-platform\|Pol Anvil Platform]]](C:/pdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md) | Steps 17, 18, 29, 30, 32, 33, 41–45 |
| Standards Library | Steps 17/29/32 (platform) |

Anvil integration is governed by [[[pdlf:makepdlf-project-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md) in full — the detailed reference (the earlier `stepwise/step-6-24-anvil-integration.md` pointer was retired 2026-07-18: the file was never created; its intended content lives in the policy).

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:makepdlf-project-library/specifications-local/spec-bft]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
