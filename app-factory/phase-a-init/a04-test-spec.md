---
title: "a04-test-spec"
doc-id: "mb-1d584a36"
updated: "2026-10-29"
---
# Step 4: Feature for App 1 — Test Specification

**Proves:** The entry record is complete and true, the business is healthy, and the run joins its route at Step 12, route C.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\a04\`; every result is recorded in `{slug}-a04-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record holds the statement and the unique feature slug. |
| PR-02 | The health check passes before any work. |
| PR-08 | App 1's whole suite ran as the baseline; any failure is recorded as a finding of the existing app. |

**On failure:** The entry stops; nothing joins the pipeline until the failure is resolved.
