---
title: "f46-test-spec"
doc-id: "mb-99b08d56"
updated: "2026-11-13"
---
# Step 46: Learning — Test Specification

**Proves:** Every lesson is written into the source the next build reads and submitted to GBrain, and `released` has David's approval.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f46\`; every result is recorded in `{slug}-f46-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 45 is complete. |
| DC-15 | Each lesson written into its source. |
| LG-07 | Each fixed problem has its test. |
| PR-03 | The `released` gate row was written by David's `pdlf-gate.sh`. |

**On failure:** A lesson not yet written into its source keeps the gate shut.
