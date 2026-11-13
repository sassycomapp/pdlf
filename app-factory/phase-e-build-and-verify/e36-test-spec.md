---
title: "e36-test-spec"
doc-id: "mb-45226792"
updated: "2026-11-13"
---
# Step 36: Design Review — Test Specification

**Proves:** Each form matches its approved screen requirement in every width, mode and role, uses the theme fully and is accessible.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e36\`; every result is recorded in `{slug}-e36-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 40B is complete or skipped for the ticket. |
| BR-04 | Each form matches its approved screen requirement, at phone and desktop width, in light and dark mode. |
| BR-05 | Keyboard, focus, names, error messages. |
| BR-03 | Each role sees only its forms. |
| DC-16 | Theme usage: no plainer component where the requirement names a better one. |
| SC-09 | Nothing sensitive in addresses or browser storage. |

**On failure:** Each finding goes to Step 39; nothing is fixed in this step.
