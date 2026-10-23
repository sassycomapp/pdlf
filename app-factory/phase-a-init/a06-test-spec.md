---
title: "a06-test-spec"
updated: "2026-10-23"
doc-id: "mb-daa547b4"
---
# Step 6: Entry point `compile-master-template` — Test Specification

**Proves:** The entry starts from a recorded, healthy state.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a06\`.

| Test | Applied here |
|---|---|
| PR-01 | The entry record and step row are complete. |
| PR-02 | The health check passes before any work. |
| PR-08 | The whole suite of the app being changed passes; any failure is recorded as a finding. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
