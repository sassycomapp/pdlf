---
title: "14-build-notes"
doc-id: "mb-3e9404a6"
updated: "2026-10-11"
---
# Step 14 (plan-ceo-review) — Build Notes

Captured during discussion, before this step file was rebuilt. Points to carry forward.

## Task list (matches `14-plan-ceo-review.md`)

1. Query GBrain (automatic, read-only) — sources explicitly nominated:
   `{slug}`, `{slug}-project-library`, `project-library-global`
2. Check Step 12's `synthesized` flag — determines whether item 5's design-doc
   preemption is load-bearing or redundant
3. Assemble Step 12's four-artifact handoff into context (design doc, first-concept
   draft, [[[pdlf:app-factory/phase-b-discover-and-define/12-office-hours|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/12-office-hours.md) output if it ran, Step 12 Step Receipt)
4. Local/global conflict check — global wins by default, deviation request to diverge
5. Invoke [[[pdlf:app-factory/phase-b-discover-and-define/14-plan-ceo-review|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/14-plan-ceo-review.md), pasting all four artifacts in full, stating explicitly
   that a design doc already exists
6. Skill runs pre-review system audit → Step 0 (mode selection) → 11-section review
7. Mode-dependent output capture (see below)
8–9. Capture and copy the plan artifact to `gstack-outputs\step-14-ceo-plan.md`
10. Verify outputs exist; deviation request if missing
11–13. Ledger row, Step Receipt, BFT Full
14–17. Housekeeping questions, present receipt, ask to continue

## Core principle — no branch on Step 12's provenance

Step 12 always hands off the same four artifacts regardless of whether
[[[pdlf:app-factory/phase-b-discover-and-define/12-office-hours|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/12-office-hours.md) ran. Step 14 always pastes all four into the [[[pdlf:app-factory/phase-b-discover-and-define/14-plan-ceo-review|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/14-plan-ceo-review.md)
prompt, in full text, before invoking it — never relies on the skill's own
design-doc glob. This mirrors Step 12's own handling of [[[pdlf:app-factory/phase-b-discover-and-define/12-office-hours|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/12-office-hours.md).

Explicitly rejected during this build: the old draft's Branch A ("no design doc
found") / Branch B ("design doc found") split. That framing assumed the skill's
internal detection determines the procedure. It doesn't — the orchestrator's own
handoff does. One procedure, not two.

## Skill-source findings — confirmed, not assumed

`SKILL.md` and `SKILL.md.tmpl` for [[[pdlf:app-factory/phase-b-discover-and-define/14-plan-ceo-review|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/14-plan-ceo-review.md) were read directly (not
inferred from Plan Eng Review Review Sections/`manifest.json` alone, which only cover the
11-section review gated behind Step 0). Three findings changed what the old
draft assumed:

1. **GStack-native plan path uses `sassycomapp-{slug}-project-library`, not
   bare `{slug}`.** `$SLUG` resolves via `~/.claude/skills/gstack/bin/gstack-slug`
   (falling back to the git toplevel's basename). This is the same resolution
   [[[pdlf:app-factory/phase-b-discover-and-define/12-office-hours|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/12-office-hours.md) uses, and matches the form already confirmed in
   `project-inventory.md` for every registered project's GStack path. The old
   draft's `~/.gstack/projects/{slug}/ceo-plans/...` was the exact same class of
   error already caught once for [[[pdlf:app-factory/phase-b-discover-and-define/12-office-hours|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/12-office-hours.md)'s design-doc path — caught
   again here by reading source instead of carrying the assumption forward.

2. **The skill runs its own design-doc glob regardless of what's pasted into
   the prompt**, and if it comes up empty (Step 12 declined [[[pdlf:app-factory/phase-b-discover-and-define/12-office-hours|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/12-office-hours.md),
   `synthesized = true`), the skill's own "Prerequisite Skill Offer" fires —
   asking the developer, inside Step 14, whether to run [[[pdlf:app-factory/phase-b-discover-and-define/12-office-hours|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/12-office-hours.md) inline.
   That would silently reopen a decision Step 12 already closed. This is why
   item 5 explicitly states in the invocation that a design doc already exists:
   not stylistic, load-bearing — it's the only thing that suppresses the
   re-offer.

3. **Plan-file persistence is mode-dependent.** Confirmed in `SKILL.md` §
   "0D-POST. Persist CEO Plan (EXPANSION and SELECTIVE EXPANSION only)" — HOLD
   SCOPE and SCOPE REDUCTION write nothing to `ceo-plans/`. This wasn't in
   either prior draft. Step 14 now branches its output-capture step: copy the
   GStack-native file for the two expansion modes, orchestrator-saves the
   conversational transcript for the other two.

## Local/global conflict check — mechanics resolved

[[[pdlf:app-factory/phase-b-discover-and-define/14-plan-ceo-review|/plan-ceo-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/14-plan-ceo-review.md)'s `SKILL.md` has zero reference to `project-library-global`
anywhere in source. The conflict check is confirmed to be entirely OpenCode's
own structured comparison, run alongside the skill invocation — not something
the skill surfaces on its own. This closes the "not yet verified" item carried
in the original `step-14-build-notes.md`.

Still open, per [[[pdlf:pdlf-library/adr-local/project-library-global-registration|Project Library Global Registration]]](C:/pdlf/pdlf-library/adr-local/project-library-global-registration.md): exactly
where PDLF verifies `project-library-global` itself is registered and
queryable (Step 11 check vs. separate bootstrap procedure). Step 14 treats a
missing registration as a deviation request, not a silent skip, but does not
resolve where that check belongs.

## Learnings

- **Reading a skill's `SKILL.md` directly, not just its section manifest,
  matters.** `manifest.json` + Plan Eng Review Review Sections alone would have left the
  design-doc preemption requirement, the mode-dependent persistence split, and
  the correct GStack path all unverified. All three were only findable in the
  actual `SKILL.md`.
- **"Never rely on the skill's internal detection" and "the skill runs its own
  detection anyway" are not in tension.** The orchestrator's paste is not a
  replacement for the skill's own audit — it's an explicit override, stated in
  the prompt, that prevents the audit's failure path (no design doc found) from
  triggering an unwanted re-ask. Both things are true at once.
- Ledger substep 11 rewritten against the real [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md)
  schema — `step_number`, `type`, `status`, `synthesized`, `artifact_path` are
  real columns, not assumed field names.

## Open, not yet decided

- Whether Step 15's [[[pdlf:app-factory/phase-b-discover-and-define/15-plan-eng-review|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/15-plan-eng-review.md) has the same mode-dependent persistence
  behavior, or always writes a file regardless of Step 14's mode. Not yet
  checked against [[[pdlf:app-factory/phase-b-discover-and-define/15-plan-eng-review|/plan-eng-review]]](C:/pdlf/app-factory/phase-b-discover-and-define/15-plan-eng-review.md)'s own `SKILL.md` — carry this question
  into that step's rebuild.
- Exact format of the "explicit design-doc-exists" statement in the invocation
  prompt (item 5) — a fixed template sentence, or freeform framing left to the
  orchestrator's judgment at invocation time? Not yet decided.

## Global conventions applied throughout

- No `<project-library>` placeholder — use `dev-{slug}\{slug}-project-library`
  in prose, full absolute path in any literal command
- No automatic git operations anywhere — every commit/push is asked
- No automatic memory-governor submission — asked, via the `mb-submit-memory` skill only
- No Step 13 references anywhere in this file — purged per the handover's
  explicit requirement
- No "Branch A/B" language — described plainly instead

## Later decisions

1. **`/sync-gbrain` replaced with the `mb-submit-memory` skill, submitting through the
   memory governor.** Same system-wide change as Steps 11 and 12 (master task list,
   items 9.2 and 9.4, which names `[[14-plan-ceo-review]]` directly). Applied here
   to this step's one `/sync-gbrain` mention, item 15. Both of this step's real
   artifacts get submitted, individually: the stable copy at
   `gstack-outputs\step-14-ceo-plan.md`, which exists in every mode, and the real
   GStack-native plan file, which only exists for SCOPE EXPANSION and SELECTIVE
   EXPANSION — for HOLD SCOPE and SCOPE REDUCTION, only the stable copy is submitted,
   since nothing else was written. Also fixed while touching this section: the old
   `[[14-plan-ceo-review]]` Reference section pointed to "substep 10" for the
   syncing question — item 10 is actually the deviation-request line, not the
   housekeeping question, which is item 15. Corrected.
2. **`gbrain dream` and `gbrain eval suspected-contradictions` added to end-of-step
   housekeeping.** Master task list, item 9.8 — applies to every step. Run for real,
   never as a dry run. `gbrain eval suspected-contradictions` does not run
   automatically as part of `gbrain dream` and must be invoked as its own separate
   command every time.
3. **`mb-submit-memory` skill built and installed, 2026-08-25.** Same skill used at
   Steps 11 and 12 — queries GBrain for related content, forms a real confidence score
   and contradiction judgment using a concrete, bounded method, reports its findings,
   and only submits after explicit developer approval. See the skill's own file for the
   full procedure.
