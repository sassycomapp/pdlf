---

title: "pdlf-overview-v4"
updated: "2026-10-12"

doc-id: "mb-4afc2cc8"
---

# PDLF Overview, V4 (work in progress)

Temporary working document in `pdlf-library/wip/`. It sets out what PDLF's steps are planned to do, phase by phase, so that gaps and surplus can be judged. Delete when the findings are dealt with.

## The whole journey, as currently planned

An application goes through PDLF in six movements:

1. **Phase B (Steps 11 to 16): define what the application is.** Set it up, write down the idea, challenge its ambition and its engineering, then fix its vocabulary.
2. **Phase C (Steps 17 to 28): design it.** Build the data tables, break the plan into feature tickets, create the design system and wireframes, and freeze the concept and the visual direction.
3. **Phase D (Steps 29 to 34): build its skeleton in Anvil.** Forms, then empty code stubs, then a check that the skeleton matches the architecture.
4. **Phase E (Steps 35 to 40B): build it one feature at a time.** Each feature is built, tested, reviewed and signed off before the next begins.
5. **Phase F (Steps 41 to 46): release and learn.** Release, test the whole application, check it after release, and capture lessons.
6. **Seven gates along the way stop PDLF until David approves:** domain locked (16), concept locked (21), wireframes approved (26), architecture verified (34), build verified for each feature (39), released to production (44), and released (46).



## Phase A: the orchestrator and the entry points

Phase A (Steps 1 to 10, the orchestrator and the entry points) is not yet designed.

**Step 1, the orchestrator: the agent that carries an application through PDLF.**

- You start it with `/pdlf-init` in OpenCode. It offers the entry points, establishes which application (and, where it applies, which step) the work concerns, and runs the health check for an existing app.
- It then runs the selected steps in the order of the run plan, checks the ledger before every step, and never decides the order itself or skips a step.
- It owns the handoffs: it passes earlier outputs in full to each skill, records where each output was saved, confirms it exists, and copies it to the step's output folder. A missing output stops the step.
- After every step it explains what was done and why, shows the Step Receipt, waits for you, and asks you to run `/mb-close-out`. It never commits.
- The run plan it follows is already written. It covers which steps depend on which, what happens when a gate passes or fails, how optional and deferred steps are offered, how test mode works, and the feature loop.

**Steps 2 to 10, the entry points: where work joins the pipeline.**

- 02 new app with no context, and 03 new app with context: both enter Step 11.
- 04 add a feature and 05 update, to App 1; 09 and 10 the same for App 3 or App 5: these take the feature path (from Step 12) or the update path (to a step you name), after the health check.
- 06 compile the master template, 07 create the client template, and 08 create the management app: where these join is still to be settled.
- None of the entry points is designed yet.

## Phase B in detail: defining the application

**Step 11, Init: lays the foundation.**

- It asks whether the application is new or existing. It gets the code repository from Anvil, because the agent never creates it, and creates the documentation repository on GitHub only with David's permission.
- It registers both repositories in GBrain, creates the ledger record, puts the three blank pre-project files in place for a new app, and checks that the ledger and `project-library-global` are reachable.
- It ends with a self-audit that reports any error and fixes nothing without permission.
- For an existing application it creates only the folders that are missing and changes nothing that already exists.

**Step 12, Office hours: writes the design doc, meaning what problem the app solves, for whom, and how.**

- For a new app it questions David until the scope is clear. For an existing app it separates the lasting concept from what merely followed from it, and proposes that split for David to confirm.
- It always writes the doc in a fixed structure: problem, demand, current alternatives, target user, constraints, approaches, recommendation, open questions, success criteria.
- It keeps two copies. The first concept is frozen, so later drift can be detected. The second is a working copy.
- It then offers GStack's `/office-hours`, which challenges the premise and the alternatives.

**Step 14, CEO review: settles how big and ambitious the application is.**

- GStack's `/plan-ceo-review` receives everything from Step 12 in full, with a statement that a design doc already exists, so it doesn't reopen Step 12.
- David chooses the scope mode: expand, expand selectively, hold, or reduce.
- Each finding is put to David one at a time. The result is the CEO plan, which also names what must be tested and why.

**Step 15, Engineering review: locks the technical plan.**

