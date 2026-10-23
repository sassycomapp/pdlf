---
title: "f43-test-spec"
updated: "2026-10-23"
doc-id: "mb-d5371799"
---
# Step 43: Client instance check — Test Specification

**Proves:** Every client instance works on the release and has its baseline.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f43\`.

| Test | Applied here |
|---|---|
| RL-05 | Smoke test and management token on every instance. |
| RL-10 | Clients activated since the last release passed activation checks. |
| SC-14 | Keys and tokens unique; storage keys scoped. |

**On failure:** Rolled back at once above the immediate thresholds.
