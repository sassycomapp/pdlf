---
title: "spec-execution-discipline"
doc-id: "mb-913cd6af"
updated: "2026-10-31"
---
# PDLF Execution Discipline

**Purpose:** This file is the single source of truth for how every PDLF step executes. Each
step file (01 through 46) references this document rather than inlining
the execution sequence. When a step file says "Follow the execution sequence in `spec-execution-discipline`," the agent loads this file and runs the procedure below.

**Use:** The orchestrator loads this file at every step. The agent applies the execution
sequence to the current step and does not skip a substep without a deviation request.

---

## Execution Sequence

Every step follows this sequence. The agent never skips a substep without a deviation request.

0. Open the step's `steps` row with `status = 'in_progress'` and `started_at`, or, when the row exists from an earlier attempt of the same run, set it back to `in_progress`. The open row is how the orchestrator resumes a run that stopped part-way through a step, and the row a gate's approval refers to.
1. Search GBrain for context relevant to this step's domain, across the federated documentation sources (one search covers the project library `{slug}-project-library`, `default`, which is `project-library-global`, and `pdlf`), adding `anvil-agent-references-code` when the step needs Anvil knowledge. Read the actual file each result points to. Application code is read directly from the app folder, never through GBrain.
2. Check step type: SKILL / MANUAL / OPTIONAL / GATE.
3. If OPTIONAL: present recommendation + justification, wait for RUN/SKIP decision.
4. If MANUAL: present instructions + references, wait for "done," verify.
5. If SKILL or OpenCode-native: invoke the skill or perform the documented procedure.
5a. Carry out the step's reference one section at a time. At the end of each section, STOP and report in at most three lines, in this form: `Step NN — section k of m done: <what was done>. Next: section j.` Wait for "continue" before the next section.
6. Verify the expected output exists. If missing: STOP, present a deviation request.
7. Run BFT checkpoint at the step's assigned level (Full / Light / None) per `[[spec-bft]]`.
8. Complete the `steps` ledger row opened at substep 0, per [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md): `step_number`, `run` (`app{n}` for a whole application, or the feature slug), `app_number`, `step_type` and `skill_family` in their allowed lowercase values, `status`, `artifact_path`, `synthesized`, and `inputs_used` listing every earlier step whose output this step used, so that input notices reach every later step.
9. Check every test of the step's test specification has its result in the step's output folder, recorded as [[[default:test-suite/ts-method]]](C:/dev/project-library-global/test-suite/ts-method.md) section 5 sets out. Generate and save the Step Receipt, with the table `ts_report.py` prints for this run's evidence in the step's output folder, to `{slug}-project-library\pdlf-outputs\{step}\{slug}-{step}-{run}-receipt.md`, where `{run}` is `app{n}` for a whole application, or the feature slug ([[[pdlf:pdlf-library/specifications-local/spec-artifact-handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), section 4).
10. Explain to the developer, in plain language, what was done and why, and show the Step Receipt.
11. STOP and ask the developer to run `/mb-close-out`.
12. Wait for "continue". The next step runs in a new OpenCode session, started with `/pdlf-init`, which resumes the run from the ledger.

Applies to every step, including OpenCode-native steps. Feature cycles inside Step 35 each
follow this sequence individually (35.1, 35.2, etc.).

---

## Failure and Flag Rules

These rules apply at every substep of every step.

1. **One fix attempt.** When a check or test fails, the agent makes at most one attempt to fix it. If that attempt fails, it STOPS and raises a flag.
2. **No experimenting.** The agent never writes trial scripts, starts trial servers or processes, or tries an untested alternative. When the reference does not say what to do, it STOPS and raises a flag.
3. **No changes to shared tools or documents during a run.** The agent never writes to `/mnt/c/pdlf`, `/mnt/c/dev/project-library-global` or `/mnt/c/mybizz`. When one of them is wrong or missing something, it STOPS and raises a flag, and never asks for a grant to change it.
4. **The flag.** A flag is this block, and the agent then waits:

```
FLAG — Step NN, section k, item i

Failed: <what failed>
Exact error: <the error text, copied>
Tried: <the one fix attempted, or "nothing">
State: <what is running, what was changed>
```

The developer takes the flag to the engineer. The fix is made at its source, and the agent continues from the item that failed.

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

Gate steps follow the expanded gate procedure defined in `[[spec-gate-procedure]]`: Full BFT,
gate summary block, and explicit developer approval.

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

Which steps may be abbreviated in `test` mode, and how, is stated in each step's own build plan. An abbreviated run sets the step's `synthesized` flag to `true`; a skipped run sets its `status` to `"skipped"` in the ledger.

**Downstream propagation:** Before invoking any step, the agent checks whether any of the
step numbers listed in that step's `inputs_used` correspond to a ledger row with
`synthesized = true` or `status = "skipped"`. If so, the Step Receipt for the current
step must show an INPUT NOTICE warning:

- Synthesized: `INPUT NOTICE: Input from Step {N} was synthesized (OpenCode produced it from pre-existing inputs, or an abbreviated test-mode run), not a full skill run. Treat this step's output as provisional to the same degree.`
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

## Commits and Memory

GBrain searching runs automatically at substep 1. Searching is read-only and has no side effects.
The agent never commits or pushes. Only the developer commits,
with `commit-all`. Close-out is `/mb-close-out`, run when the developer asks for it; new knowledge
and every lesson reach GBrain only through the memory governor and `mb-submit-memory`.

---

## Output Routing

Every artifact is written to its canonical place. Where that place is outside the step's output
folder, a copy is also written to `{slug}-project-library\pdlf-outputs\{step}\`, so that each
step's outputs for a project are all in one place.

---

## Checkpoint Writing

The ledger row, the BFT record and the Step Receipt are the complete checkpoint. No other
register is kept. The Step Receipt
is generated from the ledger row just written — it IS the ledger row, formatted for reading.
Never compose a receipt separately.
