---
title: "f43-test-spec"
doc-id: "mb-d5371799"
updated: "2026-11-13"
---
# Step 43: Client Instance Check — Test Specification

**Proves:** The test client instance runs the release healthily and its baseline is recorded.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f43\`; every result is recorded in `{slug}-f43-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 42A is complete. |
| RL-05 | Release version, schema and smoke test. |
| RL-10 | A new client starts secure, at a first release. |
| SC-14 | Client isolation holds. |

**On failure:** A failure rolls the test client instance back and stops the release.
