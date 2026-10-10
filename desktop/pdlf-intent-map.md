---
title: "pdlf-intent-map"
updated: "2026-10-10"
doc-id: "mb-8325f58e"
---
# PDLF Intent Map

Version: v08 (O1–O5 corrected; O7 nomenclature written)

## How to read this map

Every point gathered so far is one line. Nothing is dropped; a superseded line or phrase is struck through, not removed.

**Home** says where the point will finally live:
- **Intent**: the top-level statement of what PDLF is and why.
- **Explainer**: the document that says how PDLF works.
- **Rule**: a policy or specification that binds the agents.
- **Step**: settled in step design, later.
- **Open**: not yet decided.

**Status**: Decided (David agreed), Proposed (Claude proposed, not yet confirmed), Open.

Section K lists the questions raised by this review.

## A. Identity and purpose

| # | Point | Home | Status |
|---|---|---|---|
| A1 | PDLF (Project Development Lifecycle Framework) is an application development system that builds Anvil.works applications. | Intent | Decided |
| A2 | PDLF is a system, not a project. It has no code repository. It lives at `C:\pdlf` (GitHub `sassycomapp/pdlf`, private; GBrain source `pdlf`, federated, covering all of `C:\pdlf`). | Explainer | Decided |
| A3 | mybizz-os is the operating system PDLF runs on. The two are parts of one package. | Intent | Decided |
| A4 | Mybizz is the corporate entity. Each application PDLF builds is its own Mybizz business. Mybizz, mybizz-os and PDLF are never conflated. | Intent | Decided |
| A5 | makePDLF no longer exists; it is absorbed into PDLF. All PDLF work happens in `C:\pdlf`; there is no other workshop or copy. | Explainer, Rule (`AGENTS.md`) | Decided |
| A6 | Credo: simple, secure, robust, fit for purpose. | Intent | Decided |
| A7 | `project-library-global` is central to both PDLF and the projects it builds. ~~It is to move to `C:\mybizz\mybizz-os-docs`.~~ It stays where it is (`C:\dev\project-library-global`), as its own repository and GBrain source; the single GBrain search already joins it to PDLF and the projects. | Explainer | Decided (K1) |

## B. Who PDLF serves, and control

| # | Point | Home | Status |
|---|---|---|---|
| B1 | PDLF is for David, the developer, and his collaborators Claude and the OpenCode agent. | Intent | Decided |
| B2 | David is a project manager acting as developer, not a programmer. He looks at code but depends on Claude and the agents to make it correct. | Intent | Decided |
| B3 | PDLF carries the responsibility for correct code and explains every decision in plain language, so David stays in control without reading code. | Intent | Decided |
| B4 | The orchestrator never runs autonomously. It is David's tool for building the application. | Intent | Decided |
| B5 | Every change PDLF makes needs David's approval, until he says a particular approval is no longer needed. | Intent, Rule | Decided |
| B6 | More interaction is preferred to less. It can be reduced later, as confidence grows. | Intent | Decided |
| B7 | The gates are absolutely essential. | Intent, Rule | Decided |
| B8 | PDLF must never overstep or jump a gate. Cupcake enforces this in OpenCode, and PDLF runs in OpenCode, so it should hold in PDLF too; this must be proven, not assumed. Critical. | Intent, Rule | Decided; proof is to-do L1 |

## C. What PDLF builds, and where its job ends

