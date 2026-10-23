---
title: "e39-build-plan"
doc-id: "mb-011df646"
updated: "2026-10-23"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 39: Triage

**Must achieve:** Sorts the findings of Steps 37 and 38 for this feature.

**Carried out by:** Matt Pocock, using `triage`.

**Runs:** once per feature.

**Gate:** `build-verified`, for this feature: it is signed off and the next feature may start. Step 41 cannot begin until every feature has passed.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `triage` (Matt Pocock): sorts every finding from Steps 35A to 38A with its five labels → `triage_findings`, which decides the `build-verified` gate.
- A finding labelled for a fix returns the feature to Step 35, where `diagnosing-bugs` finds its root cause.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to issue triage
2. Invoke Matt `triage` — Updates issue tracker: comments, labels, state changes, agent briefs
3. Verify outputs — Labels applied, comments added, briefs written; STOP if missing
4. Write Step 39 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-39-receipt.md`
6. Apply BFT — Light level
7. Follow execution sequence — Housekeeping, stop, wait for continue

## From `matt-pocock-skills-pdlf-compliance.md`: item 2B

### B. The `grilling` dependency gap — RESOLVED, no import
Two of your five in-scope skills have documented branches into the `grilling` interview loop:
- [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) — ends with "...then grill through whichever one you pick."
- `triage` — independently documented as "categorise, verify, **grill if needed**, and write agent-ready briefs."

Neither `grilling` nor its wrappers (`grill-me`, `grill-with-docs`) will be imported. Tested against the one selection criterion PDLF actually uses — does this fit a real need OpenCode can't already do itself — it fails: PDLF's own execution discipline already has an equivalent mechanism (a step that can't complete presents a deviation request with three options, never deciding unilaterally). **Action: route the "grill if needed" branches in `triage` and [[[pdlf:app-factory/phase-e-build-and-verify/e40-reference|Step 40 Improve Codebase Architecture]]](C:/pdlf/app-factory/phase-e-build-and-verify/e40-reference.md) into PDLF's existing deviation-request flow instead of a Matt Pocock skill.** `grill-with-docs` was considered and rejected specifically — it's user-invoked only (`disable-model-invocation: true`), so it can't fire automatically mid-step in the first place, and it redundantly bundles in [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|Step 16 Domain Modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md), which PDLF already runs standalone at Step 16.

## From `matt-pocock-skills-pdlf-compliance.md`: item 2D

### D. `triage` state-machine duplication — RESOLVED, and now confirmed shipped

**Solution: treat `triage` as a pure computation step feeding the ledger, exactly like Step 38A already does for CI results.** This is not a new pattern — it's the same consolidation precedent your own pipeline already established one step earlier in the same loop.

**Status update:** this proposal is no longer just a recommendation — `triage_findings` is
a live table in [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)'s current seven-table schema, with exactly the
columns proposed below. This section is kept for its rationale, not as an open action item.

1. Add a `triage_findings` table to the `pdlf` ledger: one row per finding, scoped to the feature's Step 39 row. Columns: `finding_id`, `source_step` (36/37/38), `triage_label` (Matt's existing five values — `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`; no new vocabulary), `resolution_note`, `resolved_by`, `resolved_at`.
2. Step 39 runs `triage`, gets its label output in `.scratch/`, and immediately upserts it into `triage_findings`. Per the Step Receipt principle (the receipt IS the ledger row, not a gloss), the triage label IS the `triage_label` column — not a standing file.
3. The `.scratch/` output is transient computation input, consumed once — same status as raw CI logs at 38A, not treated as authoritative afterward.
4. `build-verified` gate evaluation becomes a pure ledger query: passes only when every `triage_findings` row for that feature is `wontfix` or has a non-null `resolved_at`. Consistent with principle 3 and with how every other gate in the system is FK-enforced rather than file-checked.

## From `pdlf-todo.md`: item C1

### C1. Integrate Suite A and Suite B into Steps 35A, 36, 37, 38, 39, and relook the testing suite

Both testing checklists ([[[pdlf:pdlf-library/templates-local/chk-pdlf-self-test|Chk Pdlf Self Test]]](C:/pdlf/pdlf-library/templates-local/chk-pdlf-self-test.md) exists; the earlier
`chk-anvil-app-testing.md` was retired and is no longer on disk anywhere —
verified 2026-09-18) are referenced from [[[pdlf:pdlf-library/policy-local/pol-testing-and-quality|pol-testing-and-quality]]](C:/pdlf/pdlf-library/policy-local/pol-testing-and-quality.md), but
their checks are not yet built into the actual step files that do
testing work. Deferred to Phase E, when those step files are rebuilt.

This step's testing is its test specification, drawn from the test suite in `C:\dev\project-library-global\test-suite\`.

> **Changed since:** The earlier lists carried the Suite A/B integration and the testing relook as two separate items; they are one job and are merged here.
