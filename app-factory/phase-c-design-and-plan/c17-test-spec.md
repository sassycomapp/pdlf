---
title: "c17-test-spec"
updated: "2026-11-12"
doc-id: "mb-957fb9e3"
---
# Step 17: Create Anvil data tables — Test Specification

**Proves:** The app's schema is exactly the authoritative schema, obeys the data rules, and is applied to the live tables.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c17\`; every result is recorded in `{slug}-c17-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete, Step 16 is complete and the gate `domain-locked` is passed. |
| Theme copies current | The app's `tests\component-inventory.yaml` equals the theme's, and the theme keys of `tests\ts-config.yaml` equal the template's. |
| ST-01 | `anvil --json validate anvil.yaml` reports no error. |
| ST-06 | No table or column separates clients. |
| ST-07 | Every table refuses client access and has `created_at`; every core table has `metadata`; the five log and control tables exist; no column holds a secret; times are datetimes. |
| Schema match | `db_schema` in `anvil.yaml` equals the authoritative schema, table by table and column by column; evidence: the difference list, empty after step 14 of the reference. |
| Applied | David confirms the Data Tables view reports no schema mismatch; every removal and type change on the difference list was checked by him by name. |
| PR-04 | Sentinel ran at High, and any Flag or Escalate has David's decision. |

**On failure:** A difference or a failed rule stops the step; the authoritative schema or `anvil.yaml` is corrected and the check is run again. A mismatch David reports after Resolve that the difference list does not hold is a deviation.
