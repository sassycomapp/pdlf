---
title: "c20-test-spec"
doc-id: "mb-8714471c"
updated: "2026-11-12"
---
# Step 20: Design system — Test Specification

**Proves:** The design system is readable in light and dark mode, stays within `m3-custom-theme`, and states the full-theme rule.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\c20\`; every result is recorded in `{slug}-c20-{run}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 19 is complete. |
| DC-12 | The chosen palette reaches WCAG 2.2 AA contrast in light and dark mode; excluded components are named; no colour, font size or spacing value is defined in `DESIGN.md`. |
| PR-04 | Sentinel ran at Medium, and any Flag or Escalate has David's decision. |

**On failure:** `DESIGN.md` is corrected with David and checked again before the step ends.
