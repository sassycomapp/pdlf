---
title: "f46-build-plan"
doc-id: "mb-9d39104e"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). Steps 42 to 44 still describe a staging and production split that PDLF does not have; they are rebuilt around the `develop` → `stable` release.

#### Step 46: Learning

**Must achieve:** The retrospective: what this build taught is captured and written into the sources the next build reads.

**Carried out by:** OpenCode.

**Gate:** `released`: the build cycle closes.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to retrospective and learning
2. Invoke GStack `/retro` — Retrospective report
3. Invoke GStack `/learn` — Capture learnings
4. Invoke GStack `/context-save` — Persist working state
5. Update ISA — Fill Verification section, update Changelog
6. Update registry — `current_step: 46`, `last_gate: "released"`, `active: false`
7. Sync and embed GBrain — Learnings now searchable for next project
8. Execute gate procedure — per `specifications-local/spec-gate-procedure.md`
9. Gate: `released` (jointly with Step 45) — Full BFT, gate summary, developer approval required to close the project cycle
10. Write Step 46 ledger row — `completed_at`
11. Generate Step Receipt — `<project-library>/pdlf/outputs/step-46-receipt.md`
12. Apply BFT — Full (gate override)
13. Follow execution sequence — Housekeeping, stop
