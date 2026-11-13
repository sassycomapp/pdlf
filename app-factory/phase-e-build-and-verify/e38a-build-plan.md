---
title: "e38a-build-plan"
doc-id: "mb-df4a6f60"
updated: "2026-11-13"
---
# Step 38A — Package Check: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`.

#### Step 38A: Package check

**Must achieve:** Anvil's own security check of the server packages captured, when the server environment was rebuilt for the feature, and each finding recorded for triage.

**Starts from:** the app's server environment in Anvil; the result of `pip-audit` at Step 35A.

**Produces:** the package report; its findings in `triage_findings`; in `pdlf-outputs\e38a\`: the report, the test results and the Step Receipt; the ledger row.

**Carried out by:** OpenCode; David copies Anvil's report from the Anvil editor.

**Must be built so that:**
- when the feature rebuilt the server environment, David copies Anvil's package report from the Anvil editor, following the agent's instructions, into the step folder; when it did not, the step is recorded `skipped`;
- the report is compared with Step 35A's `pip-audit` result; every finding goes to `triage_findings`;
- its ledger row carries the ticket, with `step_type = 'manual'`, `skill_family = 'manual'`, `synthesized = false`, and `inputs_used` naming Step 38.

**BFT level:** None.

**Gate:** none.

**References:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** None; the step records Anvil's own result.

**Layers with no skill:** all; the step only records.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e38a-test-spec|Step 38A Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38a-test-spec.md).

**Standards:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md) section 9.

## Why it is built this way

- **Anvil's view of the packages.** Anvil checks the packages it actually runs; recording its result closes the gap between local tools and the live environment.
