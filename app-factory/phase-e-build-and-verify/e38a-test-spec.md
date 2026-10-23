---
title: "e38a-test-spec"
updated: "2026-10-23"
doc-id: "mb-c66ffc80"
---
# Step 38A: Dependency check — Test Specification

**Proves:** Anvil's own report of the server packages is captured and its findings recorded.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e38a\`.

| Test | Applied here |
|---|---|
| ST-13 | Anvil's package report agrees with pip-audit; findings recorded. |

**On failure:** Findings go to Step 39.
