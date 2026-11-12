---
title: "c22-test-spec"
doc-id: "mb-868d36a0"
updated: "2026-11-12"
---
# Step 22: Screen requirements — Test Specification

**Proves:** Every form the tickets name has a complete screen requirement built from the whole theme, and the access matrix lists every form.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c22\`; every result is recorded in `{slug}-c22-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete, Step 21 is complete and `concept-locked` is passed. |
| DC-16 | Every form the tickets name has its screen requirement; every section is filled; every element names a theme component, or an approved standard component, with its reason; every property is in the theme's documentation; every data column is in the authoritative schema; every text is a phrase key; every role has a scope. |
| DC-05 | Every form is in `access-matrix.yaml`, keyed by module path, with a scope for every role. |

**On failure:** The screen requirement or the access matrix is corrected and checked again before the step ends.
