---
title: "b15-test-spec"
updated: "2026-10-22"
doc-id: "mb-19e6d914"
---
# Step 15: Engineering review — Test Specification

**Proves:** The test plan, access matrix, threat model and security decisions are complete, and the plan obeys Mybizz's rules.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\b15\`.

| Test | Applied here |
|---|---|
| DC-04 | The test plan covers every critical flow and lifecycle, with catalogue test IDs. |
| DC-05 | `access-matrix.yaml` is complete and parses. |
| DC-06 | The threat model covers every trust boundary. |
| DC-07 | Sign-in, sessions, secrets, logging, limits, outbound hosts and packages are decided. |
| DC-08 | The common aspects are met; the conformance checks are selected; contradictions settled at their source. |
| PR-04 | Sentinel ran at High. |

**On failure:** Each failure is put to the developer and the plan corrected.