- GStack's `/plan-eng-review` reviews architecture, code quality, tests and performance, one finding at a time.
- It stops for David if the plan is large (eight or more files, or two or more new services).
- It produces the test plan that Steps 35 and 38 use later.
- A second AI's opinion is shown for information only and is never adopted without David.

**Step 16, Domain modelling: fixes the vocabulary.**

- Matt Pocock's `/grill-with-docs` interviews David one decision at a time, and writes each settled term into `CONTEXT.md`.
- It writes a decision record only when a decision is hard to reverse, surprising, and the result of a real trade-off.
- Sentinel then checks for sensitive data, and the run must be proven in the ledger.
- The phase ends with the gate **domain locked**: no new terms without reopening it.

**What the Phase B review added for these steps:**

- use `grilling` in Step 12
- Anvil's `data-models` in Steps 15 and 16
- `secure-software-engineering` in Steps 14 and 15
- separate remits for 14 and 15, so David is never asked the same question twice
- possibly a gate after Step 14

## Phase C in detail: designing the application

**Step 17, Create Anvil data tables: turns the locked domain model into real tables.**

- You build the tables by hand in the Anvil editor. They follow the decision records and `CONTEXT.md` from Step 16 and the data design from Step 15, so every table and column traces back to a locked decision.
- The output lives in Anvil, not in a local file. The step checks that the tables exist and stops if they don't.
- Thinking check: Light, because the design was already decided in Phase B; this step follows the blueprint.
- Open point: its input still names a Step 15 "TDD cluster" of five documents, which Step 15 never produces.

**Step 18, Pull to local: brings Anvil's changes down to your computer.**

- The code repository is pulled from Anvil so that every later step works from the real schema, not from what the plan says it should be.
- It checks that the new tables are present locally and stops if they aren't. Thinking check: none, because it is purely mechanical.

**Step 19, To tickets: turns the plan into the feature list.**

- Matt Pocock's `to-tickets` breaks the locked plan (CEO plan, engineering review, domain model) into tickets in the order they depend on each other. Each ticket is one feature, such as authentication or a booking screen.
- For a wide mechanical change it instead produces an expand, migrate, contract sequence, so the app is never left half-changed.
- This is the only input to the build loop: Step 35 builds exactly these tickets, one at a time.
- The tickets go to the project's issue tracker. The skill finds the tracker through the setup written by `/setup-matt-pocock-skills`; if it can't, the step stops with a deviation instead of guessing.
- Open point: it still refers to a retired Step 3 "disposition table" for existing projects.

**Step 20, Design consultation: creates the design system.**

- GStack's `/design-consultation` researches the landscape and writes `DESIGN.md` (fonts, colours, spacing, motion), a preview page, and design tokens.
- It is built on Anvil's Material 3 theme and your design standards in `project-library-global`.
- In a test run you may run it in full, in a shortened form, or skip it. A shortened or skipped run is flagged, and every later step that relies on it shows a warning on its receipt.

**Step 21, Concept sanity audit: checks that everything agrees, then freezes the concept.**

- OpenCode reads every output so far (the CEO plan, the engineering review, the domain model and decision records, and `DESIGN.md`) and compares them pair by pair for contradictions.
- It writes an audit report with what was checked, what was found and its verdict.
- Gate **concept locked**: the scope is frozen; no new feature can be added without formally reopening the gate.
- Open point: its inputs still name a Step 13 specification, which no longer exists.

**Step 22, Wireframes, phase 1: explores the layout.**

- The Magdoub wireframe skill produces five black-and-white layout options for each screen, using `DESIGN.md` as context.
- On its first run it also builds a lasting design context from the codebase and screenshots, which later runs reuse.

**Step 23, Plan design review: rates the design.**

- GStack's `/plan-design-review` rates the plan's user-experience dimensions from 0 to 10 across seven passes and names the gaps, using the design system and the wireframes.
- Its report is appended to the plan.

**Step 24, Developer-experience review: checks how easy the app is to work with.**

- GStack's `/plan-devex-review` looks for friction in setup, interfaces and error messages, and appends a scorecard to the plan.
- Open point: whether this review earns its place for an Anvil application needs checking.

**Step 26, Wireframes, phase 2: polishes the chosen layout.**

- The Magdoub skill runs again on the chosen layout, skipping its context collection, and adds clean and polished colour versions.
- Gate **wireframes approved**: the visual direction is locked and Phase C ends.

**Step 27, Screen production (deferred): turns wireframes into finished screens.**

