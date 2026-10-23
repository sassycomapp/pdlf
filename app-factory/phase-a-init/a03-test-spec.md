---
title: "a03-test-spec"
updated: "2026-10-23"
doc-id: "mb-b544c58e"
---
# Step 3: Entry point `new-app-with-context` — Test Specification

**Proves:** The entry starts from a recorded, healthy state.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a03\`.

| Test | Applied here |
|---|---|
| PR-01 | The entry record and step row are complete. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
