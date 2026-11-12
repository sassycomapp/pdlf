---
title: "d31-test-spec"
doc-id: "mb-c262a8da"
updated: "2026-11-12"
---
# Step 31: Scaffold plan — Test Specification

**Proves:** Every function the screens and tickets need is planned, each with its module, access rule and test, and every existing module has its disposition.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\d31\`; every result is recorded in `{slug}-d31-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete, Step 26 is complete and `screens-approved` is passed. |
| DC-10 | Every ticket traces to planned functions; every server function a screen requirement names is planned under its name; every planned function has its access rule and a test ID. |
| Disposition | For an existing app, every existing module and server function is keep, rework or remove, and every rework and removal names its ticket. |

**On failure:** `scaffold-spec.md` or the disposition list is corrected and checked again before the step ends.