- OpenCode produces screen HTML from the approved wireframes and checks it against two checklists: faithfulness to the wireframe, and the project's screen standard.
- It runs only when you ask for it.

**Step 28, Screen to PNG (deferred): converts the screens into images.**

- An external tool renders each screen as a picture, so it can be handed to Anvil's AI in Step 29. It runs only when Step 27 has run.

## Phase D in detail: building the skeleton in Anvil

**Step 29, Build UI forms: builds the screens in Anvil.**

- You and Anvil's AI build the forms in the Anvil editor from the approved wireframes and screens. Anvil's AI also connects each component to its code-behind functions.
- Thinking check: Light, because the design was locked at Steps 21 and 26; you guide, you don't design.

**Step 30, Pull to local: brings the forms down to your computer.**

- So that later steps see the real forms and the wiring Anvil's AI created. It stops if the forms are missing locally.

**Step 31, Scaffold planning: plans the code's structure before any code is written.**

- OpenCode reads the architecture and domain model, the pulled forms and the concept audit, and decides which modules and functions are needed.
- It writes them down as empty stubs in `scaffold-plan.md`.

**Step 32, Physical scaffold build: creates the empty code structure in Anvil.**

- You create the empty client modules, server modules and functions in the Anvil editor, exactly as the scaffold plan lists them. Nothing is filled in yet.

**Step 33, Pull to local: brings the stubs down to your computer.**

- So that the build loop starts from the real structure.

**Step 34, Architectural sanity audit: checks that nothing has drifted before coding starts.**

- OpenCode compares what was actually built in Anvil against what was decided: every table and column against the decision records, the forms against the approved screens and `DESIGN.md`, and every stub against the scaffold plan, with nothing improvised.
- If something drifted, either the Anvil side is corrected or the plan is formally updated through a recorded deviation.
- Gate **architecture verified**: no code is written until it passes.

**Open point for Phase D:** Steps 18, 30 and 33 are the same "pull to local" job three times; one shared procedure could serve all three.

## Phase E in detail: building feature by feature

The loop runs once per ticket from Step 19, in this order: 35, 35A, 40, 40B, 36, 37, 38, 38A, 39. A feature is finished only when it passes its own gate at Step 39; then the next feature starts at Step 35. Each pass is recorded separately in the ledger (35.1, 35.2, and so on).

**Step 35, Build: builds one feature, tested at three levels.**

- Level 1: OpenCode writes the pure logic and its tests, and runs them on your computer until they pass.
- A backup is made. Level 2: it writes the server wrapper and integration tests, pushes to Anvil (without publishing), and runs the tests against the live development app. If they fail, it restores from the backup, fixes and retries; if they pass, a second backup is made.
- Level 3: the finished feature is checked by hand in the browser, and you sign it off.
- A signed-off feature is a known-good baseline: if something later breaks, the cause lies in work done after it.

**Step 35A, Testing: checks the local development tools.**

- `pip-audit` checks the development and test tools on your computer for known security problems, plus any extra test coverage.
- It deliberately doesn't check the app's own packages; Anvil does that itself, and Step 38A records it.

**Step 40, Architecture scan (optional, per feature): reports on code health.**

- OpenCode recommends running or skipping it for this feature, and you decide.
- If run, Matt Pocock's `improve-codebase-architecture` produces a read-only report; it changes no code.
- When the skill wants to question you about its findings, PDLF instead presents a deviation request with options (act on chosen findings, defer, or skip), so you choose.

**Step 40B, Approved fixes: applies only the fixes you approved.**

- OpenCode changes the code only for the findings you selected at Step 40. If you selected none, nothing happens.

**Step 36, Design review: a visual check of the feature as it will ship.**

- GStack's `/design-review` runs an 80-point visual audit on the live app, with before-and-after screenshots and one commit per fix.
- It runs after 40B on purpose, so it checks the code as it will actually ship, including any fixes.

**Step 37, Code review: finds bugs that tests miss.**

- GStack's `/review` checks the changes for bugs that would break in use, checks the work against its ticket and for scope drift, and fixes the obvious ones itself.
- Its findings must be written to a findings file, even when there are none, because GStack's skills can't be trusted to save on their own and Step 39 depends on it.

**Step 38, Quality testing: tests the feature against the whole app.**

- GStack's `/qa` tests the feature and checks that earlier features still work, fixes confirmed bugs, and writes regression tests into the code.
- It goes wider than Level 3 in Step 35, which only checks the single feature. Its findings file is mandatory too.

