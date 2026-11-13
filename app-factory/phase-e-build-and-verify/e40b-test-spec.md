---
title: "e40b-test-spec"
doc-id: "mb-4997316e"
updated: "2026-11-13"
---
# Step 40B: Approved Fixes — Test Specification

**Proves:** Only the approved fixes were made, and every test passes again.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e40b\`; every result is recorded in `{slug}-e40b-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 40 is complete or skipped for the ticket. |
| PR-07 | No test weakened. |
| PR-08 | The whole suite passes. |

**On failure:** A failing test is diagnosed and fixed before David commits.
