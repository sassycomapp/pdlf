---
title: "e35a-build-plan"
doc-id: "mb-cc2d83a1"
updated: "2026-11-13"
---
# Step 35A — Testing: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`.

#### Step 35A: Testing

**Must achieve:** the feature tested more widely than its build: every edge case, integration and security test the test plan gives it, its tests checked for weak or duplicate cases, and the tools and packages it brings checked for supply-chain risk.

**Starts from:** the feature as built at Step 35; the test plan; the app's `tests\`.

**Produces:** the feature's added tests; the test audit; the package and supply-chain findings in `triage_findings`; in `pdlf-outputs\e35a\`: the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with the skills below.

**Must be built so that:**
- `tdd` extends the feature's tests to every edge case, integration test and security test the test plan names for its ticket, at Levels 1 and 2;
- `test-audit` reports weak or duplicate tests in the feature's tests; each is strengthened or removed with David's approval, and no test is weakened;
- `pip-audit` checks the development and test tools, and `/cso --supply-chain` checks the feature's dependencies and tooling; every finding goes to `triage_findings`;
- its ledger row carries the ticket, with `step_type = 'skill'`, `skill_family = 'matt-skills'`, `synthesized = false`, and `inputs_used` naming Step 35.

**BFT level:** Light.

**Gate:** none.

**References:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `tdd` (Matt Pocock): the edge-case, integration and security tests → Step 38, then Step 39.
- `test-audit` (GStack), report only: weak or duplicate tests → their correction, then Step 39.
- `/cso --supply-chain` (GStack): the feature's dependencies and tooling → `triage_findings`, then Step 39.
- `pip-audit` (a tool): the development and test tools → `triage_findings`.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e35a-test-spec|Step 35A Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e35a-test-spec.md).

**Standards:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md); [[[default:specifications-global/spec-testing-methodology-standards|Testing Methodology Standards]]](C:/dev/project-library-global/specifications-global/spec-testing-methodology-standards.md).

## Why it is built this way

- **Wider than the build.** Step 35 proves the feature works; this step proves it holds under edge cases, failures and attack.
- **Tests that test something.** A weak or duplicate test gives false comfort; auditing them keeps the suite honest.
