---
title: "c27-build-plan"
doc-id: "mb-868a7285"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 27: Screen production

**Must achieve:** Produces screens from the approved wireframes. Deferred: runs only if the developer asks for it.

**Carried out by:** OpenCode.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to screen production
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Produce screen HTML from approved wireframe (Step 26)
4. Apply wireframe fidelity checklist
5. Apply screen standard compliance checklist
6. Verify outputs — Screen HTML, both checklists; STOP if missing
7. Write Step 27 ledger row — `completed_at` (or `deferred`)
8. Generate Step Receipt — `<project-library>/pdlf/outputs/step-27-receipt.md`
9. Apply BFT — Full level (if active)
10. Follow execution sequence — Housekeeping, stop, wait for continue
