---
title: "c19-build-plan"
doc-id: "mb-de445841"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 19: To tickets

**Must achieve:** Breaks the plan into features (tickets) in the order they depend on each other. This is the feature list the build loop works through.

**Carried out by:** Matt Pocock, using `to-tickets`.

**Skills.** Every skill's output is used by the step named after the arrow.
- `to-tickets` (Matt Pocock): the features as tickets in dependency order, as local files in `pdlf-tickets\`, configured at Step 11 → Steps 22 and 35.
- `secure-software-engineering` (Magnus919): each ticket's security acceptance criteria, from Step 15's threat model → Steps 35 and 37.
- `mb-archify-scope`, then `archify`: the user flows of the application and the feature flow of each ticket that spans more than one screen → Steps 21, 22 and 35.
- `mb-sentinel-review`, Medium → `triage_findings`.

**Inputs:** the CEO plan, the reviewed plan, the test plan, `CONTEXT.md` and the ADRs.

**Testing:** each ticket names its acceptance tests from Step 15's test plan → Step 35.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to issue decomposition
3. Read Step 14 CEO plan — `<project-library>/gstack-outputs/step-14-ceo-plan.md` (refined by Step 15)
4. Read CONTEXT.md + ADRs from Step 16
5. Confirm issue tracker config — From `/setup-matt-pocock-skills`
6. Invoke Matt `to-tickets` — Breaks spec into tracer-bullet issues in dependency order
7. Verify outputs — Issues published to project issue tracker; STOP if missing
8. Write Step 19 ledger row — `completed_at`
9. Generate Step Receipt — `<project-library>/pdlf/outputs/step-19-receipt.md`
10. Apply BFT — Full level
11. Follow execution sequence — Housekeeping, stop, wait for continue
