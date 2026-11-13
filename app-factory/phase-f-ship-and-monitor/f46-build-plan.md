---
title: "f46-build-plan"
doc-id: "mb-9d39104e"
updated: "2026-11-13"
---
# Step 46 — Learning: Build Plan

## Step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). For App 1, the release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md)). For App 5, Mybizz's own management app, the release is its tagged version published in Anvil; Steps 42, 42A and 43 are recorded `skipped`.

#### Step 46: Learning

**Must achieve:** what this build taught captured, each lesson written into the source the next build reads, and the build cycle closed by David at the gate `released`.

**Starts from:** the run's ledger, deviations, findings and receipts; its history in the repositories.

**Produces:** the lessons, each written into its source; each approved lesson submitted to GBrain; the `gates` row of `released`; in `pdlf-outputs\f46\`: the retrospective, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with the skills below. David approves each lesson and answers the gate.

**Must be built so that:**
- `/retro` reviews the build's history and `/learn` exports what GStack's own skills learned during the build;
- each lesson is sorted by where it belongs: a lesson about the app goes into its project library; a lesson about the machine goes into PDLF, `project-library-global` or a skill; nothing about the app stays in PDLF;
- each lesson is written into its source, with David's approval, and a fixed problem gets its test (LG-07);
- `mb-submit-memory` submits each approved lesson as a governed fact to GBrain, once it is written into its source;
- the gate follows `spec-gate-procedure`: Full BFT, the gate summary block, and David's explicit yes or no; on yes David records his approval with `pdlf-gate.sh`, and the agent reads the row; the agent never writes it;
- its ledger row is `step_type = 'gate'`, `skill_family = 'gstack'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 45.

**BFT level:** Full (gate).

**Gate:** `released`: the build cycle closes.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `/retro` (GStack): what the build taught, from its history → the lessons.
- `/learn` (GStack): what GStack's skills learned → the lessons.
- `mb-submit-memory` (MyBizz): each approved lesson → GBrain, for the next build.

**Not used:** GStack's `/context-save`; the ledger already records where a build stands.

**Layers with no skill:** sorting each lesson to its source; OpenCode does it by the rule above.

**Testing:** [[[pdlf:app-factory/phase-f-ship-and-monitor/f46-test-spec|Step 46 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f46-test-spec.md).

**Standards:** the PDLF rule that an app's files and context never stay in PDLF.

## Why it is built this way

- **Lessons go where they are read.** A lesson written into the source the next build reads changes the next build; a lesson kept in a report does not.
- **The machine stays general.** App lessons go to the app; machine lessons go to the machine.
