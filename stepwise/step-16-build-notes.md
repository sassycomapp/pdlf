---
title: "step-16-build-notes"
doc-id: "mb-9bf919a4"
updated: "2026-10-10"
---
# Step 16 (domain-modeling) — Build Notes

## Correction 1 — wrong skill invoked in every prior draft

Old draft: "Run Matt [[[pdlf:stepwise/step-16-domain-modeling|Step 16 Domain Modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md) forward from Step 15's reviewed plan."
Confirmed against the real `SKILL.md` (mattpocock/skills,
`skills/engineering/domain-modeling/SKILL.md`): `/domain-modeling` has no
interview loop, no `AskUserQuestion`-equivalent sequence, no standalone
"run and get an artifact" shape. Its own description: "Use when the user
wants to pin down domain terminology... **or when another skill needs to
maintain the domain model**." It's infrastructure other skills call into.

Actual user-invocable skill: `/grill-with-docs`. Its entire `SKILL.md` body:
"Run a `/grilling` session, using the [[[pdlf:stepwise/step-16-domain-modeling|/domain-modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md) skill." `/grilling`
is the interview engine (tree of decisions, one at a time, recommended
answer, waits for feedback); [[[pdlf:stepwise/step-16-domain-modeling|/domain-modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md) fires inline during that
interview whenever a term needs sharpening or an ADR is warranted.

## Correction 2 — "reconciliation mode" had nothing left to attach to

Old draft branched on Step 3's disposition table (SKIP/RE-RUN/RUN-AS-NEW).
That model — and Step 3 itself — was retired system-wide this session
(session-decisions-and-learnings.md #2–4). Rather than reconstruct an
equivalent branch, checked whether [[[pdlf:stepwise/step-16-domain-modeling|/domain-modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md)'s own behavior already
covers the need: it does. "Cross-reference with code" — check whether the
code agrees with what's stated, surface contradictions — fires automatically
whenever code exists to check against. New-project entry has no code yet at
Step 16; the discipline is simply idle, no harm. Existing-project entry has
code, so it fires and does the reconciliation work the old draft's separate
mode was reaching for. One procedure, context differs by entry mode — same
principle already governing every other step.

## Correction 3 — file placement doesn't match Matt's default

Matt's skill defaults to `CONTEXT.md` + `docs/adr/000N-{slug}.md` at repo
root. PDLF already has an established ADR convention (`adr-local/`, paired
with `adr-global/`) predating this research. Resolved by explicit override
at invocation, same technique used for Step 14 overriding
[[[pdlf:stepwise/step-14-plan-ceo-review|/plan-ceo-review]]](C:/pdlf/stepwise/step-14-plan-ceo-review.md)'s design-doc auto-detection: state the destination paths
in the prompt rather than accepting the skill's default. Kept Matt's
numbering+slug filename convention; changed only the parent folder.

## Why included at all — addressed directly, not assumed

Developer asked directly whether this step earns its place before agreeing
to proceed. Answer given and accepted: PDLF's premise is a non-technical
developer running a multi-session pipeline with an agent that has no native
memory. GBrain solves that for facts; `CONTEXT.md` solves the same problem
for vocabulary. Without it, a term can drift meaning across sessions with no
one positioned to catch it before Phase B builds on top of the drift.

## Prerequisite confirmed via Step 11

Whether Matt Pocock skill setup (`setup-matt-pocock-skills`) happens for a
project PDLF builds, not just for `dev-makepdlf` itself, was open going into this
step. Step 11 item 16 confirms it does: "Set up system files... Set up Matt
Pocock skills configuration" runs for every project at init, both entry
modes. No separate check needed in Step 16 itself.

## Learnings

- Same lesson as Steps 14/15: a skill's name and its README blurb aren't
  enough — [[[pdlf:stepwise/step-16-domain-modeling|/domain-modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md) reads like a standalone workflow from its
  one-line description everywhere except its own `SKILL.md` body. Only
  reading the actual file caught this.
- Matt Pocock's skill ecosystem is structured differently from GStack's:
  small, single-purpose files that compose (`/grilling` + [[[pdlf:stepwise/step-16-domain-modeling|/domain-modeling]]](C:/pdlf/stepwise/step-16-domain-modeling.md)
  = `/grill-with-docs`) rather than large self-contained skills with their
  own preambles and telemetry. Worth expecting this pattern again for Steps
  19, 37, 38, 39, 40 (the other Matt Pocock steps) — check whether each of
  those is actually invoking a composed skill correctly before assuming the
  old drafts got it right.

## Open, not yet decided

- Whether Steps 19/37/38/39/40's Matt Pocock invocations have the same
  "wrong skill name" risk as this step did. Not checked yet — carry into
  each of those steps' own rebuild.
- `docs/agents/issue-tracker.md`-style config path (from
  `setup-matt-pocock-skills`) for the MB5PDLF project specifically — Step 11
  confirms the setup runs but doesn't spell out the resulting file paths.
  Not load-bearing for Step 16 itself; relevant when Step 19 ([[[pdlf:stepwise/step-19-to-tickets|Step 19 to Tickets]]](C:/pdlf/stepwise/step-19-to-tickets.md))
  is rebuilt.

## Global conventions applied throughout

- No `<project-library>` placeholder — `dev-{slug}\{slug}-project-library`
  in prose, full absolute path in any literal command
- No automatic git operations, anywhere, ever — including at this step's own gate.
  **Corrected 2026-08-25:** this convention previously read "gate maintenance
  commit/push is part of the gate ceremony itself... not a separate ask" — that was
  itself a violation of the no-automatic-git-operations rule stated in the very same
  bullet, and it was the one place in the whole pipeline where this rule was silently
  broken. Commit/push (and memory submission) at Step 16 are now asked, separately,
  only after the gate has been explicitly approved — same as every other step, just
  covering both repos instead of one.
- No Step 3 / disposition-table / the retired `sop-existing-project-resume-audit.md`
  references anywhere in this file
- Naming follows [[[default:specifications-global/spec-nomenclature|Spec: Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md)'s Stepwise File Naming table

## Later decisions

1. **Gate-housekeeping ordering corrected, 2026-08-25.** Master task list, item 9.3.
   The real step file had "full maintenance: commit + push both repos, GBrain sync +
   embed on both sources" running before the gate summary was even presented for
   approval — a genuine defect, contradicting the rule stated explicitly elsewhere in
   this document set. Fixed: the gate now runs its full ceremony through explicit
   developer approval first; only after approval are the two housekeeping questions
   asked, separately, each covering both the code repo and the docs repo.
2. **`/sync-gbrain` replaced with the `mb-submit-memory` skill, submitting through the
   memory governor.** `CONTEXT.md` and each real ADR (if any) are submitted
   individually, each its own separate call — never batched together, even though
   Step 16 can produce a genuinely variable number of ADRs.
3. **`gbrain dream` and `gbrain eval suspected-contradictions` added to end-of-step
   housekeeping.** Run for real, never as a dry run.
4. **`mb-submit-memory` skill built and installed, 2026-08-25.** Queries GBrain for
   related content, forms a real confidence score and contradiction judgment, reports
   its findings, and only submits after explicit developer approval.
5. **`mb-sentinel-review` invoked at item 7, 2026-08-27.** Step 16 matches
   the retired `sentinel-security-system-plan.md` Section 9's own table exactly — "Domain model,"
   Low/Medium scrutiny, "sensitive data or security-relevant entities being created?"
   Placed after `CONTEXT.md` is updated (item 5) and ADRs are offered (item 6), before
   the gate — a real `FLAG` or `ESCALATE` finding is part of what the developer
   approves at `domain-locked`, not something surfaced only afterward. `mb-sentinel-review`
   itself never implements a fix; it stops and reports, per its own hard rules.
   Renumbered items 7 through 14 to 8 through 15 to accommodate this insertion; one
   stale cross-reference ("asked at item 13") corrected to item 14 in the Reference
   section as a result.
6. **Two real gaps found and closed, 2026-08-27.** First: a CLEAR outcome from
   `mb-sentinel-review` left no durable record — nothing to prove the review ever ran,
   once the conversation ended. Fixed: `triage_label` gained a sixth allowed value,
   `'clear'`, via a real migration, and the skill now writes a resolved row on CLEAR,
   the same as it already did for FLAG and ESCALATE. Second: nothing verified item 7's
   instruction to invoke `mb-sentinel-review` was actually followed, rather than
   silently skipped — a written instruction alone was never a guarantee, the same
   principle already applied everywhere else in this document set. Fixed: new item 9
   requires a real `triage_findings` row to exist for this step's `step_id` before the
   gate procedure may begin — no row, no gate, a deviation request instead. Items 9
   through 15 renumbered from the prior 8 through 14 as a result; one further stale
   cross-reference ("asked at item 14") corrected to item 15.
