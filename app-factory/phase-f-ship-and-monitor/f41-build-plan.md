---
title: "f41-build-plan"
doc-id: "mb-4042f695"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). Steps 42 to 44 still describe a staging and production split that PDLF does not have; they are rebuilt around the `develop` → `stable` release.

#### Step 41: Ship

**Must achieve:** Tests, versions and records the release, and pushes it; it stops at the push.

**Carried out by:** GStack, using `/ship`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to ship readiness
2. Invoke GStack `/ship` — Tests, VERSION bump, CHANGELOG, commit, push; stops at push
3. Verify outputs — Merged base branch, tests pass, VERSION bumped, CHANGELOG updated, branch pushed; STOP if missing
4. Write Step 41 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-41-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue
