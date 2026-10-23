---
title: "e36-test-spec"
updated: "2026-10-23"
doc-id: "mb-45226792"
---
# Step 36: Design review — Test Specification

**Proves:** The feature, as it will ship, looks as approved and is accessible.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e36\`.

| Test | Applied here |
|---|---|
| BR-04 | Matches approved screens, both widths, light and dark. |
| BR-05 | Keyboard, focus, labels, error messages. |
| BR-03 | Each role sees only its forms. |
| SC-09 | Nothing sensitive in addresses or browser storage. |

**On failure:** Findings go to `step-36-findings.md` and Step 39.
