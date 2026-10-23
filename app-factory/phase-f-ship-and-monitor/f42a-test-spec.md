---
title: "f42a-test-spec"
updated: "2026-10-23"
doc-id: "mb-1d651bfe"
---
# Step 42A: Release regression test — Test Specification

**Proves:** Every feature works on App 2 as released.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\f42a\`.

| Test | Applied here |
|---|---|
| RL-06 | All flows on App 2; public pages and checkout in Chrome, Firefox and Safari. |
| SC-09 | Released headers and TLS correct. |

**On failure:** Rolled back at Step 42.
