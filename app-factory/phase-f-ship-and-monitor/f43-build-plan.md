---
title: "f43-build-plan"
doc-id: "mb-7ecf0cbd"
updated: "2026-11-13"
---
# Step 43 — Client Instance Check: Build Plan

## Step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). For App 1, the release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md)). For App 5, Mybizz's own management app, the release is its tagged version published in Anvil; Steps 42, 42A and 43 are recorded `skipped`.

#### Step 43: Client instance check

**Must achieve:** the test client instance proven healthy on the release image and its health baseline recorded.

**Starts from:** the test client instance on the release image; the hosting specification.

**Produces:** the smoke test result; the health baseline; in `pdlf-outputs\f43\`: the results, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with GStack's `/qa-only` and `/canary`.

**Must be built so that:**
- the test client instance reports the release version and schema fingerprint in its heartbeat, and passes a quick smoke test with `/qa-only` (RL-05);
- `/canary` records the instance's health baseline for Step 45;
- at a first release, a new client instance starts secure (RL-10);
- client isolation holds (SC-14);
- an App 5 run records this step `skipped`;
- its ledger row is `step_type = 'skill'`, `skill_family = 'gstack'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 42A.

**BFT level:** Light.

**Gate:** none.

**References:** [[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md); [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `/qa-only` (GStack), quick tier: the smoke test → Step 44.
- `/canary` (GStack): the health baseline → Step 45.

**Layers with no skill:** the first-release check; OpenCode runs it against the hosting specification.

**Testing:** [[[pdlf:app-factory/phase-f-ship-and-monitor/f43-test-spec|Step 43 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f43-test-spec.md).

**Standards:** [[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md); [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md).

## Why it is built this way

- **Healthy before all clients move.** The test client proves the release works where clients run it.
- **Baseline for watching.** Step 45 compares production against this baseline.
