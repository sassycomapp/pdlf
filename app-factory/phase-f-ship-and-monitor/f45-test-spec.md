---
title: "f45-test-spec"
updated: "2026-10-23"
doc-id: "mb-bae4b13c"
---
# Step 45: Production check — Test Specification

**Proves:** Released instances stay healthy and within their plan.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f45\`.

| Test | Applied here |
|---|---|
| RL-09 | Errors, speed and heartbeats against the baseline. |
| RL-12 | Clients within their plan limits. |
| RL-11 | The periodic checks are scheduled from this release. |
| PR-04 | Sentinel ran at Medium. |

**On failure:** Above the immediate thresholds, rollback at once.