**Step 38A, Dependency check: records Anvil's own security scan.**

- Anvil scans the app's server packages itself whenever the server environment is rebuilt. This step makes sure that result is actually looked at and recorded, and raises a deviation if problems were found.

**Step 39, Triage: sorts the findings and decides whether the feature is done.**

- Matt Pocock's `triage` reads the findings of Steps 37 and 38, labels them, updates the issue tracker, and writes each finding into the ledger.
- Gate **build verified**: the gate passes only when every finding for this feature is resolved or deliberately set aside.
- If the gate passes, the next feature starts at Step 35; after the last feature, PDLF moves to Step 41. If it fails, work resumes at the step that failed, not at the start of the loop.
- Clarification questions go to you as a deviation request, never to a questioning skill.

## Phase F in detail: release and learning

**Step 41, Ship: prepares the release.**

- GStack's `/ship`, narrowed for Anvil: runs the tests, bumps the version, updates the changelog, commits and pushes. It stops at the push.

**Step 42, Publish to staging (to be rebuilt).**

- Written for a staging environment that PDLF doesn't have. Under the five-app structure, its job becomes part of the release by cloning App 1 into App 2.

**Step 42A, Whole-application test (to be rebuilt).**

- A full integration and end-to-end test of the whole application, added because a quick smoke test only proves the app is up, not that its features work together.
- This idea stays valuable for the new release: App 1 is tested as a whole before it is cloned into App 2.

**Step 43, Smoke test (to be rebuilt).**

- GStack's `/qa` or `/canary` run against the staging address. Its job moves to checking App 2 after the release.

**Step 44, Release.**

- Today it promotes the tested version from staging to production, with rollback by re-pointing to the previous version rather than reverting code.
- To be rebuilt as the release you perform: App 1's approved code is cloned into App 2 (`master_template`), which reaches every client at once.
- Gate **released to production**.

**Step 45, Production check: watches the released app.**

- GStack's `/canary` watches the live app for console errors, slow pages and load failures, against any earlier baseline.

**Step 46, Learning: closes the cycle.**

- Runs a retrospective (`/retro`), captures what was learned (`/learn`), saves working state (`/context-save`), and updates the project's ISA with its verification and changelog.
- Gate **released**, jointly with Step 45: the build cycle is closed.
- Open points: it still updates the retired project registry, and its lessons don't yet go through the memory governor and `mb-submit-memory` into the sources the next build reads.

## 

## Appendix: requirements against steps

Which steps mention each requirement of the system build plan. A mention is not always a design: several mentions are only recommendations copied in from the Phase B review.

| Requirement                                                                     | Steps that mention it                                           |
| ------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Orchestrator designed                                                           | a01 (empty)                                                     |
| Entry points 02 to 10                                                           | none (all empty)                                                |
| Health check for existing apps                                                  | none                                                            |
| App 1 built (development workspace)                                             | b11 to f46                                                      |
| App 2 release by cloning App 1                                                  | none (f44 still describes staging to production)                |
| App 3 blank client template                                                     | none                                                            |
| App 4 first client and provisioning procedure                                   | none                                                            |
| App 5 management app                                                            | none                                                            |
| No multi-tenancy given to every skill                                           | none                                                            |
| Anvil skills (anvil-agent-references)                                           | none                                                            |
| Anvil data-models skill                                                         | recommended for b15, b16, c17, d29, d32; not designed in        |
| Sentinel security review                                                        | designed in b16 only; recommended for b14, b15                  |
| secure-software-engineering skill                                               | recommended for b14, b15; not designed in                       |
| Material 3 design standard                                                      | b11, b12, b14, b15, b16, c20 (mostly as recommendations)        |
| Three-level testing per feature                                                 | e35 only                                                        |
| Gates                                                                           | b16, c21, c26, d34, e39, f44, f46                               |
| Step outputs to pdlf-outputs folders                                            | none (rule set today, steps not yet updated)                    |
| Learning into the right source; lessons through mb-submit-memory                | b11 to b16 (old wording); not in f46                            |
| Close-out by /mb-close-out, agent never commits                                 | b11 to b16 only                                                 |
| Old material still to remove (makePDLF paths, devlog, end-of-step housekeeping) | 46 steps carry makePDLF paths; 38 carry devlog and housekeeping |
