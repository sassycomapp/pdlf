---
title: "f42a-reference"
doc-id: "mb-89d4dfcf"
updated: "2026-11-08"
---

## Release regression test

## Task Execution Order

1. Confirm the test client instance runs the release image from Step 42.
2. Run the full integration/E2E suite against the test client instance — cross-feature
   flows across the whole application, not a single feature's Level 3 check.
3. → Decision point: if failures are found, present as a deviation request. Developer
   decides whether to fix before proceeding to the smoke test.
4. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
5. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level.

---

## Description

Whole-application verification on the test client instance, distinct from anything run
per-feature during the build loop. The smoke test (Step 43) confirms the instance is up;
this step confirms it behaves correctly across feature interactions, before App 5's
Release action moves any client.

## Inputs Required

- The test client instance, running the release image per Step 42
- Full application feature set (all features that reached `build-verified`)

## Outputs

- Integration/E2E test results for the whole application on the test client instance
- Deviation request, if failures are found

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 42A | GStack/OpenCode | | GStack/OpenCode |

---

## Handoff to Step 43

Step 43 (client instance check) proceeds only once this step's results are clean or any
deviations have been resolved.

---

## Reference

Design rationale — why the smoke test alone was judged insufficient:
[[[pdlf:pdlf-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md), updated 2026-07-12.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.
