---
title: "f42-build-plan"
doc-id: "mb-204ff45b"
updated: "2026-11-13"
---
# Step 42 — Release to App 2: Build Plan

## Step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). For App 1, the release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md)). For App 5, Mybizz's own management app, the release is its tagged version published in Anvil; Steps 42, 42A and 43 are recorded `skipped`.

#### Step 42: Release to App 2

**Must achieve:** App 1's tagged release pushed into App 2, `master_template`; its table changes written into App 3's table definitions; the release image built, scanned, signed and checked; and the test client instance running it by its digest, with every client's data backed up first.

**Starts from:** App 1's release tag from Step 41; the migration plan; App 2, App 3 and `{slug}-app4`.

**Produces:** App 2 at the release tag; App 3's table definitions updated; the release image under the release tag; the test client instance on the release image; in `pdlf-outputs\f42\`: the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** David, following instructions written with `wizard`; OpenCode checks each result.

**Must be built so that:**
- before the push, every client instance copies its data to its own bucket (RL-02);
- App 2's code equals App 1's release tag exactly;
- the release's table changes are written into App 3's table definitions, and the table-change check passes (RL-03);
- the image build workflow in `{slug}-app4` builds the release image from the release tag and stores it under that tag; the build stops if App 3 holds any form or server module, or if the table-change check finds a table or column removed, renamed or retyped;
- the workflow scans the release image and signs it; the build fails on end-of-life software, and the release stops while any high or critical finding is older than 14 days, as [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md) sets out;
- the whole suite passes on the release image;
- App 5 verifies the image's signature and moves the test client instance to it by its digest (RL-19), and its App Server adds the release's new tables and columns;
- rollback moves client instances back to the previous release image with `auto-migrate` off, as [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md) sets out;
- an App 5 run records this step `skipped`;
- its ledger row is `step_type = 'manual'`, `skill_family = 'manual'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 41.

**BFT level:** Light.

**Gate:** none.

**References:** [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md); [[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `wizard` (Matt Pocock): David's instructions for the backups, the push to App 2, App 3's table definitions, the image build and the rollback → Step 42A.

**Layers with no skill:** the image build, scan and signing run in the `{slug}-app4` workflow.

**Testing:** [[[pdlf:app-factory/phase-f-ship-and-monitor/f42-test-spec|Step 42 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f42-test-spec.md).

**Standards:** [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md); [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md); [[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md).

## Why it is built this way

- **Backups first.** No client's data is at risk from a release, because every client is backed up before anything moves.
- **Exactly the release.** App 2 and the image hold exactly App 1's tagged code, so what was tested is what ships.
- **Only signed images run.** A client instance runs only an image Mybizz built and signed.
