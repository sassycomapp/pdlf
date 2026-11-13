---
title: "e39-build-plan"
doc-id: "mb-011df646"
updated: "2026-11-13"
---
# Step 39 — Triage: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`. This step ends each ticket with the gate `build-verified`.

#### Step 39: Triage

**Must achieve:** every finding of Steps 35A to 38A for the feature sorted and decided, every fix returned to Step 35 and retested, the whole suite passing, the ticket and its rework items closed, and the feature locked by David at the gate `build-verified`, so that the next feature may start.

**Starts from:** the findings of Steps 35A, 36, 37, 38 and 38A; `triage_findings` for the ticket; the ticket.

**Produces:** every finding labelled and decided; the ticket closed; the `gates` row of `build-verified` for the ticket; in `pdlf-outputs\e39\`: the triage record, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with Matt Pocock's `triage`. David decides each finding he is asked about and passes or blocks the gate.

**Must be built so that:**
- `triage` sorts every finding with the label vocabulary set at Step 11, and writes its decision to `triage_findings`;
- a finding labelled for a fix returns the feature to Step 35, where `diagnosing-bugs` finds its root cause and a test is added for it (test LG-07); Steps 35A to 38A then run again for the ticket;
- the whole suite passes before the gate (test PR-08), and no test was weakened;
- the receipts of Steps 35 to 38A of the ticket match their evidence (test PR-05);
- every row of `triage_findings` for the ticket is resolved or labelled `wontfix` with David's reason;
- the ticket is closed in `pdlf-tickets\`, and its items on the rework list are marked cleared;
- the gate follows `spec-gate-procedure`: Full BFT, the gate summary block, and David's explicit yes or no; on yes David records his approval with `pdlf-gate.sh`, naming the ticket, and the agent reads the row; the agent never writes it;
- Step 41 begins only when every ticket of the run has passed `build-verified`;
- its ledger row carries the ticket, with `step_type = 'gate'`, `skill_family = 'matt-skills'`, `synthesized = false`, and `inputs_used` naming Steps 35 to 38A.

**BFT level:** Full (gate).

**Gate:** `build-verified`, for this ticket: the feature is signed off and the next feature may start.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md); [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `triage` (Matt Pocock): every finding labelled and decided → `triage_findings`, then the gate.
- `diagnosing-bugs` (Matt Pocock): the root cause of every fix returned to Step 35 → the fix and its test.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e39-test-spec|Step 39 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e39-test-spec.md).

**Standards:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md) section 6.

## Why it is built this way

- **Every finding decided.** A finding is fixed or declined with a reason; none is left open.
- **Fixed at the source.** A fix is made in the build step, with its own test, and every check runs again.
- **One feature at a time.** The next feature starts only when this one is locked, so problems never pile up across features.
