---
title: "c19-build-plan"
doc-id: "mb-de445841"
updated: "2026-11-12"
---
# Step 19 — Tickets: Build Plan

## Step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `screens-approved` (Step 26).

#### Step 19: Tickets

**Must achieve:** the locked plan broken into feature tickets in the order they can be built, each naming its forms, server functions, tables and tests, so that Step 22 knows every form to design and the build loop knows what to build next.

**Starts from:** the reviewed plan with its data design, the test plan, the glossary, the ADRs, the access matrix and the threat model, handed over at Step 16; the authoritative schema from Step 17; the business's user flows, `docs-local\user-flows.md`, when they exist; `docs\agents\issue-tracker.md` and `docs\agents\triage-labels.md`, configured at Step 11.

**Produces:** one ticket file per feature in `pdlf-tickets\{run}\`; the flow diagrams in `pdlf-outputs\c19\`; in `pdlf-outputs\c19\`: the test results and the Step Receipt; the ledger row, the BFT record and Sentinel's `triage_findings` row.

**Carried out by:** OpenCode, with Matt Pocock's `to-tickets`, Magnus919's `secure-software-engineering`, `mb-archify-scope` with `archify`, and `mb-sentinel-review`. David approves the ticket list and each flow's scope.

**Must be built so that:**
- `to-tickets` writes the tickets as local markdown files in `pdlf-tickets\{run}\`, in the format `docs\agents\issue-tracker.md` sets out;
- the tickets follow the order [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md) section 3 sets: `layouts` and `shared` first, `auth` second, then every other feature in the order its dependencies allow; every shared custom component is its own ticket, ahead of the tickets that use it;
- every ticket names: its feature; each form it needs, by module path (`<package path>.<FormName>`), with the package taken from the project library's `ui\README.md`; each server function it needs, by name; each table it reads or writes, by its name in the authoritative schema; its acceptance tests, by their IDs in the test plan; and its security acceptance criteria;
- `secure-software-engineering` writes each ticket's security acceptance criteria from Step 15's threat model;
- `mb-archify-scope`, then `archify`, draws the user flows of the application and the feature flow of each ticket that spans more than one form, into `pdlf-outputs\c19\`;
- every feature of the plan has a ticket, every ticket belongs to a feature of the plan, and the order has no cycle;
- for a feature run, only the feature's tickets are written, in `pdlf-tickets\{feature slug}\`, and the release carries its version;
- David approves the ticket list before the step ends;
- its ledger row is `step_type = 'skill'`, `skill_family = 'matt-skills'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Steps 16 and 17.

**BFT level:** Full.

**Gate:** none.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `to-tickets` (Matt Pocock): the tickets in dependency order → Steps 21, 22 and 35.
- `secure-software-engineering` (Magnus919): each ticket's security acceptance criteria → Steps 35 and 37.
- `mb-archify-scope`, then `archify`: the user flows and the multi-form feature flows → Steps 21, 22 and 35.
- `mb-sentinel-review`, Medium → `triage_findings`.

**Layers with no skill:** display (forms are designed at Steps 22 to 26).

**Testing:** [[[pdlf:app-factory/phase-c-design-and-plan/c19-test-spec|Step 19 Test Specification]]](C:/pdlf/app-factory/phase-c-design-and-plan/c19-test-spec.md): the tickets cover the plan, in a buildable order, each with its forms, functions, tables and tests.

**Standards:** [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md) section 3 (feature order); [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) section 4 (module paths).

## Why it is built this way

- **Forms named up front.** Step 22 writes one screen requirement per form; naming every form in its ticket, by module path, means no form is forgotten and none is designed twice.
- **Layouts and sign-in first.** Every page sits on a layout and the application starts on its sign-in form, so those are built before anything else.
- **Tests on every ticket.** Each ticket carries its acceptance and security tests, so the build loop knows when a feature is done.
