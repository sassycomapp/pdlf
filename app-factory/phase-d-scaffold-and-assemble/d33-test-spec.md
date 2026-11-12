---
title: "d33-test-spec"
doc-id: "mb-9089d388"
updated: "2026-11-12"
---
# Step 33: Pull to local — Test Specification

**Proves:** David's local app holds exactly what Anvil holds after the scaffold push, and validates.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\d33\`; every result is recorded in `{slug}-d33-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 32 is complete. |
| PR-10 | Only the stubs and `tests\ts-config.yaml` changed, apart from Anvil's formatting, and the app validates. |

**On failure:** The step stops with a deviation; the app is never corrected in this step.
