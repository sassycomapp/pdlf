---
title: "f44-test-spec"
doc-id: "mb-d92170d3"
updated: "2026-11-13"
---
# Step 44: Release — Test Specification

**Proves:** The release had David's approval on clean evidence, and reached every client stage by stage, or App 5's version was published.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f44\`; every result is recorded in `{slug}-f44-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 43 is complete or skipped. |
| RL-01 | No open finding. |
| PR-05 | The receipts of Steps 41 to 43 match their evidence. |
| PR-03 | The `production-released` gate row was written by David's `pdlf-gate.sh`. |
| Staged release | Each stage passed its health check before the next, for App 1. |

**On failure:** An open finding or failed stage stops the release; a failed stage rolls back by itself.
