---
title: "c20-build-plan"
doc-id: "mb-696b4ce8"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 20: Design consultation

**Must achieve:** Builds the application's design system (`DESIGN.md`) on Material 3 and David's design standards. In a test run, the developer may abbreviate or skip it.

**Carried out by:** GStack, using `/design-consultation`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to design system
2. Check test-mode flag — Present abbreviation offer (full/abbreviate/skip) if in test mode
3. Invoke GStack `/design-consultation` — Researches landscape, builds DESIGN.md + preview page
4. Verify outputs — DESIGN.md written, font/color preview page, design tokens; STOP if missing
5. Write Step 20 ledger row — `completed_at`
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-20-receipt.md`
7. Apply BFT — Full level
8. Follow execution sequence — Housekeeping, stop, wait for continue

## From `pol-step-conditional-state.md`: Step 20 eligibility

### Step 20 — /design-consultation (test-mode-eligible)

Step 20 offers abbreviation when `projects.mode = "test"`:

- **Full:** Run complete [[[pdlf:app-factory/phase-c-design-and-plan/c20-reference|/design-consultation]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-reference.md) → `status = "complete"`, `synthesized = false`
- **Abbreviated:** Run collapsed version → `status = "complete"`, `synthesized = true`
- **Skip:** Developer declines entirely → `status = "skipped"`, `synthesized = false`

In full mode, the abbreviation offer is never presented. Step 20 runs fully or
is skipped.

## From `pol-step-conditional-state.md`: full mode

- Step 20: runs fully or is skipped (if conditional)

## From `spec-execution-discipline.md`: test-mode eligibility

When a project is in `test` mode, Step 20 is eligible for abbreviation. If the
developer chooses an abbreviated or skipped run, the step's `synthesized` flag is set to
`true` (abbreviated) or the step's `status` is set to `"skipped"` in the ledger.
Step 12 is a simple yes/no decision gate — not test-mode-eligible. See
`[[step-conditional-state-policy]]` for the full state definitions.
