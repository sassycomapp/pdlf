---
title: "f41-build-plan"
doc-id: "mb-4042f695"
updated: "2026-11-13"
---
# Step 41 — Release Readiness: Build Plan

## Step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). For App 1, the release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md)). For App 5, Mybizz's own management app, the release is its tagged version published in Anvil; Steps 42, 42A and 43 are recorded `skipped`.

#### Step 41: Release readiness

**Must achieve:** proof that the app is ready to release: every feature has passed `build-verified`, the whole suite passes, every release test the app's test plan names passes, the pre-release security assessment is clean, and the release is documented; David then commits, tags and pushes the app.

**Starts from:** the run's tickets and their gates; the app; the test plan; Step 15's security assessment plan; the schema migration log; the release notes' material.

**Produces:** the readiness report; the release notes; the migration plan of any schema change; the performance baseline; the app tagged and pushed by David; in `pdlf-outputs\f41\`: the report, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with the skills below; David commits, tags and pushes.

**Must be built so that:**
- a release is one version of the app (V1, V2 and so on) and carries every feature of that version; every ticket of the run has passed `build-verified`;
- `tdd` runs the whole suite at Levels 1 and 2, and every release test the app's test plan names passes;
- `security-audit-methodology` runs the pre-release part of Step 15's assessment plan, and `/cso` runs a full static scan; no high or critical finding is open;
- `benchmark` records the performance baseline of the public pages for Step 45;
- when the release changes the schema, the change only adds tables and nullable columns, is recorded in the schema migration log with its migration plan and rollback, and is ready for App 3's table definitions at Step 42;
- the release notes are written, and before a first release the Privacy Policy, Terms of Service and Cookie Policy exist (DC-14);
- for the first release of App 1, the exit export and the legal documents system are proven on the test client instance, as [[[default:specifications-global/spec-legal-documents-and-consent|Legal Documents and Consent]]](C:/dev/project-library-global/specifications-global/spec-legal-documents-and-consent.md) section 12 sets out, and `media.mybizz.live` sets no cookie;
- `wizard` writes David's instructions to commit, tag the release version and push the app; the agent never commits;
- its ledger row is `step_type = 'skill'`, `skill_family = 'opencode'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming the last ticket's Step 39.

**BFT level:** Full.

**Gate:** none.

**References:** [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md); [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `tdd` (Matt Pocock): the whole suite and the app's release tests → the readiness report, then Step 44.
- `security-audit-methodology` (Magnus919): the pre-release part of Step 15's assessment plan → the readiness report.
- `/cso` (GStack): a full static scan of the app → the readiness report.
- `benchmark` (GStack): the performance baseline of the public pages → Step 45.
- `wizard` (Matt Pocock): David's instructions to commit, tag and push → Step 42.

**Not used:** GStack's `/ship`, because it commits and pushes itself; agents never commit.

**Layers with no skill:** the release notes and migration plan; OpenCode writes them.

**Testing:** [[[pdlf:app-factory/phase-f-ship-and-monitor/f41-test-spec|Step 41 Test Specification]]](C:/pdlf/app-factory/phase-f-ship-and-monitor/f41-test-spec.md).

**Standards:** [[[default:specifications-global/spec-deployment|Deployment]]](C:/dev/project-library-global/specifications-global/spec-deployment.md); [[[default:specifications-global/spec-legal-documents-and-consent|Legal Documents and Consent]]](C:/dev/project-library-global/specifications-global/spec-legal-documents-and-consent.md).

## Why it is built this way

- **The last judgement before release.** Everything that must be true of a release is proven here, so the gate at Step 44 rests on evidence.
- **Additive schema only.** Client instances keep their data through a release because a release never removes or changes a column.
