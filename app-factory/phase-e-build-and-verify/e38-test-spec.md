---
title: "e38-test-spec"
doc-id: "mb-4ca3ae2d"
updated: "2026-11-13"
---
# Step 38: Quality Testing — Test Specification

**Proves:** Every spec-sheet action gives its stated result, every earlier feature still works, and the feature's pages meet their performance budget.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e38\`; every result is recorded in `{slug}-e38-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 37 is complete for the ticket. |
| BR-01 | Every flow end to end. |
| BR-02 | Edge cases and errors. |
| BR-03 | Roles. |
| BR-06 | Performance budgets, measured by `benchmark`. |
| BR-07 | Earlier features, console, hosts. |
| BR-08 | Payments in test mode, when touched. |
| SC-10 | Payment pages and card data, when touched. |
| IN-18 | Hosted test data removed. |
| PR-04 | Sentinel ran at High. |

**On failure:** Each finding goes to Step 39; nothing is fixed in this step.
