---
title: "a08-test-spec"
updated: "2026-10-22"
doc-id: "mb-210a9629"
---
# Step 8: Entry point `create-management-app` — Test Specification

**Proves:** The entry starts from a recorded, healthy state.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a08\`.

| Test | Applied here |
|---|---|
| PR-01 | The entry record and step row are complete. |
| PR-02 | The health check passes before any work. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
