---
title: "d34-test-spec"
updated: "2026-10-22"
doc-id: "mb-97443c97"
---
# Step 34: Architectural sanity audit — Test Specification

**Proves:** The skeleton passes every static check and implements the threat model's controls before code is written.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\d34\`.

| Test | Applied here |
|---|---|
| ST-01 | The whole app validates. |
| ST-02 | Access, matrix and rate limits. |
| ST-03 | Secrets. |
| ST-04 | Dangerous code. |
| ST-05 | Error handling. |
| ST-06 | No client separation. |
| ST-07 | Schema rules. |
| ST-08 | Money and time. |
| ST-09 | Integration patterns. |
| ST-10 | Structure. |
| ST-11 | UI rules. |
| ST-12 | Sign-in settings. |
| ST-13 | bandit, pip-audit and `/cso` clean. |
| DC-06 | Every trust boundary's control exists in the skeleton. |
| DC-08 | The skeleton obeys the common aspects; App 3 needs no code. |
| PR-04 | Sentinel ran at Very High; no finding open. |
| PR-03 | `architecture-verified` has the developer's approval. |

**On failure:** Any failure blocks the gate; the fault is corrected at its step and Step 34 runs again.
