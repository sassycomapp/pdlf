---
title: "f44-build-plan"
doc-id: "mb-c7cb929d"
updated: "2026-11-13"
---
# Step 44 — Release: Build Plan

## Step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). For App 1, the release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md)). For App 5, Mybizz's own management app, the release is its tagged version published in Anvil; Steps 42, 42A and 43 are recorded `skipped`.

#### Step 44: Release

**Must achieve:** David's decision to release, taken at the gate `production-released` on the results of Steps 41 to 43, and the release carried out: for App 1, App 5's Release action moves every client instance to the release image in stages; for App 5, David publishes App 5's tagged release in Anvil.

**Starts from:** the results of Steps 41, 42A and 43; the open findings in `triage_findings`; the receipts of Steps 41 to 43.

**Produces:** the `gates` row of `production-released`; the release carried out; in `pdlf-outputs\f44\`: the release record, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** David, at the gate; OpenCode prepares the gate and checks the release.

**Must be built so that:**
- an open finding in `triage_findings` blocks the gate;
- the receipts of Steps 41 to 43 match their evidence (PR-05);
- the gate follows `spec-gate-procedure`: Full BFT, the gate summary block, and David's explicit yes or no; on yes David records his approval with `pdlf-gate.sh`, and the agent reads the row; the agent never writes it;
- for App 1, App 5's Release action runs only after the gate; every release is staged, as [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md) sets out: the test client instance, then 10% of client instances, then all, each stage passing its health check first; a failed health check rolls that stage back and stops the release; a rollback trigger of the deployment specification moves the client instances back to the previous release image at once;
- for App 5, David publishes App 5's tagged release in Anvil, following the agent's instructions;
- App 5 sends the release notification to clients after the last stage;
- its ledger row is `step_type = 'gate'`, `skill_family = 'manual'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Steps 41 to 43.

**BFT level:** Full (gate).

**Gate:** `production-released`: the app is released.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md); [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md).

**Skills.** None: the gate reads the results of Steps 41 to 43, and the release is App 5's own action.

**Layers with no skill:** all; David decides and App 5 releases.

**Testing:** [[[pdlf:app-factory/phase-f-ship-and-monitor/f44-test-spec|Step 44 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f44-test-spec.md).

**Standards:** [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md).

## Why it is built this way

- **David decides on evidence.** The gate shows the proven results of every release check.
- **Staged release.** A fault reaches the test client, then a tenth of clients, before it can reach everyone, and each stage rolls back by itself on failure.
