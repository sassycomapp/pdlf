---
title: "a02-test-spec"
doc-id: "mb-f267b498"
updated: "2026-10-29"
---
# Step 2: New application, no context — Test Specification

**Proves:** The entry record is complete and true, and the run joins its route at Step 11, route A.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a02\`; every result is recorded in `{slug}-a02-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The `projects` row holds the slug, the name and the mode, and the entry row holds the entry record. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
