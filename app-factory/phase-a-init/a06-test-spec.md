---
title: "a06-test-spec"
doc-id: "mb-daa547b4"
updated: "2026-10-29"
---
# Step 6: Release into App 2 — Test Specification

**Proves:** The entry record is complete and true, the business is healthy, and the run joins its route at Step 41.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a06\`; every result is recorded in `{slug}-a06-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete. |
| PR-02 | The health check passes before any work. |
| PR-08 | App 1's whole suite passes. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
