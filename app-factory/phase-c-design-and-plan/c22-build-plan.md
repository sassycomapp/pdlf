---
title: "c22-build-plan"
doc-id: "mb-70132173"
updated: "2026-11-12"
---
# Step 22 — Screen Requirements: Build Plan

## Step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `screens-approved` (Step 26).

#### Step 22: Screen requirements

**Must achieve:** a screen requirement for every form the tickets name, written to [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) section 14.1, each element built from the theme component that serves it best out of the whole of `m3-custom-theme`, so that `mb-form-builder` can build every form without guessing.

**Starts from:** the tickets and flows from Step 19; `DESIGN.md` from Step 20; the concept locked at Step 21; the authoritative schema; the access matrix; the glossary; the theme's whole component documentation: `m3-custom-theme-project-library\docs\base-inventory.md`, `docs\components\` and `docs\usage-guide.md`; the model screen requirement `ui\(PACKAGE-NAME)\(FORM-NAME)\(FORM-NAME)-requirement.md`.

**Produces:** `ui\<package path>\<FormName>\<FormName>-requirement.md` for every form the tickets name, each with `status: draft`; each new form's entry in `access-matrix.yaml`; in `pdlf-outputs\c22\`: the requirement index, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode. David answers the questions the agent cannot settle from the documents.

**Must be built so that:**
- before writing any screen requirement, the agent reads the theme's whole component inventory and every component specification in `docs\components\`;
- every screen requirement is written from the model, with all nine sections of [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) section 14.1 filled;
- every element of a screen names the theme component chosen for it and why that component serves the element better than the other theme components that could serve it; a plain component is chosen only where no theme component serves the element better; an Anvil standard component is chosen only where the theme has none for the purpose and only if it is in `approved_components`;
- every element names only properties, events and values the theme's documentation gives;
- the data of every element names a table and column of the authoritative schema;
- every action names the event handler, `<component name>_<event>`, with the component prefix from `spec-nomenclature`, the server function it calls, by the name its ticket gives, and its result;
- every visible text and tooltip is a phrase key with its English text, in the tone `DESIGN.md` sets;
- every role of the access matrix has a scope for the form, and every form missing from `access-matrix.yaml` is added under `forms`, keyed by module path;
- every process on the form names its help video; every form names the user flows it takes part in;
- the screen type, width and pattern follow [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) section 7; every page form sits on a layout form of the `layouts` package;
- the forms of a ticket are written together, in the tickets' build order;
- for an existing application, every existing form the tickets name is given a screen requirement at its module path; an existing form no ticket names is listed on the receipt, because `mb-form-builder` removes it when its feature is built;
- every screen requirement is written with `status: draft`; only Step 26 sets it to `approved`;
- its ledger row is `step_type = 'skill'`, `skill_family = 'opencode'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Steps 19 to 21.

**BFT level:** Full.

**Gate:** none.

**References:** [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md), [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** No installed skill writes a screen requirement from a theme's documentation, so OpenCode writes them, from the model and the rules.

**Layers with no skill:** display (the requirement is the design; the form is built later by `mb-form-builder`); security (each form's access comes from the access matrix, checked by DC-05; data rules live in the server code, which Sentinel reviews at Step 35).

**Testing:** [[[pdlf:app-factory/phase-c-design-and-plan/c22-test-spec|Step 22 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c22-test-spec.md): every form has its complete screen requirement, built from the whole theme, and the access matrix lists every form.

**Standards:** [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) sections 3 to 14; [[[default:specifications-global/spec-nomenclature|Nomenclature]]](C:/dev/project-library-global/specifications-global/spec-nomenclature.md) section 1.6; [[[default:specifications-global/spec-translation|Translation]]](C:/dev/project-library-global/specifications-global/spec-translation.md); [[[default:specifications-global/spec-component-properties|Component Properties]]](C:/dev/project-library-global/specifications-global/spec-component-properties.md).

## Why it is built this way

- **The requirement is the design.** `mb-form-builder` builds each form exactly as its approved requirement says, so every decision about the form is made and approved here.
- **The whole theme, every time.** Reading the whole inventory before writing, and justifying each component against the others, is how every screen gets the best component the theme has rather than the first one that works.
- **Nothing guessed.** Components, properties, data and functions are named only from the documents that define them, so the builder never has to invent one.
