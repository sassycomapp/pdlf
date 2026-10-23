---
title: "e37-test-spec"
updated: "2026-10-23"
doc-id: "mb-5a7320b0"
---
# Step 37: Code review — Test Specification

**Proves:** The changes are reviewed independently and still pass every static check.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e37\`.

| Test | Applied here |
|---|---|
| SC-15 | `code-review`, `/cso --diff` and Sentinel at Very High, each in its own session. |
| ST-02 | The scanner passes on the changed code (ST-02 to ST-12). |
| ST-13 | bandit and `/cso` findings decided. |
| PR-04 | Sentinel's row recorded. |

**On failure:** Findings go to `step-37-findings.md` and Step 39.
