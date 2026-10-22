---
title: "a10-test-spec"
updated: "2026-10-22"
doc-id: "mb-206988a2"
---
# Step 10: Entry point `update-management-app` — Test Specification

**Proves:** The entry starts from a recorded, healthy state.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a10\`.

| Test | Applied here |
|---|---|
| PR-01 | The entry record and step row are complete. |
| PR-02 | The health check passes before any work. |
| PR-08 | The whole suite of the app being changed passes; any failure is recorded as a finding. |
| LG-07 | When the work fixes a fault, a test that fails on the current code is written first. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
