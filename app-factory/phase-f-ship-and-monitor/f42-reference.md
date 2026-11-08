---
title: "f42-reference"
doc-id: "mb-8ad89930"
updated: "2026-11-08"
---

## Release to App 2

## Task Execution Order

1. Every client instance copies its data to its own R2 bucket
2. Developer: Push App 1's tagged release into App 2's repository, and write the release's table changes into App 3's table definitions
3. The image build workflow in `{slug}-app4` builds and checks the release image, and stores it under the release tag
4. The whole test suite runs on the release image
5. App 5 moves the test client instance to the release image
6. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
7. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) at assigned level (None)

---

## Description

The developer pushes the release into App 2 and App 3. The release image is built,
checked and tested, and only the test client instance runs it.

## Outputs

- The release image, stored under the release tag
- The test client instance running the release image

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 42 | Manual | | Release to App 2 and build the release image |

## Reference Files

| [[[pdlf:pdlf-library/policy-local/pol-anvil-platform\|Pol Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md) | Steps 17, 18, 29, 30, 32, 33, 41–45 |
| Standards Library | Steps 41–45 (deployment) |

Anvil integration is governed by [[[pdlf:pdlf-library/policy-local/pol-anvil-platform|Policy: Anvil Platform]]](C:/pdlf/pdlf-library/policy-local/pol-anvil-platform.md) in full — the detailed reference (the earlier `stepwise/step-6-24-anvil-integration.md` pointer was retired 2026-07-18: the file was never created; its intended content lives in the policy).

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
