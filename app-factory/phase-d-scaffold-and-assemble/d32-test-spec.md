---
title: "d32-test-spec"
updated: "2026-10-23"
doc-id: "mb-4f9f675a"
---
# Step 32: Physical scaffold build — Test Specification

**Proves:** Every planned stub exists and validates, and nothing else.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\d32\`.

| Test | Applied here |
|---|---|
| ST-01 | The app validates. |
| ST-10 | Stubs equal the plan; Anvil's structure rules hold. |
| PR-06 | The developer committed and pushed. |

**On failure:** Missing or extra stubs are corrected before the push.
