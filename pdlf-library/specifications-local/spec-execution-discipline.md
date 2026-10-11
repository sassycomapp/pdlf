---
title: "spec-execution-discipline"
doc-id: "mb-913cd6af"
updated: "2026-10-11"
---
# PDLF Execution Discipline

**Purpose:** This file is the single source of truth for how every PDLF step executes. Each
step file (11 through 46) references this document rather than inlining
the execution sequence. When a step file says "Follow the execution sequence in
specifications-local/spec-execution-discipline.md," the agent loads this file and runs the procedure below.

**Use:** The orchestrator loads this file at every step. The agent applies the 13-point
sequence to the current step, does not skip substeps without a deviation request.

---

## 13-Point Execution Sequence

Every step follows this sequence. The agent never skips a substep without a deviation request.

1. Query GBrain for context relevant to this step's domain.
2. Check step type: SKILL / MANUAL / OPTIONAL / GATE.
3. If OPTIONAL: present recommendation + justification, wait for RUN/SKIP decision.
4. If MANUAL: present instructions + references, wait for "done," verify.
5. If SKILL or OpenCode-native: invoke the skill or perform the documented procedure.
6. Verify the expected output exists. If missing: STOP, present a deviation request.
7. Run BFT checkpoint at the step's assigned level (Full / Light / None) per `[[spec-bft]]`.
8. Write the `steps` ledger row (step_number, status, artifact_path, synthesized, etc.).
9. Generate and save the Step Receipt to `dev-{slug}\{slug}-project-library\pdlf\step-{N}-receipt.md`.
10. Ask the two housekeeping questions — separately, never combined, never auto-run:
    - "Commit and push to GitHub?"
    - "Sync/embed GBrain?"
11. STOP and report to the developer.
12. Wait for "continue" to proceed to the next step.

Applies to every step, including OpenCode-native steps. Feature cycles inside Step 35 each
follow this sequence individually (35.1, 35.2, etc.).

---

## Step-Type Routing

### Optional Steps

Present a recommendation with justification:
```
Step NN is optional.

Recommendation: [RUN / SKIP]
Reason: [justification]

Your decision? (run/skip)
```
Do not proceed until the developer answers.

### Manual Steps

Present instructions and reference documents. Wait for the developer to confirm "done."
Verify the expected output exists before proceeding.

### Skill Steps

Invoke the named skill. Read the skill's own SKILL.md first — never trust a skill name
alone. If the skill cannot be invoked, present a deviation request. Do not silently do the
work manually.

### Gate Steps

Gate steps follow the expanded gate procedure defined in `[[spec-gate-procedure]]`. Full BFT,
full maintenance, gate summary block, and explicit developer approval.

---

## Deviation Request Mechanism

If the agent cannot complete a step, it does not skip silently. It presents:

```
DEVIATION REQUEST — Step NN

Prescribed tool: <name>
Status: BLOCKED
Reason: <specific reason>

Options:
  A) Authorize deviation — <alternative action>
  B) Do not authorize — attempt to resolve the blocker
  C) Skip this step — proceed to next step
     Impact: <what is lost>

Your decision? (A/B/C)
```

The agent never decides to deviate. All deviations are recorded in the `deviations` table
with description, options presented, decision, and timestamp. The developer decides.

---

## Synthesized Flag Propagation

When a project is in `test` mode, Step 20 is eligible for abbreviation. If the
developer chooses an abbreviated or skipped run, the step's `synthesized` flag is set to
`true` (abbreviated) or the step's `status` is set to `"skipped"` in the ledger.
Step 12 is a simple yes/no decision gate — not test-mode-eligible. See
`[[step-conditional-state-policy]]` for the full state definitions.

**Downstream propagation:** Before invoking any step, the agent checks whether any of the
step numbers listed in that step's `inputs_used` correspond to a ledger row with
`synthesized = true` or `status = "skipped"`. If so, the Step Receipt for the current
step must show an INPUT NOTICE warning:

- Synthesized: `INPUT NOTICE: Input from Step {N} was synthesized (test-mode shortcut),
  not a full skill run. Treat this step's output as provisional to the same degree.`
- Skipped: `INPUT NOTICE: Input from Step {N} was skipped (developer declined). Treat
  this step's output as provisional.`

This ensures the taint is visible at every step downstream of a shortcut, not just at the
step where the shortcut happened. A developer glancing at a later receipt should not have
to remember that an earlier step was abbreviated.

---

## Stop-and-Review Discipline

Every step, including each feature cycle inside Step 35, produces a Step Receipt and stops
for "continue." The loop does not collapse the per-step stop discipline. A step is verified
complete when: its expected output exists, its BFT checkpoint passed, its ledger row is
written, and its Step Receipt is saved.

---

## Housekeeping

GBrain querying runs automatically at substep 1. Querying is read-only — no side effects.
GBrain syncing is a write operation asked at substep 10, never auto-run. The two housekeeping
questions are asked separately, every step, never combined.

---

## Output Routing

Skill outputs route per the project's own AGENTS.md. PDLF's own process artifacts go to
`dev-{slug}\{slug}-project-library\pdlf\`.

---

## Checkpoint Writing

The ledger row, Step Receipt, and devlog-index/judgement-trail entries are the complete
checkpoint. No separate state file, devlog file, or completion report. The Step Receipt
is generated from the ledger row just written — it IS the ledger row, formatted for reading.
Never compose a receipt separately.
