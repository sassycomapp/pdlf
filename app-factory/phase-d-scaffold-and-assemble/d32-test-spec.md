---
title: "d32-test-spec"
doc-id: "mb-4f9f675a"
updated: "2026-11-12"
---
# Step 32: Create the scaffold — Test Specification

**Proves:** Every planned stub exists and validates, nothing unplanned was created, and the scanner's settings match the plan.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\d32\`; every result is recorded in `{slug}-d32-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 31 is complete. |
| ST-01 | The app validates. |
| ST-10 | The structure rules hold; `tests\ts-config.yaml` matches the scanner settings. |
| Stubs equal the plan | Every planned module and function exists; nothing exists that `scaffold-spec.md` does not name. |
| PR-06 | David committed and pushed; no secret was published. |

**On failure:** A failure in a file this step created is corrected before the push; a failure in an existing file is recorded for Step 34.
