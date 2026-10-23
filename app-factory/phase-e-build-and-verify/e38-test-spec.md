---
title: "e38-test-spec"
updated: "2026-10-23"
doc-id: "mb-4ca3ae2d"
---
# Step 38: Quality testing — Test Specification

**Proves:** The feature works for real users, and every earlier feature still works.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e38\`.

| Test | Applied here |
|---|---|
| BR-01 | Every flow end to end. |
| BR-02 | Edge cases and errors. |
| BR-03 | Roles. |
| BR-06 | Performance budgets. |
| BR-07 | Earlier features, console, hosts. |
| BR-08 | Payments in test mode, when touched. |
| SC-10 | Payment pages and card data, when touched. |
| PR-04 | Sentinel ran at High. |

**On failure:** Findings go to `step-38-findings.md` and Step 39.
