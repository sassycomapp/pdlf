---
title: "f41-build-plan"
doc-id: "mb-4042f695"
updated: "2026-10-22"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is the clone of App 1's approved code into App 2, `master_template`, which every client instance depends on.

#### Step 41: Release readiness

**Must achieve:** Proves App 1 is ready to release: every feature has passed `build-verified`, the whole test suite passes, the pre-release security assessment is clean, and the release notes are written. The developer commits, tags and pushes App 1.

**Carried out by:** OpenCode; the developer commits, tags and pushes.

**Skills.** Every skill's output is used by the step named after the arrow.
- `tdd` (Matt Pocock): the full test suite at levels 1 and 2 → the readiness report.
- `security-audit-methodology` (Magnus919): the pre-release part of Step 15's security assessment plan → the readiness report.
- `/cso` (GStack), full static scan of App 1 → the readiness report.
- `wizard` (Matt Pocock): the developer's instructions to commit, tag the release version and push App 1 → Step 42.

**Not used:** GStack `/ship`, because it commits, pushes and opens a pull request itself; agents never commit or push.

**Testing:** the whole suite passes; any failure returns its feature to Step 35.

**Must be built so that:**
- a release is one version of the application (V1, V2 and so on) and carries every feature of that version;
- when the release changes the schema, its migration plan for App 3 and every client instance exists before the release continues;
- the compliance documents named in the CEO plan exist before a first release;
- `benchmark` (GStack) records the performance baseline of the public pages → Step 45;
- for the first release, the exit export is proven on the test client: all its data lands in its R2 bucket;

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to ship readiness
2. Invoke GStack `/ship` — Tests, VERSION bump, CHANGELOG, commit, push; stops at push
3. Verify outputs — Merged base branch, tests pass, VERSION bumped, CHANGELOG updated, branch pushed; STOP if missing
4. Write Step 41 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-41-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue
