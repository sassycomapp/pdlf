---
title: "c20-build-plan"
doc-id: "mb-696b4ce8"
updated: "2026-10-21"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 20: Design consultation

**Must achieve:** Builds the application's design system (`DESIGN.md`) on Material 3 and David's design standards. In a test run, the developer may abbreviate or skip it.

**Carried out by:** GStack, using `/design-consultation`.

**Skills.** Every skill's output is used by the step named after the arrow.
- `/design-consultation` (GStack), held strictly to Material 3: it chooses only what the M3 standards leave open (brand colour, type pairing within the M3 scale) → `DESIGN.md`, then Steps 22, 26, 27 and 29.
- `client-forms` (Anvil), styling reference: the brand colour is recorded as the first entry for `theme/parameters.yaml` → Step 29.
- `mb-sentinel-review`, Medium/High → `triage_findings`.
- The step writes `wireframe/brain/design-context.md` in the project library from `DESIGN.md`, so the Magdoub wireframe skill starts from the application's own design → Step 22.

**Testing:** the palette meets the accessibility rules of the screen production standard (contrast, dark mode).

**Standards:** [[[default:specifications-global/spec-m3-design-standards|M3 Design Standards]]](C:/dev/project-library-global/specifications-global/spec-m3-design-standards.md), [[[default:specifications-global/spec-material-3-theme|Material 3 Theme]]](C:/dev/project-library-global/specifications-global/spec-material-3-theme.md), [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md), [[[default:specifications-global/spec-m3_component_mapping|M3 Component Mapping]]](C:/dev/project-library-global/specifications-global/spec-m3_component_mapping.md), and Anvil's own M3 documentation in `C:\mybizz\anvil-agent-references\docs\m3`.

**Must be built so that:**
- `DESIGN.md` names the components the application may not use: those outside the M3 dependency, Anvil Extras and `HTMLTemplate`;

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
