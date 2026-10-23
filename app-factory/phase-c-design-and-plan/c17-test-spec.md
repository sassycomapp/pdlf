---
title: "c17-test-spec"
updated: "2026-10-23"
doc-id: "mb-957fb9e3"
---
# Step 17: Create Anvil data tables — Test Specification

**Proves:** The schema is exactly the locked data design and obeys the data rules.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c17\`.

| Test | Applied here |
|---|---|
| ST-01 | `anvil.yaml` validates. |
| ST-07 | Client access none, `created_at`, metadata columns, log tables, no secret columns, datetimes. |
| ST-06 | No tenant-style column. |
| DC-05 | Every table's access is in the access matrix; after Step 18 the tables equal the data design. |
| PR-04 | Sentinel ran at High. |

**On failure:** A difference stops the step; the schema is corrected and applied again.
