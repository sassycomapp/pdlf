---
title: "b11-test-spec"
updated: "2026-10-23"
doc-id: "mb-ec4af50a"
---
# Step 11: Init — Test Specification

**Proves:** The business's repositories, project library, ledger row and GBrain source are sound, nothing secret is public, and every app is ready to be tested.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\b11\`.

| Test | Applied here |
|---|---|
| PR-01 | The `projects` row is complete. |
| PR-09 | The local runtime, both Uplink connections, a `TEST_` user with a second factor and the mail catcher all work. |
| PR-06 | No secret is in any repository the step created or touched. |
| ST-10 | Every app's `.gitignore` covers `.env` and caches; `tests\` holds the four templates. |
| PR-04 | Sentinel ran at High. |
| PR-02 | The health check passes as the step's self-audit. |

**On failure:** The step stops with a deviation; a published secret is removed and rotated before the step ends.
