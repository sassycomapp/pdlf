---
title: "e39-reference"
doc-id: "mb-43a89cf2"
updated: "2026-10-12"
---

## From `39-triage.md`

## Task Execution Order

1. Read `<project-library>/pdlf/outputs/step-37-findings.md` and
   `step-38-findings.md`. Both must exist and be non-empty (per ADR-0009); if either is
   missing, this is a deviation, not a silent skip.
2. Run Matt `triage` against whatever findings those artifacts contain — including the
   explicit "clean pass" case, where triage confirms there is nothing to process.
3. Apply category (bug/enhancement) + state role per the five-state machine, using the
   triage label vocabulary from `/setup-matt-pocock-skills`.
3a. Upsert each triage finding into the `triage_findings` ledger table. For each finding
    from the `.scratch/` triage output:
    - INSERT on first pass for this feature cycle (matching `finding_id` is not yet present
      for this `step_id`).
    - UPDATE `resolution_note`, `resolved_by`, `resolved_at` on subsequent passes when the
      same `finding_id` already exists for this `step_id`.
    The `.scratch/` triage output is transient input to this upsert — not authoritative
    afterward. The ledger row is the source of truth (same pattern as Step 38A's CI
    consolidation). On clean-pass (no findings), write a single row with
    `finding_id = 'clean-pass'` and `triage_label = 'wontfix'` so the gate query below sees
    a resolved state.
4. → GATE: Execute gate procedure per [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md), including the ledger
   integrity check (no orphaned `steps`/`gates`/`isc`/`deviations` rows).
5. → GATE: `build-verified` — evaluated for this feature only. Developer approval
   required. Pipeline does not advance to Step 41 until every feature has individually
   passed this gate.
6. Follow execution sequence in [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md).
7. Apply BFT per [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md) (Full — gate override).

---

## Description

Updates the issue tracker with what Steps 36–38 found — comments, labels, and state
changes. This is the loop-end step for a given feature cycle: the `build-verified` gate
lives here, not at Step 40, because remediation applied at Step 40B must be retested by
Steps 36–38 before a feature can be called verified (see ADR-0007). A feature is not
signed off until this gate passes.

## Inputs Required

- Tickets from Step 19
- `step-37-findings.md` and `step-38-findings.md` (mandatory, verified non-empty)
- Triage label vocabulary from `/setup-matt-pocock-skills`

## Outputs

- `triage_findings` ledger rows (one per finding, upserted — authoritative)
- Transient `.scratch/` triage output (input to upsert, not authoritative afterward)
- Issue tracker updates: labels applied, comments added, agent briefs for ready issues
- GATE `build-verified` — full BFT, gate summary, ledger integrity check, developer
  approval required
- Ledger row for this feature cycle (e.g., 39.1, 39.2 — one per feature)

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 39 | Skill | **GATE** `build-verified` | Matt `triage` |

## Gate

| Gate | After Step | What is Locked |
|---|---|---|
| `build-verified` | 39 | Architecture scan and any developer-approved remediation applied and retested, design review done, code review done, QA passed, triage complete for this feature cycle. **Gate query:** join `gates.step_id` to `triage_findings.step_id` — every `triage_findings` row for this feature's `steps.id` must satisfy `triage_label = 'wontfix'` OR `resolved_at IS NOT NULL`. No open (`needs-triage`/`needs-info`/`ready-for-agent`/`ready-for-human`) rows remain. Evaluated once per feature — pipeline does not advance to Step 41 until every feature has individually passed. Features are known-good baselines. |

---

## Loop behavior

On gate PASS: this feature is signed off. Return to Step 35 for the next feature, or —
if this was the last feature from Step 19's ticket list — exit the loop and proceed to
Step 41.
On gate FAIL: this feature's cycle stops, blocker recorded, not marked signed off. Developer
resolves; re-entry point is the failed step, not the start of the cycle.

---

## Grilling Branch Routing

If the `triage` skill's output indicates a "grill if needed" / clarification-required
condition on a finding, do not invoke any grilling-family skill (`grilling`, `grill-me`,
`grill-with-docs`). Instead, present a deviation request per
[[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md) with three options, and hold that
finding at `needs-info` in the ledger until the developer responds.

```
DEVIATION REQUEST — Step 39 (Triage Clarification)

Prescribed tool: grilling-family (not imported — routing to deviation-request flow)
Status: BLOCKED
Reason: Finding requires clarification — cannot be fully triaged without developer input.

Options:
  A) Authorize clarification — developer provides the needed input now
  B) Hold at needs-info — leave finding in needs-info state, proceed with remaining findings
  C) Skip this finding — mark wontfix, proceed
     Impact: This finding will not be actioned

Your decision? (A/B/C)
```

The agent never decides to invoke grilling. All deviations are recorded in the `deviations`
table with description, options presented, decision, and timestamp. The developer decides.

---

## Reference

Skill path: `~/.agents/skills/triage/SKILL.md`

Gate-placement rationale: ADR-0007. Artifact-dependency rationale: ADR-0009.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft|spec-bft]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)
For gate procedure: [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|spec-gate-procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.

Skills save where designed. PDLF process artifacts go to `<project-library>/pdlf/`.