| # | Point | Home | Status |
|---|---|---|---|
| C1 | PDLF builds many Anvil applications, each a separate business. | Intent | Decided |
| C2 | Every application follows the five-app structure (`spec-five-app-architecture-model.md` in `project-library-global`). Each business has its own dedicated set of five apps. | Intent, Rule | Decided |
| C3 | PDLF builds the entire five-app structure of a business in one continuous pipeline, so the apps stay consistent with each other. Today Step 46 ends with `master_template`; steps are to be added for the rest, after Step 46. | Intent, Step | Decided (K3) |
| C4 | App 4 (client instances): PDLF builds and verifies one client instance, the provisioning procedure and the README every instance must carry. That instance is the first real client, used as the test client. Provisioning each later client follows the procedure as business operations, outside the build pipeline. | Intent, Step | Decided |
| C5 | App 5 (management tooling) is built within the same pipeline as the rest of that business's apps. | Intent, Step | Decided |
| C6 | Release to `master_template` is the `develop` → `stable` merge, performed by David as a gated step. | Step | Decided |
| C7 | ~~The first application through PDLF is `mb-3-cs`.~~ A small test application goes through PDLF first, in `mb5pdlf`, to expose PDLF's own faults cheaply. Then `mb-3-cs` (Mybizz CS, consulting and services), then others such as `mb4ecom` (e-commerce). Which test application is still to be chosen. | Explainer | Decided (M1) |
| C8 | A new application with no prior context starts from the three pre-project files (brief, scoping ideas, constraints and notes). An existing application brings its own context. How each enters is settled at Step 11. | Step | Open |
| C9 | How a released application re-enters PDLF for fixes, features or upgrades. Steps 2 to 10 were deliberately left open for entry points such as this (see D1). | Step | Open |

## D. How PDLF runs

| # | Point | Home | Status |
|---|---|---|---|
| D1 | David chooses an application and starts the orchestrator in OpenCode. PDLF works through the OpenCode Build agent and its model. The entry point depends on the work: a new project starts at Step 11; a feature on an existing application may start at Step 2; an update or upgrade at Step 3; reworking any of the other apps of the five-app structure somewhere in Steps 4 to 9. First builds of the other apps happen in the pipeline after Step 46; Steps 4 to 9 are for returning to apps that already exist. The other four apps may later need their own maintenance entry points (features, updates, upgrades): a thought, not a decision. | Explainer, Step | Decided in intent; entry points to be designed |
| D2 | The orchestrator (currently Step 1) asks David questions to establish the entry point (D1), then runs the modules selected for that entry, in order. | Explainer | Decided |
| D3 | A module is one finished step, packaged as a single unit. `app-factory/` holds 46 placeholders (`module-01` to `module-46`), kept until their step is built. | Explainer | Decided |
| D4 | Steps are designed in `stepwise/`. `run-plan.md` decides order; `step-mapping.md` says what each step is; `workflow.md` describes the steps. `stepwise/` is read-only until step design resumes. | Explainer, Rule | Decided |
| D5 | ~~Step renumbering (orchestrator unnumbered, pipeline steps 1, 2, 3 … with no gaps): done once, at the end of scoping.~~ Rejected: the current numbering is kept, because Steps 2 to 10 are entry points (D1). | Step | Decided |
| D6 | Two repositories per application: code and documentation. Only part of the code repository returns to Anvil (`anvil.yaml`, `client_code`, `server_code`, `theme`; to be confirmed against Anvil); the rest is kept out. Re-entry reads both repositories directly; no third repository. | Explainer, Rule | Decided (Anvil list to confirm) |
| D7 | No `CLAUDE.md` in PDLF; `AGENTS.md` is the single instruction file. A PDLF `opencode.json` is written when the orchestrator is designed. | Explainer | Decided |

## E. Knowledge and standards

| # | Point | Home | Status |
|---|---|---|---|
| E1 | `project-library-global` is the central repository of all knowledge PDLF draws on, Anvil knowledge included. It is permanent, project-agnostic, and the standard every application is built to. Its location is to change (A7). | Intent | Decided |
| E2 | One home per kind of knowledge: `pdlf-library` holds how PDLF works; `project-library-global` holds what a good application is; a project's own `project-library/docs-local` holds what is true of that project only. A fact lives in one of them, never two. | Intent, Explainer | Decided |
| E3 | Anvil standards, specifications, principles and methodologies are applied throughout every application, using the Anvil skill set `C:\mybizz\anvil-agent-references\skills`. This is a core success criterion. | Intent | Decided |
| E7 | Two sources of Anvil knowledge: the `anvil-agent-references` skills, issued directly by Anvil; and `anvil-docs` in `project-library-global`, downloaded from the Anvil documentation together with the Anvil runtime documentation. The download could not include images, so `anvil-docs` lacks them. | Explainer | Decided (K4) |
| E8 | Where Anvil sources conflict, the conflict is raised to David, who resolves it. Neither source silently wins. | Rule | Decided (K4) |
| E4 | Standards and instructions form one integrated, consistent, rational whole. There is no contest over which wins: a conflict is a defect, fixed at its source. | Intent, Rule | Decided |
| E5 | PDLF may propose changes to `project-library-global` when a lesson concerns Anvil, with David's approval. Lessons canonical to one project go to that project's `project-library/docs-local`, never to `project-library-global`. | Intent, Rule | Decided |
| E9 | Nomenclature (David, 2026-10-10): one single document, `project-library-global/specifications-global/spec-nomenclature.md`. Part 1 holds what is common; Part 2 holds what is unique to PDLF; one further part per application holds what is unique to it. A term is defined once. This is the one deliberate exception to E2: PDLF's names live in the global document. PDLF's two nomenclature files retire to `obsolete/`. | Rule | Decided |
| E6 | One search covers everything: every documentation repository is a federated GBrain source. | Explainer | Decided (mybizz-os) |

