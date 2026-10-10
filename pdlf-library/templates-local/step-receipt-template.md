---
title: "step-receipt-template"
doc-id: "mb-c0c99119"
updated: "2026-10-10"
---
# PDLF Step Receipt Template

**What this is:** The single structured readout shown at every stop, after every step. It is
generated directly from the row(s) just written to the Postgres ledger — not composed
separately by the agent. If a value doesn't appear in the ledger row, it doesn't appear on the
receipt.

**Where it's shown:** Inline, in the conversation, at the end of every step — this is what you
review before deciding whether to say "continue."

**Where it's also saved:** As a file, `dev-{slug}\{slug}-project-library\pdlf\step-{step_number}-receipt.md`, so
the full run has a readable, git-tracked history alongside the queryable ledger.

---

## Template

```markdown
# Step Receipt — {project_slug} — Step {step_number}

Phase: {phase}   |   Type: {step_type}   |   Status: {status}
Started: {started_at}   |   Completed: {completed_at}

## What was invoked

Skill family: {skill_family}
Skill: {skill_name}
Inputs used: {inputs_used}

## Output

Artifact: {artifact_path}
Synthesized (test-mode shortcut): {synthesized}   <!-- only rendered if TRUE, and rendered
                                                        prominently — never silently omitted -->

## BFT checkpoint

Level applied: {bft_level}    <!-- full | light | none -->
<!-- if full or light, render the six fields below; if none, state "No BFT — mechanical
     pass-through step" and nothing else -->
Bones:   {bones}
Muscle:  {muscle}
Nerves:  {nerves}
Fat:     {fat}
Skin:    {skin}
Health:  {health}

## Gate status

<!-- only rendered if this step_type = 'gate' -->
Gate: {gate_name}
Passed: {passed}
Approved at: {approved_at}

## Deviation

<!-- only rendered if a deviation row exists for this step -->
Description: {description}
Options presented: {options_presented}
Decision: {decision}

## Ledger row written

<!-- the literal row(s) inserted, shown verbatim — this is the "shown, not just claimed" part -->
steps:        {raw steps row as inserted}
gates:        {raw gates row, if applicable}
bft_records:  {raw bft_records row, if applicable}
deviations:   {raw deviations row, if applicable}

## Housekeeping (asked every step, separately — never combined, never auto-run)

1. Commit and push this step's changes to GitHub? (y/n)
2. Sync and embed this step's artifacts to GBrain? (y/n)

## Blockers

<!-- always rendered, even when empty — state "None" explicitly rather than omitting the
     section, so its absence is never ambiguous with "not checked" -->
{blockers}

## Notes for next session

<!-- always rendered, even when empty — state "None" explicitly -->
{notes_for_next_session}

## Next action

{next_action}

---
Type "continue" to proceed to the next step, or raise anything you want changed first.
```

---

## Worked example

This is what a real receipt would look like for a gate step (Step 16, `domain-modeling`, in `full`
mode) — filled in with plausible values, so you can see the shape before it's wired up for real.

```markdown
# Step Receipt — mb5pdlf — Step 16

Phase: A   |   Type: skill   |   Status: complete
Started: 2026-07-04 14:02:11+00   |   Completed: 2026-07-04 14:09:47+00

## What was invoked

Skill family: matt-skills
Skill: /grill-with-docs (using domain-modeling internally)
Inputs used: {"plan_file": "ceo-plans/checkout-flow-2026-07-04.md", "context_md": "CONTEXT.md"}

## Output

Artifact: dev-{slug}\{slug}-project-library\CONTEXT.md, adr-local/0004-checkout-session-model.md
Synthesized (test-mode shortcut): false

## BFT checkpoint

Level applied: full
Bones:   Domain terms locked: Session, Cart, Reservation Hold
Muscle:  Logic — glossary terms had to necessarily follow from the reviewed plan, not invented
Nerves:  Analyzing — decomposed the plan into discrete named concepts
Fat:     Cut "Wishlist" as out-of-scope per ISA section 3
Skin:    Presented as glossary + ADR pair, conclusion-first
Health:  Good in itself — terms are consistent with existing CONTEXT.md; good for project — unblocks step 17/19

## Gate status

Gate: domain-locked
Passed: true
Approved at: 2026-07-04 14:11:03+00

## Housekeeping (asked every step, separately — never combined, never auto-run)

1. Commit and push this step's changes to GitHub? (y/n)
2. Sync and embed this step's artifacts to GBrain? (y/n)

## Blockers

None

## Notes for next session

Developer wanted "Wishlist" reconsidered for a future initiative — noted here so it isn't
forgotten, without reopening scope now.

## Next action

Proceed to Step 17 — manual creation of Anvil data tables per the ADR above.

---
Type "continue" to proceed to the next step, or raise anything you want changed first.
```

---

*Step Receipt template version 1.0. Consumes: `steps`, `gates`, `bft_records`, `deviations`
tables from the `pdlf` Postgres database. Produces: inline chat output +
`dev-{slug}\{slug}-project-library\pdlf\step-{step_number}-receipt.md`.*
