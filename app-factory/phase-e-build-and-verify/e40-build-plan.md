---
title: "e40-build-plan"
doc-id: "mb-71500d0b"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 40: Architecture scan

**Must achieve:** An optional, read-only scan of the feature's code architecture. The developer decides for each feature whether it runs.

**Carried out by:** Matt Pocock, using `improve-codebase-architecture`.

**Runs:** once per feature.

**Skills.** Every skill's output is used by the step named after the arrow.
- `improve-codebase-architecture` (Matt Pocock), read-only, when the developer chooses to run it → the findings, then Step 40B.
- `graphify`: the code graph from Step 34, refreshed for this feature, gives the scan its evidence of coupling → the findings.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to architecture health scan
2. Present RUN/SKIP recommendation with justification
   - Branch RUN: Invoke Matt `improve-codebase-architecture` — Interactive HTML architecture report
   - Branch SKIP: Skip the scan
3. Write Step 40 ledger row — `completed_at`
4. Generate Step Receipt — `<project-library>/pdlf/outputs/step-40-receipt.md`
5. Apply BFT — Full
6. Follow execution sequence — Housekeeping, stop, wait for continue

## From `matt-pocock-skills-pdlf-compliance.md`: item 2B

### B. The `grilling` dependency gap — RESOLVED, no import
Two of your five in-scope skills have documented branches into the `grilling` interview loop:
- [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) — ends with "...then grill through whichever one you pick."
- `triage` — independently documented as "categorise, verify, **grill if needed**, and write agent-ready briefs."

Neither `grilling` nor its wrappers (`grill-me`, `grill-with-docs`) will be imported. Tested against the one selection criterion PDLF actually uses — does this fit a real need OpenCode can't already do itself — it fails: PDLF's own execution discipline already has an equivalent mechanism (a step that can't complete presents a deviation request with three options, never deciding unilaterally). **Action: route the "grill if needed" branches in `triage` and [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) into PDLF's existing deviation-request flow instead of a Matt Pocock skill.** `grill-with-docs` was considered and rejected specifically — it's user-invoked only (`disable-model-invocation: true`), so it can't fire automatically mid-step in the first place, and it redundantly bundles in [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md), which PDLF already runs standalone at Step 16.
