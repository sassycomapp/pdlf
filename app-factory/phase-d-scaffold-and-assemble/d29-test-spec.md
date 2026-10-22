---
title: "d29-test-spec"
updated: "2026-10-22"
doc-id: "mb-e4e104aa"
---
# Step 29: Build UI forms — Test Specification

**Proves:** Every approved screen has a form that validates and obeys the UI rules, and the schema is unchanged.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\d29\`.

| Test | Applied here |
|---|---|
| ST-01 | The app validates (checked after Step 30's pull). |
| ST-11 | Material 3 only, no banned components or hard-coded colours, `wrap_on`, loop handlers, no `navigate_to`. |
| ST-07 | The schema equals Step 17's: Anvil's AI changed no table. |

**On failure:** The form is corrected in the editor and pulled again.
