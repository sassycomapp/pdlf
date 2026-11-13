---
title: "f45-build-plan"
doc-id: "mb-1628cc4a"
updated: "2026-11-13"
---
# Step 45 — Production Check: Build Plan

## Step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). For App 1, the release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md)). For App 5, Mybizz's own management app, the release is its tagged version published in Anvil; Steps 42, 42A and 43 are recorded `skipped`.

#### Step 45: Production check

**Must achieve:** the released app watched for errors, slowness and resource strain against its baseline; and the post-release part of the security assessment plan carried out.

**Starts from:** the release record of Step 44; the health baseline of Step 43 and the performance baseline of Step 41; Step 15's assessment plan.

**Produces:** the production report; in `pdlf-outputs\f45\`: the report, the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode, with the skills below.

**Must be built so that:**
- `/canary` watches the released app against its baseline: errors below 5%, response times within 20%, every heartbeat arriving (RL-09); for App 1, the test client instance is watched;
- App 5 reads every client instance's heartbeat: each reports the release version and schema fingerprint and passes its smoke test (RL-05); App 5 flags any client near its container's memory and the business near its cluster's client limit (RL-12);
- `security-audit-methodology` runs the post-release part of Step 15's assessment plan, and the periodic checks are scheduled (RL-11);
- `mb-sentinel-review` runs at Medium scrutiny on the production report;
- a rollback trigger of the deployment specification is acted on at once;
- its ledger row is `step_type = 'skill'`, `skill_family = 'gstack'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 44.

**BFT level:** Full.

**Gate:** none.

**References:** [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md); [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `/canary` (GStack): the released app against its baseline → the report, then Step 46.
- `security-audit-methodology` (Magnus919): the post-release part of the assessment plan → the report.
- `mb-sentinel-review`, Medium → `triage_findings`.

**Layers with no skill:** none.

**Testing:** [[[pdlf:app-factory/phase-f-ship-and-monitor/f45-test-spec|Step 45 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f45-test-spec.md).

**Standards:** [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md).

## Why it is built this way

- **Watched, not assumed.** A release can pass every test and still fail under real use; watching against the baseline catches it.
