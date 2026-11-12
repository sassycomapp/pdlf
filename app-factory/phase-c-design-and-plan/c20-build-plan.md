---
title: "c20-build-plan"
doc-id: "mb-696b4ce8"
updated: "2026-11-12"
---
# Step 20 — Design System: Build Plan

## Step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `screens-approved` (Step 26).

#### Step 20: Design system

**Must achieve:** the application's design system, `DESIGN.md`, written within `m3-custom-theme`: the choices the theme leaves to each application made and recorded, so that every screen requirement and every form follows one design.

**Starts from:** the reviewed plan, the glossary and the ticket list from Step 19; the business's brand material in `assets-local\`; an existing `DESIGN.md`, when there is one; the theme's documentation: `m3-custom-theme-project-library\docs\usage-guide.md`, `docs\base-inventory.md` and `docs\components\`.

**Produces:** `docs-local\DESIGN.md`; in `pdlf-outputs\c20\`: its copy, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with GStack's `/design-consultation`. David approves `DESIGN.md`.

**Must be built so that:**
- `/design-consultation` makes only the choices `m3-custom-theme` leaves to the application: the starting palette, one of the theme's eight, and its mode; whether users may change palette and mode; the menu style; the brand's logo and imagery; the tone of the text; it never defines a colour value, font size or spacing of its own, because the theme's tokens hold them all;
- `DESIGN.md` restates no rule of [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md); it names that specification as the rules every form meets, and records only this application's choices;
- `DESIGN.md` states that every element of every screen uses the theme component that serves it best, chosen from the whole of the theme's component inventory, and names the components the application may not use: `Label`, `HtmlTemplate`, `HtmlPanel`, every Anvil Extras component, and every component outside the theme and `approved_components`;
- the chosen palette meets WCAG 2.2 AA contrast in light and dark mode;
- `DESIGN.md` is written to `docs-local\DESIGN.md` in the project library, never to a repository root;
- for an existing `DESIGN.md`, the step brings it to these rules and keeps every choice David made that still meets them;
- in a test run, David may abbreviate or skip the step, as `pol-step-conditional-state` sets out;
- David approves `DESIGN.md` before the step ends;
- its ledger row is `step_type = 'skill'`, `skill_family = 'gstack'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 19.

**BFT level:** Full.

**Gate:** none.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[pdlf:pdlf-library/policy-local/pol-step-conditional-state|Policy: Step Conditional State]]](C:/pdlf/pdlf-library/policy-local/pol-step-conditional-state.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `/design-consultation` (GStack), held to the choices the theme leaves open → `DESIGN.md`, then Steps 22, 23 and 26, and the `layouts` ticket.

**Layers with no skill:** security; `DESIGN.md` holds no data, access rule or secret, so Sentinel does not review this step.

**Testing:** [[[pdlf:app-factory/phase-c-design-and-plan/c20-test-spec|Step 20 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c20-test-spec.md): the design system is readable in light and dark mode and stays within the theme.

**Standards:** [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md); [[[default:adr-global/adr-dark-mode|Dark Mode]]](C:/dev/project-library-global/adr-global/adr-dark-mode.md); the documentation of `m3-custom-theme`.

## Why it is built this way

- **The theme holds the design.** Every colour, type size and spacing comes from the theme's tokens, so an application chooses among the theme's options and never invents its own values.
- **One home for each rule.** The rules every form meets live in `spec-ui-standards`; `DESIGN.md` holds only what is particular to this application, so the two never disagree.
- **The whole theme.** Stating in the design system that every screen draws on the full component set makes it the first of the checks that keep plain components out where a better one exists.
