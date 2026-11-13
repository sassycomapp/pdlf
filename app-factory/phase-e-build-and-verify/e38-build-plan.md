---
title: "e38-build-plan"
doc-id: "mb-8b5ce355"
updated: "2026-11-13"
---
# Step 38 — Quality Testing: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`.

#### Step 38: Quality testing

**Must achieve:** the feature tested as users will use it, every action of every spec sheet giving its stated result, every earlier feature still working, and its pages fast enough; with every finding recorded and a clean-pass statement when there is none.

**Starts from:** the feature after Step 37; the spec sheets of the ticket's forms; the test plan's critical flows; every earlier signed-off feature.

**Produces:** the quality findings; the performance results; in `pdlf-outputs\e38\`: the findings, the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode, with GStack's `/qa-only` and `benchmark`, and `mb-sentinel-review`.

**Must be built so that:**
- `/qa-only` carries out every action of every spec sheet of the feature, on hosted App {n} with `TEST_` data only, signed in as each role and signed out for public pages, and checks each gives the result its spec sheet states;
- `/qa-only` runs every flow of every earlier signed-off feature again, and checks the browser console shows no error and only approved hosts are contacted;
- payments are tested end to end in test mode when the feature touches them;
- `benchmark` measures each of the feature's pages against its performance budget;
- every finding goes to the findings file with its evidence and severity; with none, the file states a clean pass; nothing is fixed in this step; `TEST_` data is removed afterwards;
- `mb-sentinel-review` runs at High scrutiny on the findings;
- its ledger row carries the ticket, with `step_type = 'skill'`, `skill_family = 'gstack'`, `synthesized = false`, and `inputs_used` naming Step 37.

**BFT level:** Full.

**Gate:** none.

**References:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `/qa-only` (GStack), report only: every spec-sheet action, every earlier flow → the findings, then Step 39.
- `benchmark` (GStack): each page against its budget → the findings, then Step 39.
- `mb-sentinel-review`, High → `triage_findings`.

**Not used:** GStack's `/qa`, because it commits its own fixes; agents never commit.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e38-test-spec|Step 38 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e38-test-spec.md).

**Standards:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md); [[[default:specifications-global/spec-testing-methodology-standards|Testing Methodology Standards]]](C:/dev/project-library-global/specifications-global/spec-testing-methodology-standards.md).

## Why it is built this way

- **The spec sheet is the contract.** Each action it lists must give its stated result for the feature to be done.
- **Nothing earlier broken.** Every signed-off feature is tested again, so a new feature cannot quietly break an old one.
- **Fast enough.** Performance is measured, not assumed.
