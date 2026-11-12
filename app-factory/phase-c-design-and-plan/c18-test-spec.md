---
title: "c18-test-spec"
doc-id: "mb-369422b2"
updated: "2026-11-12"
---
# Step 18: Pull to local — Test Specification

**Proves:** David's local the app holds exactly what Anvil holds, with only the expected change, and validates.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c18\`; every result is recorded in `{slug}-c18-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 17 is complete. |
| PR-10 | Only the expected files changed, and the app validates. |

**On failure:** The step stops with a deviation; the app is never corrected in this step.
