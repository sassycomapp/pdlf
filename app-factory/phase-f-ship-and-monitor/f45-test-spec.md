---
title: "f45-test-spec"
doc-id: "mb-bae4b13c"
updated: "2026-11-13"
---
# Step 45: Production Check — Test Specification

**Proves:** The released app stays healthy against its baseline, and the post-release security checks are done.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f45\`; every result is recorded in `{slug}-f45-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 44 is complete. |
| RL-09 | Errors, response times and heartbeats against the baseline. |
| RL-05 | Every client instance runs the release correctly. |
| RL-12 | Clients within their resources. |
| RL-11 | Periodic checks scheduled. |
| PR-04 | Sentinel ran at Medium. |

**On failure:** A rollback trigger rolls the release back at once; a finding goes to triage.
