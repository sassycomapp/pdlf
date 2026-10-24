---
title: "b15-test-spec"
updated: "2026-10-24"
doc-id: "mb-19e6d914"
---
# Step 15: Engineering review — Test Specification

**Proves:** The architecture fits Anvil and obeys Mybizz's rules, and its test plan, access matrix, threat model and security decisions are complete and approved by David.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\b15\`; the DC results are written to `{slug}-b15-{run}-dc-checks.md`, each with the section or file that shows it.

| Test | Applied here |
|---|---|
| PR-01 | The entry record is complete and Step 14 is complete, with its reviewed plan approved. |
| DC-04 | `test-plan.md` gives every critical flow its preconditions, steps with expected results, performance budget and data checks, its edge cases and error paths, and the catalogue test IDs it uses; every lifecycle is a state machine with allowed and forbidden transitions. |
| DC-05 | The app's `access-matrix.yaml` lists every server function the architecture names and every form and settings tab the plan names, against every role, with readable and writable fields; it parses. |
| DC-06 | `threat-model.md` lists every trust boundary with its threats, control, owner, governing document and test IDs. |
| DC-07 | The Security Decisions section states the sign-in and second-factor rules, session periods, every secret with its home and maximum age, the security events logged, the limits on expensive functions, every outbound host and every server package with its review. |
| DC-08 | Each of the 14 common aspects names where it is met or its ADR; the conformance checks that apply are listed in `test-plan.md`; every contradiction between rules is settled at its source. |
| DC-01 | Every requirement and acceptance criterion the step added is testable. |
| PR-06 | No secret is in any document the step wrote or in `pdlf-outputs\b15\` (gitleaks on the project library's working tree). |
| PR-04 | Sentinel ran at High. |

**On failure:** Each failure is put to David and the documents corrected and checked again; a secret found is removed before the step ends.