## F. Learning and self-healing

| # | Point | Home | Status |
|---|---|---|---|
| F1 | No lesson is learned twice and no mistake is repeated. PDLF grows smarter, finer-tuned and more precise over time. | Intent | Decided |
| F2 | Learning: each lesson is written once, into the source that will be read next time. Anvil lessons go to `project-library-global`; lessons about PDLF go to the relevant module or rule; lessons about one application go to that project's `project-library/docs-local`. | Intent, Rule | Decided |
| F3 | Self-healing: when a step fails or David corrects something, PDLF proposes the fix to that source, David approves it, and the fact is recorded in GBrain through `mb-submit-memory`. | Intent, Rule | Decided |
| F4 | The mechanisms use what exists (GBrain, the ledger, governed memory, close-out). Established AI-engineering techniques are welcome where they fit. This is a design principle for every step. | Explainer, Step | Decided in principle; how per step |

## G. Records and ceremony

| # | Point | Home | Status |
|---|---|---|---|
| G1 | Ceremony is any process that does not serve the objective, such as reports and logs nobody reads. It is not wanted. | Intent | Decided |
| G2 | Stops and checks are control, not ceremony. They stay. | Intent | Decided |
| G3 | Close-out is the mybizz-os skill `/mb-close-out`, run on David's request. `commit-all` is run by David; agents never commit or push. The two housekeeping questions at the end of every step are removed and replaced by `/mb-close-out`. | Explainer, Rule, Step | Decided |
| G4 | The workshop's devlog index and judgement trail are retired. Whether a project built by PDLF needs a judgement trail of its own is undecided. | Open | Open |

## H. Success criteria

| # | Point | Home | Status |
|---|---|---|---|
| H1 | PDLF is perpetually learning and self-healing, so the lifecycle is stable and dependable. | Intent | Decided |
| H2 | Anvil standards are applied throughout every application built. | Intent | Decided |
| H3 | PDLF consists only of the skills that best serve its objectives: nothing superfluous, nothing lacking. | Intent | Decided |
| H4 | Policy change: skill usage takes precedence over the OpenCode agent doing the work itself. When a skill in the library covers a task, the agent must use it, not improvise. Together with H3, a skill joins the library only if it earns its place. This replaces the current skill-use principle (a skill only when it does better than the agent). | Rule | Decided (K5) |

## I. Discovery still to do

Work order (David, 2026-10-10): resolve the PDLF system first, then move to the steps. Anything that can be settled by question and answer is asked now.

