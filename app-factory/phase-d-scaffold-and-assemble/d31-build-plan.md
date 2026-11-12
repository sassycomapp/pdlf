---
title: "d31-build-plan"
doc-id: "mb-ea170848"
updated: "2026-11-12"
---
# Step 31 — Scaffold Plan: Build Plan

## Step entry

### Phase D — Scaffold and Assemble

Ends with the gate `architecture-verified` (Step 34).

#### Step 31: Scaffold plan

**Must achieve:** the structure of the app being run planned in full before any code exists: every module and every function the code needs, at clean seams, each function with its access rule, the behaviour it will hold and the test that proves it, written into the project's `scaffold-spec.md`, so that Step 32 creates exactly that structure and the build loop only fills it.

**Starts from:** the reviewed plan with its architecture and data design, the glossary, the ADRs, the access matrix, the threat model and the test plan; the tickets; the approved screen requirements and the requirement index from Step 26; the authoritative schema; the project's `docs-standard-local\scaffold-spec.md`; for an existing app, its code.

**Produces:** `docs-standard-local\scaffold-spec.md`, written or extended; the scanner settings for Step 32; for an existing app, the module disposition list; in `pdlf-outputs\d31\`: the copies, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with Matt Pocock's `codebase-design`, Anvil's `data-models`, `server-code` and `client-modules`, and `graphify` for an existing app. David approves `scaffold-spec.md`.

**Must be built so that:**
- `scaffold-spec.md` is the one home of the app's structure: its packages, client and server modules, functions, navigation, startup and dependencies; no other structure document is written;
- `codebase-design` shapes the modules from the reviewed plan's architecture: deep modules at clean seams, with the business logic in pure modules apart from Anvil code, as [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) sections 2 and 3 set out;
- `data-models` decides, for each table, which behaviour goes on model classes, which in server methods and which in plain server functions;
- `server-code` and `client-modules` place every module where Anvil requires it and name it as [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) section 16 sets out;
- every server function a screen requirement names has its planned function, in the module its ticket's feature belongs to, with the same name;
- every planned function names: its module, its access rule from the access matrix (the decorator, or the reason it is public), its rate limit where it is public, the behaviour it will hold, and the test ID from the test plan that proves it;
- the modules of the common aspects (Vault, payments, webhooks, email, R2 storage and exit export, heartbeat, management endpoints) follow the one structure [[[default:adr-global/adr-common-architecture-across-mybizz-applications|Common Architecture Across Mybizz Applications]]](C:/dev/project-library-global/adr-global/adr-common-architecture-across-mybizz-applications.md) sets for every Mybizz application;
- every shared custom component is a module of its own, planned before the forms that use it;
- the section on tables points to the authoritative schema, and the section on components points to `spec-ui-standards` and `DESIGN.md`; neither is repeated in `scaffold-spec.md`;
- the scanner settings for the app's `tests\ts-config.yaml` are planned from the structure: the access decorators, rate-limit markers, public functions and endpoints, the single-role modules (Vault, constants, outbound), the pure modules and the core tables;
- for an existing app, `graphify` maps its code, and every existing module and server function is listed as keep (it fits the plan), rework (naming the ticket whose build reworks it) or remove (naming the ticket whose build removes it); nothing is changed in this step;
- for a feature run, `scaffold-spec.md` is extended for the feature, never rewritten;
- David approves `scaffold-spec.md` and, for an existing app, the disposition list;
- its ledger row is `step_type = 'skill'`, `skill_family = 'matt-skills'`, `synthesized = false`, `run` and `app_number` from the entry record, and `inputs_used` naming Step 26.

**BFT level:** Full.

**Gate:** none.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-artifact-handover|Spec: Artifact Handover]]](C:/pdlf/pdlf-library/specifications-local/spec-artifact-handover.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md), [[[default:test-suite/ts-method|Test Suite — Method]]](C:/dev/project-library-global/test-suite/ts-method.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `codebase-design` (Matt Pocock): the modules at clean seams → `scaffold-spec.md`, then Steps 32, 34 and 35.
- `data-models` (Anvil): where each table's behaviour lives → `scaffold-spec.md`, then Step 35.
- `server-code` and `client-modules` (Anvil): where each module lives and the rules it follows → `scaffold-spec.md`, then Step 32.
- `graphify`: for an existing app, its code mapped → the disposition list, then Steps 34 and 35.

**Layers with no skill:** security (each function's access rule comes from the access matrix; Step 34 verifies it against the threat model).

**Testing:** [[[pdlf:app-factory/phase-d-scaffold-and-assemble/d31-test-spec|Step 31 Test Specification]]](C:/pdlf/app-factory/phase-d-scaffold-and-assemble/d31-test-spec.md): every screen requirement's functions and every ticket trace to planned functions, each with its access rule and test; every existing module has its disposition.

**Standards:** [[[default:specifications-global/spec-anvil-platform-standards|Anvil Platform Standards]]](C:/dev/project-library-global/specifications-global/spec-anvil-platform-standards.md) sections 2, 3, 10 and 16; [[[default:adr-global/adr-common-architecture-across-mybizz-applications|Common Architecture Across Mybizz Applications]]](C:/dev/project-library-global/adr-global/adr-common-architecture-across-mybizz-applications.md); [[[default:policy-global/pol-common-aspects-for-mybizz-anvil-applications|Common Aspects]]](C:/dev/project-library-global/policy-global/pol-common-aspects-for-mybizz-anvil-applications.md).

## Why it is built this way

- **Structure before code.** Planning every module and function first, and checking it at Step 34, stops structure from being improvised one feature at a time.
- **One home.** `scaffold-spec.md` already exists in every project library for this purpose; writing the plan there keeps one document, not two that drift apart.
- **The screens name the functions.** The approved screen requirements already name every server function a form calls; planning exactly those functions means the forms and the server code meet without guessing.
- **Existing code is mapped, not judged.** Marking each existing module keep, rework or remove, against a named ticket, lets an existing app pass through PDLF without rebuilding everything at once, and without losing track of anything.
