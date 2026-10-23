---
title: "spec-pdlf-process-tests"
doc-id: "mb-b514a377"
updated: "2026-10-23"
---
# Spec: PDLF Process Tests

## What it is

The PR tests prove that PDLF ran a step correctly and that its records are true. They sit beside the test suite's catalogue ([[[default:test-suite/ts-catalogue|Test Suite — Catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md)), which proves the application itself. A step's test specification names tests from both by their IDs. They are run, and their evidence is saved, as the test suite's method sets out ([[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md)).

## The PR tests

| ID | Test | Passes when | Level · where | Basis |
|---|---|---|---|---|
| PR-01 | The step starts from the right state | The entry record and step row are complete, and every step the run plan names as a dependency is complete | D · ledger | [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md); the run plan |
| PR-02 | The health check passes | Every check of the health check SOP passes before work on an existing app | 0 · WSL | [[[pdlf:pdlf-library/operating-procedures/sop-health-check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) |
| PR-03 | A gate cannot pass without the developer | An agent's attempt to pass a gate is blocked by Cupcake, and every passed gate has the developer's approval | 0 · ledger, Cupcake log | [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md) |
| PR-04 | The security review ran | Sentinel's row for the step is in `triage_findings`, and any Flag or Escalate has the developer's decision | D · ledger | `mb-sentinel-review` |
| PR-05 | The receipt matches its evidence | `ts_report.py --check` passes on the step's receipt | D · output folder | [[[default:test-suite/ts-method]]](C:/dev/project-library-global/test-suite/ts-method.md) rule 2 |
| PR-06 | No agent committed and no secret was published | Every commit is the developer's; gitleaks finds no secret in the working tree or history of any repository the step touched | 0 · WSL | `rules-cupcake-global`; [[[default:security-global/secrets/sec-secret-exposure-response]]](C:/dev/project-library-global/security-global/secrets/sec-secret-exposure-response.md) |
| PR-07 | No test was weakened or silenced | Compared with the last signed-off state, no test or assertion was removed or loosened, and no skip, `noqa` or `nosec` was added, unless the developer approved it | 0 · `tests\` diff | `no_test_tampering`, `no_suppression_directives_without_approval` |
| PR-08 | The whole suite passes | The scanner, `anvil --json validate .`, and the logic, integration and security suites all pass; before a change, a failure is recorded as a finding of the existing app | 0–2 · WSL, local runtime | [[[default:test-suite/ts-method]]](C:/dev/project-library-global/test-suite/ts-method.md) rule 9 |
| PR-09 | The local test environment works | The local runtime starts App 1 on an empty database; both Uplink connections work; a `TEST_` user signs in with a second factor; the mail catcher receives an email | 0 · WSL | [[[default:test-suite/ts-method]]](C:/dev/project-library-global/test-suite/ts-method.md) section 3 |
| PR-10 | The pull holds the expected change | After a pull, only the expected files changed (plus Anvil's formatting) and the app validates | 0 · App 1 repository | the Step 18 pull procedure |

## Why it works this way

The application's tests describe what a good Mybizz application is, so they live in `project-library-global`. The PR tests describe how PDLF itself must behave, so they live with PDLF.
