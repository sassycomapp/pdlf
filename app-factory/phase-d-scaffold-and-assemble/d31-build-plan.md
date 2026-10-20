---
title: "d31-build-plan"
doc-id: "mb-ea170848"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 31: Scaffold planning

**Must achieve:** Plans the modules and functions the code needs, as empty stubs, in `scaffold-plan.md`.

**Carried out by:** OpenCode.

**Skills.** Every skill's output is used by the step named after the arrow.
- `codebase-design` (Matt Pocock): the modules from Step 15's design, as deep modules at clean seams, with the business logic in pure modules apart from Anvil code → `scaffold-plan.md`, then Steps 32, 34 and 35.
- `data-models` (Anvil): which behaviour goes on model classes, which in server methods and which in ordinary server functions → `scaffold-plan.md`.
- `server-code` and `client-modules` (Anvil): where each module lives and the rules it follows (no `client_code/__init__.py`, server code isolated to the app) → `scaffold-plan.md`, then Step 32.
- For every stub, `scaffold-plan.md` names the behaviour it will hold and the test from Step 15's test plan that proves it → Step 35.

**Inputs:** the reviewed plan, `CONTEXT.md` and the ADRs, the concept audit, the tickets and the pulled forms.

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) sections 2 and 3 (server function pattern, three-tier module pattern with pure logic).

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
