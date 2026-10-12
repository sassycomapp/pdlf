---
title: "b12-build-plan"
doc-id: "mb-19064cbb"
updated: "2026-10-12"
---

## From `12-build-notes.md`

# Step 12 — Build Notes: Full Task List

## Task list (matches [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|12-office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md))

1. Query GBrain (automatic, read-only)
2. Branch on entry mode, determined at Step 11

**New-project entry:**
3. Read the three pre-project docs from `dev-{slug}\{slug}-project-library\pre-project\`
4. Query the developer diligently, from scratch — loop until scope is adequately
   described

**Existing-project entry:**
3e. Read the whole existing project-library via GBrain — identify canonical (durable
    concept) vs. consequential (things that followed from it)
4e. If an existing document already claims to state the concept (old `design-doc.md`,
    `CONTEXT.md`, etc.), surface it explicitly — never fold it silently into the read
5e. Propose the canonical/consequential split, side by side with anything surfaced at
    4e. Developer confirms or corrects — propose-and-confirm, not from-scratch
    interrogation

**Both converge:**
6. Synthesize a design doc (always — not conditional on the [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) decision):
   Problem Statement, Demand Evidence, Status Quo, Target User & Narrowest Wedge,
   Constraints, Approaches Considered, Recommended Approach, Open Questions, Success
   Criteria. For existing-project entry, this represents the redeveloped concept, built
   from what was identified as canonical — not a copy of consequential material.
7. Save the draft to two files: `design-doc-first-concept.md` (permanent, never
   overwritten again) and `design-doc.md` (working copy)
8. Ask the developer: run [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md)? (yes/no)

**If declined:** ledger `synthesized = true`; downstream INPUT NOTICE.

**If accepted:** pre-load the source material (pre-project docs or the
propose-and-confirm result) and the full text of `design-doc-first-concept.md` into the
[[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) prompt — recognized as a fully formed plan, so it skips the interview
but still runs Premise Challenge and Alternatives. Invoke [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md). Capture its
GStack-native output path. Copy that file over `design-doc.md` (working copy only —
first-concept file untouched). Ledger `synthesized = false`. Never move the
GStack-native file.

**Both paths converge:**

9. Verify `design-doc.md` exists (and GStack path, if [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) ran)
10. If missing: deviation request
11. Write ledger row
12. Save Step Receipt to `dev-{slug}\{slug}-project-library\pdlf\step-12-receipt.md`
13. Apply BFT — Full
14. Ask separately: commit and push?
15. Ask separately: "Run the end-of-step memory sequence?" This is five actions, in
    order, every time: (1) invoke `mb-submit-memory` for `design-doc-first-concept.md`
    and for `design-doc.md`, each as its own separate submission; (2) run `gbrain dream`
    for real, NEVER `--dry-run`; (3) run `gbrain eval suspected-contradictions`
    immediately afterward; (4) read what it reports; (5) if anything is marked
    high-severity, STOP and present it to the developer before continuing.
16. Present Step Receipt, stop, wait for "continue"
17. Ask: continue to Step 14?

**Handoff:** Step 14 must run, taking into context together: `design-doc.md`,
`design-doc-first-concept.md`, the [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) output file (if it ran), and the
Step 12 Step Receipt. The first-concept file is a fourth artifact added during drafting
— flagged in the step file itself, not silently assumed.

## Core principle — existing-project entry

Submitting an existing project to PDLF means redeveloping it around its canonical
concept, not auditing, maintaining, or correcting what already exists. PDLF is a
development system, not a refactoring system. This principle also retired the
disposition-audit model entirely (`step-02-existing-registration.md`,
`step-03-resume-point-audit.md`, the retired `sop-existing-project-resume-audit.md` — all removed).
Every step always runs, for every project. What differs for an existing project is only
the material a step starts from, never whether the step runs.

## Learnings

- **[[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md) accepts a pre-written draft, confirmed from the actual skill file
  (not assumed).** It has a built-in "fully formed plan" path: if given one, it skips
  the interview questions but still forces the draft through Premise Challenge and
  Alternatives — pressure-tested, not rubber-stamped.
- **The draft must be pasted into the invocation prompt itself**, not just saved to a
  file. [[[pdlf:app-factory/phase-b-discover-and-define/b12-reference|/office-hours]]](C:/pdlf/app-factory/phase-b-discover-and-define/b12-reference.md)'s own Phase 1 does not scan our project folder — it only reads
  `CLAUDE.md`, `TODOS.md`, git history, and its own native design-doc history at
  `~/.gstack/projects/sassycomapp-dev-{slug}\{slug}-project-library/*-design-*.md`. None of those is our
  `docs-local\design-doc.md`.
- GStack-native save path confirmed correct against the actual skill file:
  `~/.gstack/projects/sassycomapp-dev-{slug}\{slug}-project-library/{user}-{branch}-design-{datetime}.md`.

## Global conventions applied throughout

- No `<project-library>` placeholder — use `dev-{slug}\{slug}-project-library` in prose, full
  absolute path in any literal command
- No automatic git operations anywhere — every commit/push is asked
- No automatic memory-governor submission — asked, via the `mb-submit-memory` skill only

## Later decisions

1. **`/sync-gbrain` replaced with the `mb-submit-memory` skill, submitting through the
   memory governor.** Same system-wide change as Step 11 (master task list, items 9.2
   and 9.4, which names `[[12-office-hours]]` directly). The old `/sync-gbrain`
   command reads whatever files happen to be sitting in a registered folder with nothing
   checking them first — which could silently undo a decision the memory governor
   already made about a piece of content. Applied here to this step's one `/sync-gbrain`
   mention, item 15. Both real files this step produces —
   `design-doc-first-concept.md` and `design-doc.md` — are submitted individually, each
   its own separate call. No boilerplate-versus-real-content question applies here the
   way it did at Step 11: both of these files are genuine, synthesized content, never
   copied template text.
2. **`gbrain dream` and `gbrain eval suspected-contradictions` added to end-of-step
   housekeeping.** Master task list, item 9.8 — applies to every step, not just Step 11.
   Run for real, never as a dry run; a dry run writes nothing and cannot serve as a
   check. `gbrain eval suspected-contradictions` does not run automatically as part of
   `gbrain dream` and must be invoked as its own separate command every time.
3. **`mb-submit-memory` skill built and installed, 2026-08-25.** Same skill used at
   Step 11 — it queries GBrain for related content, forms a real confidence score and
   contradiction judgment using a concrete, bounded method, reports its findings, and
   only submits after explicit developer approval. See the skill's own file for the full
   procedure.
