---
title: "step-42A-staging-integration-e2e"
doc-id: "mb-48ff7204"
updated: "2026-10-12"
---
## Task Execution Order

1. Confirm the Staging publish from Step 42 has completed.
2. Run the full integration/E2E suite against the Staging environment — cross-feature
   flows across the whole application, not a single feature's Level 3 check.
3. → Decision point: if failures are found, present as a deviation request. Developer
   decides whether to fix before proceeding to the smoke test.
4. Follow execution sequence in [[[makepdlf-project-library:specifications-local/spec-execution-discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).
5. Apply BFT per [[[makepdlf-project-library:specifications-local/spec-bft]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level.

---

## Description

Whole-application verification at Staging, distinct from anything run per-feature during
the build loop. Added specifically because the Staging smoke test (Step 43) alone was
found to verify too little — it confirms the app is up, not that it behaves correctly
across feature interactions. This step closes that gap before Production promotion.

## Inputs Required

- Staging environment, published per Step 42
- Full application feature set (all features that reached `build-verified`)

## Outputs

- Integration/E2E test results for the whole application at Staging
- Deviation request, if failures are found

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 42A | GStack/OpenCode | | GStack/OpenCode |

---

## Handoff to Step 43

Step 43 (Staging smoke test) proceeds only once this step's results are clean or any
deviations have been resolved.

---

## Reference

Design rationale — why the smoke test alone was judged insufficient:
[[[makepdlf-project-library:policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/pol-anvil-platform.md), updated 2026-07-12.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[makepdlf-project-library:specifications-local/spec-execution-discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[makepdlf-project-library:specifications-local/spec-bft]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.
