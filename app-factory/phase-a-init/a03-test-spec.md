---
title: "a03-test-spec"
doc-id: "mb-b544c58e"
updated: "2026-10-29"
---
# Step 3: New application with context — Test Specification

**Proves:** The entry record is complete and true, and the run joins its route at Step 11, route B.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a03\`; every result is recorded in `{slug}-a03-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The `projects` row holds the slug, the name and the mode; the entry record names the apps that exist, the project context and the reference platform, each confirmed by David. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
