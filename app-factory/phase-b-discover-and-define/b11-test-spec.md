---
title: "b11-test-spec"
updated: "2026-10-24"
doc-id: "mb-ec4af50a"
---
# Step 11: Init — Test Specification

**Proves:** The business's repositories, project library, ledger row and GBrain source are sound, nothing secret is public, and the app worked on is ready to be tested.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\b11\`.

| Test | Applied here |
|---|---|
| PR-01 | The `projects` row and the entry record are complete. |
| ST-01 | The cloned app validates with `anvil --json validate .`. |
| ST-12 | The app's Users service has the sign-in settings of `spec-security`. |
| ST-10 | The app's `.gitignore` covers `.env` and caches; an app that holds code has `tests\` with `conftest.py`, `pytest.ini`, `ts-config.yaml` and `integration\test_pr09_environment.py`; App 3 holds no code. |
| PR-09 | For an app that holds code: the local runtime starts it on an empty database, both Uplink connections work, a `TEST_` user signs in with a second factor, and the mail catcher receives an email (`test_pr09_environment.py`, run through `ts_local.sh`). |
| PR-06 | No secret is in any repository the step created or touched; `.env` is not tracked. |
| PR-04 | Sentinel ran at High. |
| PR-02 | The health check passes as the step's self-audit. |

**On failure:** The step stops with a deviation; a published secret is removed and rotated before the step ends.
