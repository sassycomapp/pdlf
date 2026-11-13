---
title: "e37-test-spec"
doc-id: "mb-5a7320b0"
updated: "2026-11-13"
---
# Step 37: Code Review — Test Specification

**Proves:** The feature's changes meet Anvil's rules, the Mybizz standards and their ticket, its forms match their screen requirements, and its security has been reviewed independently.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e37\`; every result is recorded in `{slug}-e37-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 36 is complete for the ticket. |
| SC-15 | `code-review`, `/cso --diff` and Sentinel at Very High, each in its own session. |
| ST-02 | The scanner passes on the changed code (ST-02 to ST-12). |
| DC-13 | Each form and spec sheet matches its approved screen requirement; Anvil's agent changed only handler bodies. |
| ST-13 | bandit and `/cso` findings decided. |
| PR-04 | Sentinel ran at Very High; its row is recorded. |

**On failure:** Each finding goes to Step 39; nothing is fixed in this step.