| # | Area | When |
|---|---|---|
| I1 | The gates: which gates, where, and why. | Deferred to steps work |
| I2 | The ledger and the records each project keeps (receipts, ISA, deviations), tested against the ceremony rule. | Now (M4) |
| I3 | BFT thinking checkpoints: their place and weight. | Deferred to steps work |
| I4 | The skill library: which skills, from which sources, and why. | Now |
| I5 | GBrain's role during a build. | Now |
| I6 | Cupcake and governance during a build. | Now |
| I7 | Testing and quality. | Now |
| I8 | Design and wireframes. | Now |
| I9 | The orchestrator: role and form. | Now |
| I10 | The deviation mechanism. | Now |
| I11 | Artifacts and the `output/` folder. | Now |
| I12 | The test project `mb5pdlf`: its role in proving PDLF. | Now (M1) |
| I13 | The entry points in Steps 2 to 10 (D1, C9). | Deferred to steps work |
| I14 | `run-plan.md` says every step always runs for every project; D1 and D2 make the entry point select which modules run (moved from J10). | Deferred to steps work |
| I16 | The table of which `project-library-global` standard each step applies (formerly in PDLF's nomenclature file) belongs in the step design. | Deferred to steps work |
| I15 | `pol-stepwise-gating.md` is empty; `pol-stepwise.md` is a working document about developing steps, not a policy (moved from J4). | Now (M5) |

## N. Final system answers (2026-10-10)

| # | Point | Home | Status |
|---|---|---|---|
| N1 | Skill library (I4): the skills catalog in `mybizz-os-docs` is the single register of PDLF's skills; which skill each step uses is decided in steps work. | Explainer | Decided |
| N2 | GBrain (I5): every step starts with a GBrain search; the actual file a search points to is read before it is applied; new knowledge enters only through close-out and `mb-submit-memory`. All knowledge has been submitted to GBrain and is available there. | Explainer, Rule | Decided |
| N3 | Governance (I6): PDLF runs under the same global `AGENTS.md` and Cupcake rules as all OpenCode work, with no separate rule system. Its access to each project's folders is set when the orchestrator is designed. | Explainer, Rule | Decided |
| N4 | Testing (I7): every feature is tested at three levels before David signs it off: logic alone, connected to the live Anvil app, then by hand in the browser. Review and QA findings are always written to a file. `anvil_cop_testing.md` (in `desktop/`) is a major input to the testing protocol. | Intent, Rule | Decided; COP review at writing (O6) |
| N5 | Design (I8): Material 3 on David's standards in `project-library-global`; structural wireframes, then polished wireframes, then screens; David approves each stage. | Intent, Step | Decided |
| N6 | Orchestrator (I9): the orchestrator is a step; its form is settled in steps work. | Step | Deferred to steps work |
| N7 | Deviations (I10): when a step cannot be done as written, the agent stops, sets out the options and what each costs, and David decides; the decision is recorded in the ledger. | Rule | Decided |
| N8 | Artifacts (I11): every artifact is written to its canonical destination, and a copy is also written to `output/`, for David's convenience. ~~Retire `output/`.~~ `AGENTS.md` rule 4 stands. | Explainer, Rule | Decided |
| N9 | Judgement trail for projects (G4): not needed; the ledger records every deviation and gate, and every step explains itself in plain language. | Rule | Decided |
| N10 | Test application (C7): the Daily Intentions Tracker is the first test build in `mb5pdlf`. It may be too small to test PDLF fully; it can be extended as required. | Explainer | Decided |

## O. Writing stage (what will be written, in order)

| # | Document | What changes |
|---|---|---|
| O1 | `pdlf-library/pdlf-explainer-docs/pdlf-intent.md` (new) | The statement of intent: sections A to H and N, each line pointing to where its detail lives. |
| O2 | `pdlf-explainer.md` | Rewritten as the explainer of how PDLF works, consistent with this map; history, market comparison and contradictions removed (J1). |
| O3 | `app-factory-explainer.md` | Rewritten to D2 and D3 (J2). |
| O4 | `orchestrator-agent-explainer.md` | makePDLF references removed; otherwise kept until steps work. |
| O5 | Policies in `policy-local/` | `pol-skill-invocation` to H4 (J11); `pol-memory-and-knowledge` to G3, F2, N2, N9; `pol-sequential-enforcement-and-deviation` and `pol-anvil-platform` to G3 and C6 (J3); `pol-INDEX` updated. |
| O6 | Testing standard (moved to to-do L4 by David, 2026-10-10) | `anvil_cop_testing.md` reviewed and merged with `spec-testing-methodology-standards.md` in `project-library-global` (application knowledge, E2); `pol-testing-and-quality` points to it. |
| O7 | Nomenclature | `spec-nomenclature.md` and `spec-nomenclature-b.md` consolidated with the `project-library-global` specification (J5). |
| O8 | `pdlf-library/README.md` | Consolidated with `app-factory/README.md` (J9). |

## J. Known conflicts in the existing documents (writing stage only)

| # | Conflict | Resolution at writing |
|---|---|---|
| J1 | `pdlf-explainer.md` says the agent asks to commit and sync after every step, says gates commit and push automatically, and also says close-out is `/mb-close-out`. | `/mb-close-out` replaces the earlier rule (G3). |
| J2 | `app-factory-explainer.md` rests on the retired build-then-migrate plan. | Rewrite to D2 and D3. |
| J3 | Several policies still require the devlog index, judgement trail, per-step syncing and a staging release. | Remove: G3 replaces per-step syncing; G4 retires the workshop logs; C6 replaces the staging release with the `develop` → `stable` merge. |
| J5 | Two nomenclature specifications (`spec-nomenclature.md`, `spec-nomenclature-b.md`); a nomenclature specification also exists in `project-library-global`. | Consolidate with `project-library-global`. |
| J6 | `pdlf-objective-review.md` is an outside assessment, not intent. | Retire or keep: M2. |
| J7 | `artifact-lifecycle explainer.md` contains history and has a space in its name. | Retire or keep: M3. |
| J8 | The `pdlf-library/agents/` files describe the old makePDLF workspace. | Adjust or retire: M6. |
| J9 | `app-factory/README.md` and `pdlf-library/README.md` probably describe the old plan (deferred). | Consolidate into `pdlf-library/README.md`. |
| J11 | `pol-skill-invocation.md` states the skill-use principle that H4 replaces. | Rewrite to H4. |

J4 and J10 moved to section I (I15, I14).

M decisions (2026-10-10), actioned in one terminal command: M1 test application first (C7). M2 `pdlf-objective-review.md` to `obsolete/`. M3 `artifact-lifecycle explainer.md` to `obsolete/` (renamed `artifact-lifecycle-explainer.md`); `spec-artifact-handover.md` holds the binding rules, and the explainer stays available in `obsolete/` for comparison at writing. M4 the ledger stays, as control. M5 `pol-stepwise-gating.md` to `obsolete/`; `pol-stepwise.md` is not a policy, so it becomes `pdlf-library/docs-local/stepwise-development-process.md`. M6 `pdlf-library/agents/` to `obsolete/`: Step 11 already runs `setup-matt-pocock-skills` for every application, which writes that application's own configuration, so `mb5pdlf` receives its own when it is set up, and `mb-3-cs` its own after that; nothing needs moving by hand.

## M. Questions for David now

| # | Question | Claude's recommendation |
|---|---|---|
| M1 | Does a small test application go through PDLF in `mb5pdlf` before `mb-3-cs`, or is `mb-3-cs` the first build (C7)? | Test first. A small application exposes PDLF's own faults cheaply, before they can damage `mb-3-cs`, a real business. |
| M2 | Retire `pdlf-objective-review.md`? | Yes. It assesses PDLF from outside; it is neither intent nor how PDLF works. |
| M3 | Retire `artifact-lifecycle explainer.md`? | Yes, once anything in it that is still true is confirmed to be in `spec-artifact-handover.md`, which holds the binding rules. |
| M4 | Should PDLF keep its own database record (the ledger) of each project's progress: steps done, gates passed, deviations decided? | Yes. It is what lets the orchestrator refuse to pass a gate that was never approved, and lets a build resume or re-enter where it left off. It is control, not ceremony. |
| M5 | Retire the empty `pol-stepwise-gating.md`, and treat `pol-stepwise.md` as steps-work material rather than a PDLF policy? | Yes to both. |
| M6 | The `pdlf-library/agents/` files configure Matt Pocock's skills for the repository they sit in. Retire them from PDLF, so each application receives its own configuration when it is set up? | Yes. `instructions.md` is replaced by `AGENTS.md`; the other three belong to each application, not to PDLF. |

## K. Questions raised by the v01 review (all resolved in v03)

| # | Question | Claude's recommendation |
|---|---|---|
| K1 | Moving `project-library-global`: placed inside the `mybizz-os-docs` repository (merged into it), or moved beside it under `C:\mybizz` as its own repository? | Beside it, as its own repository and GBrain source. Merging would change the source of hundreds of existing links and mix two kinds of knowledge in one repository; a move keeps everything intact and needs only a path rewrite, which the earlier migration already proved. |
| K2 | How is it proven that Cupcake stops gate-jumping in PDLF? | A deliberate test run once the orchestrator exists: an agent attempts to pass a gate without approval, and Cupcake must block it. |
| K3 | C3 builds the other apps after Step 46; D1 places rework of the other apps in Steps 4 to 9. Are first builds after Step 46 and later rework through Steps 4 to 9? | Yes: first builds belong in the continuous pipeline after Step 46; Steps 4 to 9 are for returning to an app that already exists. |
| K4 | The Anvil skill set (`anvil-agent-references`) and `project-library-global` both hold Anvil knowledge. How do they relate? | The vendor skills are how agents apply Anvil correctly; `project-library-global` holds your own standards and decisions. Where they overlap, one must be named the source and the other point to it (decided under I4). |
| K5 | H4: does "skills take precedence" mean the agent must use a skill whenever a selected skill covers the task, rather than improvising? | Yes, with that exact wording. Combined with H3, a skill is in the library only if it earns its place, and once there it is always used for its task. |

Resolutions: K1 `project-library-global` stays where it is (A7). K2 proof added to the to-do list (L1). K3 agreed, with a possible later maintenance entry for the other four apps (D1). K4 two Anvil sources recorded, conflicts go to David (E7, E8). K5 agreed as worded (H4).

## L. Claude's to-do list

| # | Action | Priority |
|---|---|---|
| L1 | Prove that Cupcake stops gate-jumping when PDLF runs: once the orchestrator exists, an agent deliberately attempts to pass a gate without approval, and Cupcake must block it. | Critical |
| L2 | Confirm against the Anvil documentation exactly which parts of a code repository return to Anvil (D6). | Normal |
| L3 | Note the missing images in `anvil-docs` when Anvil standards are reviewed (E7). | Normal |
| L4 | Testing is a component of its own, to be designed (David, 2026-10-10): the testing disciplines are reviewed and investigated first, then the standard is written for `project-library-global`. Inputs: `anvil_cop_testing.md` (its philosophy only; its multi-tenant pattern, Factory Droid and dev-log references are excluded) and further information from David. `pol-testing-and-quality` is updated then. | Normal |
| L5 | ~~Nomenclature (O7): needs the contents of `pdlf-library/specifications-local/spec-nomenclature.md` and `spec-nomenclature-b.md`. Also: the `project-library-global` nomenclature specification is titled "Mybizz CS" and holds `mb-3-cs`-specific content in a project-agnostic library, which breaks E2.~~ Resolved: see E9. | Done |

## P. Writing status (2026-10-10)

| # | Document | Status |
|---|---|---|
| O1 | `pdlf-intent.md` (new) | Drafted; checked against sections A–H and N; design stages (N5), quality (N4) and governance (N3) added |
| O2 | `pdlf-explainer.md` | Rewritten |
| O3 | `app-factory-explainer.md` | Rewritten |
| O4 | `orchestrator-agent-explainer.md` | Rewritten |
| O5 | `pol-skill-invocation`, `pol-memory-and-knowledge`, `pol-sequential-enforcement-and-deviation`, `pol-anvil-platform`, `pol-INDEX` | Rewritten |
| O6 | Testing | Deferred (L4) |
| O7 | Nomenclature | Written (E9). Removed as obsolete: the `pdlf-` filename prefix rule (doc-id is now a code), the per-environment makePDLF folders, the GBrain "PGlite" note, the LifeOS acronym, the old link reference patterns. Corrected: "pull-based updates" now matches the five-app model (automatic via `stable`). The table of standards per step moves to steps work (I16). |
| O8 | READMEs | Written last, once everything else is done (David, 2026-10-10) |
| A4 add | No multi-tenancy, ever: written into intent §4, explainer §10, `pol-anvil-platform`. | Done |
