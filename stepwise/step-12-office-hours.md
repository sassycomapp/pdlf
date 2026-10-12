---
title: "step-12-office-hours"
doc-id: "mb-f5ca1c50"
updated: "2026-10-12"
---
## Task Execution Order

1. Query GBrain for context relevant to product ideation (automatic, read-only).
2. → If **new-project entry**: follow items 3–5.
   → If **existing-project entry**: follow items 3e–5e.

### New-project entry

3. Read the three pre-project documents from
   `dev-{slug}\{slug}-project-library\pre-project\`.
4. Query the developer diligently. If the scope is not adequately described, ask the
   developer to explain further. Repeat until satisfied — this is a from-scratch
   interrogation; there is no existing material to work from yet.
5. Continue at item 6.

### Existing-project entry

3e. Read the entire existing project-library via GBrain (it was registered as a source
    at Step 11) — not a brute-force read of every file. The goal is to identify what is
    canonical (the project's fundamental, durable concept) versus what is consequential
    (decisions and artifacts that followed from that concept but aren't the concept
    itself).
4e. → Decision point: if any existing document already claims to state the project's
    concept — an old `design-doc.md`, `CONTEXT.md`, a prior `design-doc-first-concept.md`
    — surface it to the developer explicitly and plainly: "here's what already exists."
    Do not fold it silently into the general read.
5e. Independently propose a canonical/consequential split across the whole
    project-library. Present that proposal side by side with anything surfaced at item
    4e, naming where they agree and where they diverge. The developer confirms or
    corrects the proposal — this is not a from-scratch interrogation, it is
    propose-and-confirm.

### Convergence — synthesis onward, identical regardless of entry mode

6. Synthesize a design doc using this structure: Problem Statement, Demand Evidence,
   Status Quo, Target User & Narrowest Wedge, Constraints, Approaches Considered,
   Recommended Approach, Open Questions, Success Criteria. This always runs, regardless
   of what the developer decides at item 8 — it does not depend on declining
   [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md). For existing-project entry, this doc represents the redeveloped
   concept — built from what was identified as canonical, not a copy of consequential
   material.
7. Save the synthesized draft to two files:
   - `dev-{slug}\{slug}-project-library\docs-local\design-doc-first-concept.md` — permanent, never
     overwritten again. This is the project's first concept draft, kept for later
     concept-drift checking.
   - `dev-{slug}\{slug}-project-library\docs-local\design-doc.md` — the current working copy. May
     be replaced below.
8. Ask the developer: "Run [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md)? (yes/no)"

### If the developer declines [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md)

8a. Ledger: `status = complete`, `synthesized = true`,
    `artifact_path = dev-{slug}\{slug}-project-library\docs-local\design-doc.md`.
8b. Downstream steps get an INPUT NOTICE on their receipts (synthesized-input
    propagation).

### If the developer accepts [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md)

8c. Pre-load into the [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) invocation prompt: the source material read at
    item 3 or 3e, and the full text of `design-doc-first-concept.md` — included directly
    in the prompt, not just referenced by path, so the skill recognizes it as a fully
    formed plan. Confirmed against the skill's own source: a fully formed plan skips its
    interview questions but still runs Premise Challenge and Alternatives Generation.
8d. Invoke GStack [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md).
8e. The skill saves its output to its own GStack-native path:
    `~/.gstack/projects/sassycomapp-dev-{slug}\{slug}-project-library/{user}-{branch}-design-{datetime}.md`.
8f. Capture the output path the skill reports.
8g. Copy that file to `dev-{slug}\{slug}-project-library\docs-local\design-doc.md`, replacing the
    working copy. `design-doc-first-concept.md` is never touched again after item 7.
8h. Ledger: `status = complete`, `synthesized = false`,
    `artifact_path` = the GStack-native path.
8i. Never modify or move the GStack-native file — GStack skills expect it to stay put.

### Convergence — both paths

9. Verify `docs-local\design-doc.md` exists. If [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) ran, also verify the
   GStack-native path exists.
10. If either is missing: deviation request per [[[makepdlf-project-library:specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).
11. Write the Step 12 ledger row with `completed_at`.
12. Save the Step Receipt to `dev-{slug}\{slug}-project-library\pdlf\step-12-receipt.md`.
13. Apply BFT per [[[makepdlf-project-library:specifications-local/spec-bft|Spec: BFT]]](C:/dev/dev-makepdlf/makepdlf-project-library/specifications-local/spec-bft.md) at **Full**.
14. Ask separately: "Commit and push to GitHub?"
15. Ask separately: "Run the end-of-step memory sequence?" This covers five actions, in
    this exact order, every time — do not skip any of them and do not reorder them:
    (1) invoke the `mb-submit-memory` skill for `design-doc-first-concept.md` and for
    `design-doc.md`, each as its own separate submission, using the `pdlf_step_sync`
    credential — this is a PDLF step's own routine housekeeping, not a developer's
    independent, ad-hoc request — these are the only two real,
    developer-relevant files this step produces; (2) run `gbrain dream` for real —
    NEVER `--dry-run`; a dry run writes nothing at all and is not a valid substitute for
    this step; (3) run `gbrain eval suspected-contradictions` immediately afterward —
    this does NOT run automatically as part of `gbrain dream` and must be invoked as its
    own separate command; (4) read what that command reports; (5) if anything is marked
    high-severity, STOP and present it to the developer before continuing. Do not
    resolve, dismiss, or silently proceed past a high-severity finding.
16. Present the Step Receipt to the developer. Stop, wait for "continue."
17. Ask: "Continue to step 14?"

---

## Description

Step 12 always produces a synthesized design doc first, regardless of what happens
after. What differs by entry mode is never *whether* this happens, only what source
material it draws from and how the developer is engaged:

- **New-project entry** has no existing material — the agent interrogates the developer
  from scratch, using the three pre-project files as a starting point.
- **Existing-project entry** has a whole project-library already — the agent reads it,
  separates canonical from consequential, and the developer confirms or corrects that
  read rather than being asked to explain from nothing. Submitting an existing project
  to PDLF means redeveloping it around its canonical concept. It is not an audit,
  maintenance pass, or correction of what already exists.

Either way, the result is the same: a permanent first-concept draft
(`design-doc-first-concept.md`) and a working copy (`design-doc.md`). Only after that
draft exists is the developer asked whether to also run [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md). If declined,
the synthesized draft stands as the final design doc for this step. If accepted, the
draft is handed to [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) as a fully formed plan — this lets the skill skip its
redundant interview questions while still forcing the draft through Premise Challenge
and Alternatives Generation, so the underlying thinking still gets tested, not just
accepted. [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md)'s output then becomes the new working copy of
`docs-local\design-doc.md`; the first-concept draft is never overwritten.

**Decision made while drafting, flagged plainly:** the handoff to Step 14 was originally
specified as three artifacts (design doc, [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) output, Step Receipt). The
permanent first-concept draft is a fourth artifact that didn't exist when that was
specified. Its whole purpose is concept-drift checking — a downstream concern by
definition — so it's included in the handoff below. Confirm or correct.

## Inputs Required

- Entry mode, determined at Step 11 (new vs. existing)
- New-project entry: pre-project documents from
  `dev-{slug}\{slug}-project-library\pre-project\`
- Existing-project entry: the existing project-library, via its registered GBrain source
- Developer's answers during the diligent-querying or propose-and-confirm pass
- Developer's yes/no decision on running [[[makepdlf-project-library:stepwise/step-12-office-hours|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md)
- GBrain query at item 1 (automatic, read-only)

## Outputs

| Artifact | Path | Notes |
|---|---|---|
| First concept draft | `dev-{slug}\{slug}-project-library\docs-local\design-doc-first-concept.md` | Permanent, written once, never overwritten again |
| Working design doc | `dev-{slug}\{slug}-project-library\docs-local\design-doc.md` | Either the synthesized draft (declined) or the [[[makepdlf-project-library:stepwise/step-12-office-hours\|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) output (accepted) |
| [[[makepdlf-project-library:stepwise/step-12-office-hours\|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md) output (if it ran) | `~/.gstack/projects/sassycomapp-dev-{slug}\{slug}-project-library/{user}-{branch}-design-{datetime}.md` | GStack-native, never modified or moved |
| Step Receipt | `dev-{slug}\{slug}-project-library\pdlf\step-12-receipt.md` | |
| BFT record | — | Full |

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 12 | Skill (conditional) | | GStack [[[makepdlf-project-library:stepwise/step-12-office-hours\|/office-hours]]](C:/dev/dev-makepdlf/makepdlf-project-library/stepwise/step-12-office-hours.md), or OpenCode synthesis, or both |

---

## Handoff

Step 14 **must** run — not optional, not skippable. It takes into context, together:

- `dev-{slug}\{slug}-project-library\docs-local\design-doc.md`
- `dev-{slug}\{slug}-project-library\docs-local\design-doc-first-concept.md`
- The `/office-hours` output file, if `/office-hours` ran
- The Step 12 Step Receipt

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: `[[spec-execution-discipline]]`
For BFT procedure: `[[spec-bft]]`

GBrain querying is automatic and read-only. Getting new content into durable memory is a
write action and is never automatic — always asked. It goes through the `mb-submit-memory`
skill and the five-action sequence described at item 15, never GStack `/sync-gbrain`.

Git operations (commit, push) are permission-only, per the global [[[makepdlf-project-library:agents|AGENTS.md]]](C:/dev/dev-makepdlf/makepdlf-project-library/AGENTS.md) —
never automatic, never run without the developer's explicit approval first.

The ledger row, Step Receipt, and devlog-index/judgement-trail entries are the complete
checkpoint. No separate state file or completion report.
