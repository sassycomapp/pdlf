---
title: "step-14-plan-ceo-review"
doc-id: "mb-c449927c"
updated: "2026-10-12"
---
## Task Execution Order

1. Query GBrain for context relevant to scope and strategy review (automatic,
   read-only). Sources nominated explicitly: `{slug}`, `{slug}-project-library`,
   `project-library-global`.
2. Check Step 12's `synthesized` flag in the ledger. If `true`, this step's receipt
   will carry an INPUT NOTICE per [[[makepdlf-project-library:policy-local/step-conditional-state-policy|Step Conditional State Policy]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/step-conditional-state-policy.md), and item 5
   below applies (design doc not present at the skill's canonical path).
3. Assemble Step 12's four-artifact handoff into context:
   - `dev-{slug}\{slug}-project-library\docs-local\design-doc.md`
   - `dev-{slug}\{slug}-project-library\docs-local\design-doc-first-concept.md`
   - The `/office-hours` GStack-native output file, if `/office-hours` ran
     (`synthesized = false` on Step 12's ledger row)
   - The Step 12 Step Receipt
4. Local/global conflict check: compare anything in `{slug}-project-library` that
   this review touches against `project-library-global`. Global wins by default.
   A real reason to diverge goes through a deviation request to the developer —
   see § Local/Global Conflict Check below.
5. Invoke GStack [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md), pasting the full text of all four artifacts
   from item 3 directly into the invocation prompt. State explicitly in the
   invocation that a design doc already exists and is provided above — this
   preempts the skill's own pre-review design-doc check (confirmed in its
   `SKILL.md`: it globs `~/.gstack/projects/$SLUG/*-design-*.md`, and if
   `synthesized = true` at Step 12 that glob finds nothing, triggering a "No
   design doc found" prerequisite offer to run [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) inline). That
   decision was already made at Step 12; it is not re-opened here.
6. [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md) runs its full review: pre-review system audit, Step 0
   (premise challenge, existing code leverage, dream state mapping, implementation
   alternatives, mode selection: SCOPE EXPANSION / SELECTIVE EXPANSION / HOLD
   SCOPE / SCOPE REDUCTION), 11-section deep review, completion summary.
7. Mode-dependent output capture — confirmed against `SKILL.md` § "0D-POST.
   Persist CEO Plan": the skill only writes a file to
   `~/.gstack/projects/$SLUG/ceo-plans/` for EXPANSION and SELECTIVE EXPANSION
   modes. For HOLD SCOPE and SCOPE REDUCTION, nothing is persisted to that
   directory — the review and `## GSTACK REVIEW REPORT` exist only in the
   conversation/plan-mode output. See § Mode-Dependent Persistence below for
   how each case is captured.
8. Capture the plan artifact per item 7's mode branch.
9. Copy/save the plan artifact to `dev-{slug}\{slug}-project-library\output-gstack\makepdlf-step-14-ceo-plan.md`.
10. Verify the output exists: GStack-native file (EXPANSION/SELECTIVE EXPANSION)
    or orchestrator-saved transcript capture (HOLD SCOPE/REDUCTION), plus the
copy at `output-gstack\`. If missing: STOP, present a deviation request per
[[[makepdlf-project-library:specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).
11. Write Step 14 `steps` ledger row: `step_number = 14`, `type = 'SKILL'`,
    `status = 'complete'`, `synthesized = false`, `artifact_path` = the path
    captured at item 8.
12. Save Step Receipt to `dev-{slug}\{slug}-project-library\pdlf\step-14-receipt.md`.
13. Apply BFT per [[[makepdlf-project-library:specifications-local/spec-bft|Spec: BFT]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) at **Full** (scope and
    ambition review, strategic decisions).
14. Ask separately: "Commit and push to GitHub?"
15. Ask separately: "Run the end-of-step memory sequence?" This is five actions, in
    order, every time: (1) invoke the `mb-submit-memory` skill, using the
    `pdlf_step_sync` credential — this is a PDLF step's own routine housekeeping, not a
    developer's independent, ad-hoc request — for
    `output-gstack\makepdlf-step-14-ceo-plan.md` — this file exists in every mode and is always
    submitted; ALSO invoke `mb-submit-memory` the same way for the real GStack-native
    plan file if
    this run's mode was SCOPE EXPANSION or SELECTIVE EXPANSION — that file only exists
    for those two modes, so for HOLD SCOPE or SCOPE REDUCTION, only the first submission
    happens; (2) run `gbrain dream` for real, NEVER `--dry-run`; (3) run `gbrain eval
    suspected-contradictions` immediately afterward; (4) read what it reports; (5) if
    anything is marked high-severity, STOP and present it to the developer before
    continuing.
16. Present the Step Receipt. Stop, wait for "continue."
17. Ask: "Continue to Step 15?"

---

## Description

CEO/founder-mode scope and ambition review. Challenges premises and finds the
10-star version. [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md) offers four modes: SCOPE EXPANSION (dream
big), SELECTIVE EXPANSION (hold scope + cherry-pick expansions), HOLD SCOPE
(maximum rigor), SCOPE REDUCTION (strip to essentials). The developer selects
the mode — every scope change is an explicit opt-in via `AskUserQuestion`, and
once selected the skill commits to it (confirmed in source: "If EXPANSION is
selected, do not argue for less work during later sections... If REDUCTION is
selected, do not sneak scope back in").

Step 14 is entered directly from Step 12. There is no Step 13 in this pipeline
— it was removed (confirmed in [[[makepdlf-project-library:policy-local/pol-skill-invocation|Policy: Skill Invocation]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/pol-skill-invocation.md): `to-prd`/`to-spec`
had no confirmed downstream consumer, verified directly against
[[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md)'s own GBrain query schema, which does not reference an
issue-tracker or spec artifact at all).

There is no branch on how Step 12 produced its design doc. Step 12 always
hands off the same four artifacts regardless of whether [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) ran;
Step 14 always loads all four directly into the [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md) prompt, in
full text, before invoking it — the same move Step 12 itself used when handing
its draft to [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md).

This is more than a style preference here: it's load-bearing. Confirmed
directly against `SKILL.md`'s pre-review system audit, the skill runs its own
design-doc check regardless of what's pasted into the prompt:

```bash
DESIGN=$(ls -t ~/.gstack/projects/$SLUG/*-$BRANCH-design-*.md 2>/dev/null | head -1)
[ -z "$DESIGN" ] && DESIGN=$(ls -t ~/.gstack/projects/$SLUG/*-design-*.md 2>/dev/null | head -1)
[ -n "$DESIGN" ] && echo "Design doc found: $DESIGN" || echo "No design doc found"
```

If Step 12 ran [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) (`synthesized = false`), this glob finds the
real GStack-native design doc and the check passes harmlessly — redundant with
the paste, not in conflict with it. If Step 12 declined (`synthesized = true`),
no file exists at that path, the glob comes up empty, and the skill's own
"Prerequisite Skill Offer" fires: it asks the developer whether to run
[[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) inline, right there in Step 14. That would silently re-open a
decision Step 12 already settled. Item 5 above exists specifically to preempt
this — the invocation states plainly that a design doc already exists and is
provided in the prompt, so the offer never triggers.

The skill runs a pre-review system audit (git history, TODOs, existing code,
the design-doc check above, and a handoff-note check for
`*-ceo-handoff-*.md` from a prior paused session), then Step 0 (premise
challenge, dream state mapping, implementation alternatives, mode selection),
followed by an 11-section deep review covering architecture, error/rescue map,
security/threat model, data flow & interaction edge cases, code quality,
tests, observability, database/state management, API design,
performance/scalability, and design/UX. Confirmed against the actual
[[[makepdlf-project-library:stepwise/skill-source-reference/plan-eng-review-review-sections|Plan Eng Review Review Sections]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/skill-source-reference/plan-eng-review-review-sections.md) skill source: sections 1–11 are mandatory, non-skippable,
and each stops for `AskUserQuestion` per finding rather than batching findings
into a single plan write (the "anti-shortcut clause").

Steps 14–15 jointly produce the test plan consumed by Steps 35 and 38. Step 14
identifies what must be tested and why — the scope of testing. Step 15 produces
the concrete test specification.

## Mode-Dependent Persistence

Confirmed against `SKILL.md` § "0D-POST. Persist CEO Plan (EXPANSION and
SELECTIVE EXPANSION only)" — this is genuinely mode-dependent, not a gap in
the reference material:

- **EXPANSION / SELECTIVE EXPANSION:** the skill itself writes to
  `~/.gstack/projects/$SLUG/ceo-plans/{date}-{feature-slug}.md`, where `$SLUG`
  resolves via `$GSTACK_BIN/gstack-slug` (falling back to the
  git toplevel's basename). This matches the confirmed repo-naming form for this docs repo —
  `sassycomapp-{slug}-project-library` — since [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md) and
  [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) both run against the same repo and resolve `$SLUG` the same
  way. The orchestrator captures this path from the skill's own output and
  copies it to `output-gstack\makepdlf-step-14-ceo-plan.md`. Never modified in place —
  Step 15 appends its own review report to this same GStack-native file.
- **HOLD SCOPE / SCOPE REDUCTION:** nothing is written to `ceo-plans/`. The
  review and its `## GSTACK REVIEW REPORT` exist only as conversational
  output. The orchestrator itself saves this transcript to
  `dev-{slug}\{slug}-project-library\output-gstack\makepdlf-step-14-ceo-plan.md` — there
  is no GStack-native file to copy from in these two modes. Step 15 will not
  find an automatic canonical path to append to either; the orchestrator
  supplies the `output-gstack\` copy directly into Step 15's invocation
  prompt instead, same principle as item 5 above.

## Local/Global Conflict Check

Step 14 (with Step 15) is where anything in `{slug}-project-library` this
review touches gets checked against `project-library-global`.

- Default resolution: **global wins.**
- A real reason to diverge from a global standard goes through a deviation
  request to the developer — the same mechanism used everywhere else in PDLF,
  not a new one.
- Depends on `project-library-global` already being a real, GBrain-registered,
  queryable source. Per [[[makepdlf-project-library:adr-local/project-library-global-registration|Project Library Global Registration]]](C:/dev/dev-makepdlf/makepdlf-project-library/adr-local/project-library-global-registration.md),
  exactly where PDLF verifies this foundational layer is in place is still
  open (Step 11 check vs. a separate bootstrap procedure) — if it is not yet
  registered when Step 14 runs, that is itself a deviation request, not a
  silent skip.
- Mechanics confirmed, not assumed: [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md)'s `SKILL.md` has zero
  awareness of `project-library-global` — no reference to it anywhere in
  source. The conflict check is therefore entirely OpenCode's own structured
  comparison, run alongside the skill invocation, not something the skill
  surfaces on its own.

## Inputs Required

- Step 12's four-artifact handoff, pasted in full into the invocation prompt:
  - `dev-{slug}\{slug}-project-library\docs-local\design-doc.md`
  - `dev-{slug}\{slug}-project-library\docs-local\design-doc-first-concept.md`
  - [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) GStack-native output file, if it ran
  - Step 12 Step Receipt
- `project-library-global` content relevant to this review, for the
  local/global conflict check (OpenCode-run, not skill-run — see above)
- Prior CEO-review handoff note if present — the skill reads
  `~/.gstack/projects/$SLUG/*-$BRANCH-ceo-handoff-*.md` automatically; the
  orchestrator does not need to supply this
- Developer's mode selection during Step 0 (SCOPE EXPANSION / SELECTIVE
  EXPANSION / HOLD SCOPE / SCOPE REDUCTION)
- GBrain query at substep 1 (automatic, read-only, sources explicitly
  nominated)

## Outputs

| Artifact | Location | Notes |
|---|---|---|
| CEO plan + review report (GStack-native) | `~/.gstack/projects/{slug}/ceo-plans/{date}-{feature-slug}.md` | EXPANSION / SELECTIVE EXPANSION only. `$SLUG` = `sassycomapp-{slug}-project-library` form, confirmed. Living document — Step 15 appends to it. |
| CEO plan + review report (transcript capture) | Orchestrator-saved, no GStack-native source | HOLD SCOPE / SCOPE REDUCTION only — the skill persists nothing in these modes. |
| CEO plan + review report (stable copy) | `dev-{slug}\{slug}-project-library\output-gstack\makepdlf-step-14-ceo-plan.md` | Captures state after Step 14 either way. Step 15 updates this copy after appending the Eng review. |
| Test plan scope | Within the plan artifact | What must be tested and why — flows, roles, edge cases. Produced jointly with Step 15. Consumed by Steps 35 and 38. |
| Step Receipt | `dev-{slug}\{slug}-project-library\pdlf\step-14-receipt.md` | No `outputs` subfolder |
| BFT record | — | Full |

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 14 | Skill | | GStack [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review\|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md) |

---

## Handoff to Step 15

Step 15's [[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md) needs the CEO plan (this step's output), the
design doc, and the design doc's first-concept draft. Same principle applied
throughout: paste directly into context. For EXPANSION/SELECTIVE EXPANSION,
[[[makepdlf-project-library:stepwise/step-15-plan-eng-review|/plan-eng-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-15-plan-eng-review.md) will also find the GStack-native plan file automatically at
its canonical path (same `$SLUG` resolution). For HOLD SCOPE/REDUCTION, there
is no canonical file to find — Step 15 must be given the `output-gstack\`
copy directly.

### INPUT NOTICE Propagation

If Step 12 was synthesized (`synthesized = true`), this step's receipt shows:

```
INPUT NOTICE: Input from Step 12 was synthesized (OpenCode synthesized from
pre-project docs), not a full skill run. Treat this step's output as
provisional to the same degree.
```

Per [[[makepdlf-project-library:policy-local/step-conditional-state-policy|Step Conditional State Policy]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/step-conditional-state-policy.md), this propagates to every downstream
step whose `inputs_used` includes Step 12 — Steps 15, 19, and 21.

### Artifact Table

| Artifact | Location |
|---|---|
| CEO plan + review report (GStack-native, EXPANSION/SELECTIVE EXPANSION only) | `~/.gstack/projects/{slug}/ceo-plans/{date}-{feature-slug}.md` |
| CEO plan + review report (stable copy, all modes) | `dev-{slug}\{slug}-project-library\output-gstack\makepdlf-step-14-ceo-plan.md` |
| Test plan scope | Within the plan artifact |
| Ledger row | `steps` table — `step_number = 14`, `status`, `synthesized`, `artifact_path` |
| Step Receipt | `dev-{slug}\{slug}-project-library\pdlf\step-14-receipt.md` |
| BFT record | `bft_records` table — Full |
| Devlog index | `dev-{slug}\{slug}-project-library\pdlf\devlog-index.md` — updated |
| Judgement trail | `dev-{slug}\{slug}-project-library\pdlf\judgement-trail.md` — updated |

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode
directly — confirmed here: [[[makepdlf-project-library:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-14-plan-ceo-review.md) was checked against
[[[makepdlf-project-library:policy-local/pol-skill-invocation|Policy: Skill Invocation]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/pol-skill-invocation.md)'s skill-use principle and found to add real, unique
value (the 11-section adversarial review with mandatory `AskUserQuestion`
stops is not something OpenCode would replicate natively).

For execution sequence: [[[makepdlf-project-library:specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[makepdlf-project-library:specifications-local/spec-bft|Spec: BFT]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md)
For conditional-state definitions: [[[makepdlf-project-library:policy-local/step-conditional-state-policy|Step Conditional State Policy]]](C:/dev/dev-makepdlf/makepdlf-project-library/policy-local/step-conditional-state-policy.md)
For ledger schema: [[[makepdlf-project-library:specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-postgres-ledger.md)

GBrain is queried automatically at substep 1. Getting new content into durable memory is
never auto-run — it is asked at item 15, through the `mb-submit-memory` skill and the
five-action sequence described there, never GStack `/sync-gbrain`. The two housekeeping
questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the
complete checkpoint. No separate state file, devlog file, or completion
report.

Skills save where designed. PDLF process artifacts go to
`dev-{slug}\{slug}-project-library\pdlf\`.
