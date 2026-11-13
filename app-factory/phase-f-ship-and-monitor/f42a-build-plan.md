---
title: "f42a-build-plan"
doc-id: "mb-f3b31ed1"
updated: "2026-11-13"
---
# Step 42A — Release Regression: Build Plan

## Step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). For App 1, the release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md)). For App 5, Mybizz's own management app, the release is its tagged version published in Anvil; Steps 42, 42A and 43 are recorded `skipped`.

#### Step 42A: Release regression

**Must achieve:** every feature of the release tested on the test client instance running the release image, in Chrome, Firefox and Safari, with the release's dynamic security scan clean.

**Starts from:** the test client instance on the release image; the test plan's critical flows.

**Produces:** the regression findings; the dynamic scan result; in `pdlf-outputs\f42a\`: the findings, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with the skills below.

**Must be built so that:**
- `/qa-only` runs every feature's flows on the test client instance, signed in as each role and signed out, in Chrome, Firefox and Safari (RL-06);
- `security-audit-methodology` runs the release part of Step 15's assessment plan: the dynamic scan of the release image, with no high or medium alert left open (SC-18);
- nothing sensitive appears in page addresses or browser storage (SC-09);
- every finding is recorded; a failure moves the test client instance back to the previous release image and stops the release;
- an App 5 run records this step `skipped`;
- its ledger row is `step_type = 'skill'`, `skill_family = 'gstack'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 42.

**BFT level:** Light.

**Gate:** none.

**References:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md); [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `/qa-only` (GStack), report only: every feature on the release image → the findings, then Step 43.
- `security-audit-methodology` (Magnus919): the release part of the assessment plan → the findings, then Step 44.

**Not used:** GStack's `/qa`, because it commits its own fixes.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-f-ship-and-monitor/f42a-test-spec|Step 42A Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42a-test-spec.md).

**Standards:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md); [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md).

## Why it is built this way

- **The image, not App 1.** Clients run the release image, so the image is what is tested.
- **Three browsers.** Customers use all three; a page that fails in one fails for them.
