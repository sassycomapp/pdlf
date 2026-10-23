---
title: "f46-test-spec"
updated: "2026-10-23"
doc-id: "mb-99b08d56"
---
# Step 46: Learning — Test Specification

**Proves:** Every escaped fault is turned into a test and a corrected rule.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f46\`.

| Test | Applied here |
|---|---|
| DC-15 | Every lesson has its root cause, test and corrected document. |
| LG-07 | Each escaped fault's test fails without its fix. |
| PR-03 | `released` has the developer's approval. |

**On failure:** The gate stays closed until every lesson is complete.
