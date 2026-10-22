---
title: "a09-test-spec"
updated: "2026-10-22"
doc-id: "mb-1de3b3eb"
---
# Step 9: Entry point `add-feature-management-app` — Test Specification

**Proves:** The entry starts from a recorded, healthy state.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a09\`.

| Test | Applied here |
|---|---|
| PR-01 | The entry record and step row are complete. |
| PR-02 | The health check passes before any work. |
| PR-08 | The whole suite of the app being changed passes; any failure is recorded as a finding. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
