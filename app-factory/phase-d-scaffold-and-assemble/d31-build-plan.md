---
title: "d31-build-plan"
doc-id: "mb-ea170848"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 31: Scaffold planning

**Must achieve:** Plans the modules and functions the code needs, as empty stubs, in `scaffold-plan.md`.

**Carried out by:** OpenCode.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to module/function structure planning
2. Review Step 15/16 architecture and domain model — TDD cluster, CONTEXT.md, ADRs
3. Review Step 30 pulled UI form structure
4. Review Step 21 concept audit report
5. Plan module/function structure — Determine what stubs to create
6. Write `scaffold-plan.md` — Saved to `<project-library>/`
7. Verify output — `scaffold-plan.md` exists; STOP if missing
8. Write Step 31 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-31-receipt.md`
10. Apply BFT — Full level
11. Follow execution sequence — Housekeeping, stop, wait for continue
