---
title: "d31-test-spec"
updated: "2026-10-22"
doc-id: "mb-c262a8da"
---
# Step 31: Scaffold planning — Test Specification

**Proves:** Every stub is planned with its module, seam, access rule and test, and the scanner's settings match the plan.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\d31\`.

| Test | Applied here |
|---|---|
| DC-10 | Every ticket traces to stubs and every stub to a test ID. |
| ST-10 | `tests\ts-config.yaml` matches the plan's modules, decorators and endpoints. |

**On failure:** The plan is corrected before Step 32.
