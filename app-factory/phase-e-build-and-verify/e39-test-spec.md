---
title: "e39-test-spec"
updated: "2026-10-22"
doc-id: "mb-0bff5864"
---
# Step 39: Triage — Test Specification

**Proves:** Every finding is decided and `build-verified` rests on the whole suite passing.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e39\`.

| Test | Applied here |
|---|---|
| PR-04 | Every finding of 35A to 38A is in `triage_findings`, resolved or declined. |
| PR-08 | The whole suite passes. |
| PR-05 | Receipts of Steps 35 to 38A match their evidence. |
| LG-07 | Every fixed finding has its test. |
| PR-03 | `build-verified` has the developer's approval. |

**On failure:** A finding for a fix returns the feature to Step 35.
