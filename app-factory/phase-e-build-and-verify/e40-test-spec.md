---
title: "e40-test-spec"
updated: "2026-10-22"
doc-id: "mb-57eabeaa"
---
# Step 40: Architecture scan — Test Specification

**Proves:** The scan reports with evidence and changes nothing.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e40\`.

| Test | Applied here |
|---|---|
| ST-10 | The code graph matches the scaffold plan; `git status` is unchanged. |

**On failure:** Any change is reverted.
