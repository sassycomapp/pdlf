---
title: "pdlf-full-scope-v1-b2"
updated: "2026-10-13"
doc-id: "mb-25edae39"
---

# PDLF Full Scope, V1 (work in progress)

Temporary working document in `pdlf-library/wip/`. It sets out what PDLF's steps are planned to do, phase by phase, so that gaps and surplus can be judged. Delete when the findings are dealt with.

Full Scope V1 builds out Phase B in full. Every other part is unchanged from overview V4.

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
- 06 compile the master template: a step near the end of the pipeline, not Phase B.
- 07 create the client template (App 3) and 08 create the management app (App 5): Step 11, like 02 and 03. For App 3, Steps 12 to 16 do not run.
- None of the entry points is designed yet.

## Phase B in full: defining the application

Phase B is Steps 11, 12, 14, 15 and 16. Step 13 is not used. Phase B turns an idea, or an existing application, into a defined application: its repositories and records exist, its concept is written down, its scope and its engineering are challenged and settled, and its vocabulary is fixed. Phase B ends at the gate `domain-locked`. Nothing in Phase C is built until David passes that gate.

### How to read this section

This section is the full technical scope of Phase B. It was built from every file of every Phase B step, the run plan, the system build plan, the PDLF specifications and policies, the skills catalogue, the source of every skill Phase B uses, and the `project-library-global` standards that Phase B applies. The list of files read is at the end of this document.

Every point carries one of four labels, so that what already exists is never confused with what is proposed:

- **Designed** means the existing step files already say this. It is carried forward, sometimes in clearer words.
- **Finding** means something in the existing design is out of date, contradicts another document, or contradicts the skill it relies on. A finding states the evidence.
- **Proposal** means a new design, written to make the step excellent. A proposal is not yet agreed. David decides.
- **Open for David** means a decision about intent that only David can make. Each one is collected again, with a recommendation, in the list at the end of this section.

Phase A (the orchestrator and the entry points) is not yet designed. This section states only what Phase B needs to receive from Phase A, so that Phase A can be designed to deliver it.

### B.1 What Phase B receives from Phase A [DONE]

[DONE] **Settled.** `/pdlf-init` starts the orchestrator (Step 1). The orchestrator offers the entry points and David chooses exactly one. Each one joins the pipeline as follows:

| Entry point                     | App        | Where it joins Phase B                                                                                                          |
| ------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------- |
| 02 `new-app-no-context`         | App 1      | Step 11, at the project slug question.                                                                                          |
| 03 `new-app-with-context`       | App 1      | Step 11, at the repository questions.                                                                                           |
| 04 `add-feature-main-app`       | App 1      | Health check, then the feature path from Step 12.                                                                               |
| 05 `update-main-app`            | App 1      | Health check. A change to what the app does takes the feature path from Step 12; any other update goes to the step David names. |
| 06 `compile-master-template`    | App 2      | Not Phase B (a step near the end of the pipeline).                                                                              |
| 07 `create-client-template`     | App 3      | Step 11, at the project slug question or the repository questions, depending on whether there is existing context or not. Steps 12 to 16 do not run for App 3. |
| 08 `create-management-app`      | App 5      | Step 11, at the project slug question or the repository questions, depending on whether there is existing context or not.       |
| 09 `add-feature-management-app` | App 3 or 5 | Health check, then the feature path from Step 12.                                                                               |
| 10 `update-management-app`      | App 3 or 5 | Health check. A change to what the app does takes the feature path from Step 12; any other update goes to the step David names. |

Why Steps 12 to 16 do not run for App 3: App 3 holds only App 1's data table schema, one startup module and the link to App 2 (`spec-five-app-architecture-model.md`). There is nothing in it to design.

[DONE] **Settled: the entry record.** Every Phase B step behaves differently depending on how the work entered PDLF. So before Step 11 or Step 12 runs, the orchestrator establishes these facts, which this document calls the entry record:

1. the entry point chosen (02 to 10);
2. the business slug, and which app is worked on (1, 3 or 5);
3. the path: a whole application, a feature, or an update;
4. for a feature or an update, a short statement of it in David's words, and a short name for it (the feature slug). The orchestrator must ask David for both;
5. the project's mode, `full` or `test` (`mb-5-pdlf` is `test`).

Where the entry record is written:

- Entries 04 to 10: the business row already exists, so the orchestrator writes the entry record at once to the ledger row of the step where the entry joins.
- Entries 02 and 03: no business row exists yet, so the orchestrator passes the entry record to Step 11, which writes the business row first and then the entry record.
- The mode is always kept in the business row, because it belongs to the business, not to one entry.

Every Phase B step reads the entry record from the ledger and never asks David again for what it already says. Why: each step asks David only what is new, and the answers cannot drift between steps.

[DONE] **Settled: the health check is one standard procedure.** The entry points that work on an existing app (04 to 10) check the app's setup first, and Step 11 ends with a self-audit that checks the same things. Both use one standard procedure, `sop-health-check.md`, saved in `C:\pdlf\pdlf-library\operating-procedures\`. Step 11 runs it as its self-audit; entries 04 to 10 run it as their health check. Why: one procedure cannot drift into two different ideas of what "a sound setup" means.

The health check verifies, for the business and the app being worked on:

1. The ledger is reachable on port 5433 and holds its seven tables.
2. The business row in the ledger matches what is on disk.
3. Each app folder (`{slug}-app1`, `{slug}-app2`, `{slug}-app3`, `{slug}-app5`) is a Git repository linked to the right GitHub repository, and holds `anvil.yaml`.
4. Each app folder is up to date with GitHub, so nothing is waiting to be pulled from the Anvil editor.
5. Each app folder's `.gitignore` keeps out `.env`, credentials and test output.
6. The project library (`{slug}-project-library`) is linked to GitHub and has its standard folders and its `pdlf-outputs` step folders.
7. The project library is registered in GBrain as the source `{slug}-project-library`, and is covered by the commit hook and by `commit-all`.
8. The Matt Pocock configuration points to `CONTEXT.md` and `adr-local`.

Any failure is reported to David. Nothing is fixed without his permission, and work does not start until every check passes.

[DONE] **Applied (2026-10-13).** Build plan section 4 (entry table, entry record, health check) and section 9; `a01-build-plan.md`; `a02-build-plan.md` to `a10-build-plan.md`, one entry each; `pdlf-library/operating-procedures/sop-health-check.md` (new); the library README.

### B.2 Rules that apply to every Phase B step [DONE]

These rules apply to all five steps. They are stated once here, as the build plan requires (section 10, rule 4.4), and not repeated in each step.

[DONE] **Settled: where the rules live.** Each rule is saved as its own file in `pdlf-library/policy-local/` (a `pol-` file, listed in `pol-INDEX.md`) and is referenced from each phase and step where it applies. Where a specification in `pdlf-library/specifications-local/` already states a rule in full, `pol-INDEX.md` points to that specification instead of copying it, so the rule exists in one place only. `adr-local` never holds rules: it records a decision and why it was made, and the rule that follows from it points to that record.

#### B.2.1 The step pattern [DONE]

[DONE] **Settled.** Every step follows the execution sequence in `spec-execution-discipline.md`: search GBrain and read the real files the search points to, do the work with the step's skill, verify that the output exists, answer the thinking checkpoint (BFT), write the ledger row and produce the Step Receipt from it, explain in plain language what was done and why, stop, and ask David to run `/mb-close-out`. Gate steps add the ceremony in `spec-gate-procedure.md`: Full BFT, the gate summary, David's explicit yes or no, and the gate row, then the same request for `/mb-close-out`.

[DONE] **Done (2026-10-13): both specifications corrected to the build plan.** The agent never commits or pushes; the dream cycle is not part of any step; memory is written only at close-out, through `/mb-close-out`. `spec-execution-discipline.md` no longer asks the two housekeeping questions, sends step outputs to `pdlf-outputs\{step}\`, and drops the devlog and judgement trail. `spec-gate-procedure.md` no longer commits, pushes or syncs GBrain at a gate, and its gate summary no longer reports a push. `pol-INDEX.md` lists the step pattern and points to these two specifications.

[DONE] **Done (2026-10-13): the five Phase B reference files cleaned.** Each now ends with "explain, stop, ask David to run `/mb-close-out`" and nothing else; the two housekeeping questions, the five-action memory sequence and the devlog and judgement-trail entries are gone.

[DONE] **Done (2026-10-13): every other place the old ending lived.** The five Phase B build plans and five decision trees, the Step Receipt template, the PDLF self-test checklist, `spec-skill-design.md` and the PDLF to-do list (items B2 and B3, now finished, removed). The retired devlog and judgement-trail templates are deleted.

[DONE] **Recorded.** The decision is recorded in `adr-local/step-housekeeping-retired.md`. The rule is stated in the two specifications and listed in `pol-INDEX.md`; how memory is written stays in `pol-memory-and-knowledge.md`.

#### B.2.2 Searching GBrain with the real source names [DONE]

[DONE] **Settled.** Every step starts with one GBrain search of the federated documentation sources. One search covers the project library `{slug}-project-library`, `default` (which is `project-library-global`) and `pdlf`. A step that needs Anvil knowledge (Steps 15 and 16) also names `anvil-agent-references-code`. Application code is never a GBrain source; the agent reads it directly from the app folder. The step reads the real file behind every result before applying it, and a step that applies a `project-library-global` standard names the file it read in its receipt or BFT answer.

Why: the old instruction named sources (`{slug}`, `project-library-global`) that do not exist under those names in GBrain (`repo-organization.md`), so the searches found nothing there.

[DONE] **Done (2026-10-13).** Corrected in the build plan (section 8), `spec-execution-discipline.md` (point 1), `pol-memory-and-knowledge.md` (searching) and the ADR `global-content-discovery-and-application-discipline.md`.

#### B.2.3 Handing work from one step to the next [DONE]

[DONE] **Designed.** The handoff contract in `spec-artifact-handover.md`: the orchestrator pastes the full text of every earlier output into the skill's invocation, because skills do not read PDLF's folders; where a skill checks for a file on its own, the invocation states plainly that the file already exists and is provided, so the skill does not reopen a decision already made; the orchestrator captures the path the skill reports, never an assumed path; it never moves or edits a skill's own file; and an expected output that is missing stops the step with a deviation.

[DONE] **Finding: the output paths in the Phase B files are all out of date.** The reference files save copies to `output-gstack\makepdlf-step-14-ceo-plan.md` and similar, and receipts to `pdlf\step-NN-receipt.md`. The build plan's rule is now: every artifact goes to its canonical place, with a copy in the step's output folder `{slug}-project-library\pdlf-outputs\{step}\`, named `{slug}-{step}-{name}`, for example `mb5pdlf-b14-ceo-plan.md`; the receipt is `{slug}-{step}-receipt.md` in the same folder. `spec-nomenclature.md` in `project-library-global` still carries the old forms (receipts in `pdlf\`, copies in `C:\pdlf\output\output-{tool}\`, the code repository named `{slug}`) and must be corrected with them.

[DONE] **Proposal: names for repeated runs.** Applied: `{slug}-{step}-{run}-{name}` in `spec-artifact-handover.md`, `spec-execution-discipline.md`, build plan sections 1 and 8, and `spec-nomenclature.md`. The feature path runs Steps 12 to 16 once for every feature, so a fixed file name would be overwritten. Every Phase B output name therefore carries the run it belongs to: `app` for the whole application, or the feature slug for a feature. For example, `mb5pdlf-b14-app-ceo-plan.md` and `mb5pdlf-b14-reminders-ceo-plan.md`. Why: each feature's outputs stay side by side with the application's, and none is lost.

#### B.2.4 Where GStack skills run [DONE]

[DONE] **Proposal.** GStack's skills work out where to save from the Git repository they are started in (the "GStack slug"). They also look at that repository's history and files during their own pre-review audit. Phase B's GStack skills (`/office-hours`, `/plan-ceo-review`, `/plan-eng-review`) are always started from the project library. Their GStack slug is then fixed as `sassycomapp-{slug}-project-library`, and every Phase B skill finds the others' files in the same place. Why: Phase B produces documents, not code, and the project library is where those documents belong. The existing code of an existing application reaches the skill by being pasted in, not by the skill's own audit of a code repository.

#### B.2.5 The Anvil context pack [DONE]

[DONE] **Finding.** The Phase B review (finding 1.8) found that no Phase B skill is given the platform's non-negotiable rules. Steps 12, 14 and 15 shape the architecture through general-purpose GStack skills written for ordinary web development. A general architecture review is exactly where a shared database, or a build pipeline Anvil does not have, gets proposed. The review's correction 3 asked for "a standard context pack"; it was never designed.

[DONE] **Proposal: what the pack is.** One document in `pdlf-library`, `spec-skill-context-pack.md`, lists the files that make up the pack. It holds no content of its own, only the list, so that each fact keeps its one home. At every skill invocation in Phase B the orchestrator pastes the full text of the listed files, after the step's own handoff material. The pack for Phase B is:

1. `spec-five-app-architecture-model.md`: the five apps, why each exists, and the rule never to add forms or server modules to a client instance.
2. `adr-dependency-based-not-multi-tenant.md` and the threat model `sec-multi-tenant-assumption-leakage.md`: no shared database, no tenant column, no tenant filter, ever.
3. `pol-anvil-first-development.md`: use Anvil's own facility first; the Vault is the only standing exception.
4. PDLF's `pol-anvil-platform.md`: `anvil.yaml` is never written by an agent; `client_code` and `theme/assets` are public; what goes to Anvil.
5. `spec-anvil-platform-standards.md` and `adr-anvil-platform-constraints.md`: what Anvil can and cannot do.
6. The defaults of Anvil's `data-models` skill: tables default to no client access, data rules live in model classes and server code, server-side authority over identity and ownership.
7. `spec-m3-design-standards.md`: every application uses Anvil's Material 3 theme.

[DONE] **Proposal: the "not applicable to Anvil" list.** The pack ends with a short list of the parts of the GStack reviews that have no meaning for an Anvil application, with the instruction to record each as "not applicable: Anvil application" and not to put a question to David about it. From the skill sources read: the distribution check and distribution architecture (Anvil has no build or publish pipeline of the app's own), the worktree parallelisation strategy, test-framework detection (PDLF states its own test method instead, see Step 15), and pull-request and CI/CD assumptions. Why: every question that does not apply costs David attention and makes him more likely to agree to the ones that do (the review's finding 2.3).

Why the pack matters most in Phase B: Phase B fixes the concept, the scope, the architecture and the data design. A mistake that enters here, such as a tenant column, is built into every later step.

#### B.2.6 Questions to David [DONE]

[DONE] **Designed.** GStack's plan reviews put every finding to David as its own question, one at a time, with options and a recommendation, and stop until he answers. Their "anti-shortcut" rule forbids writing findings into the plan without asking first.

[DONE] **Finding: the Matt Pocock interview asks in rounds.** The installed `grilling` skill (the pinned version, commit `84fdeff`) maps the decisions as a tree and asks "the whole frontier in one round": every question that can be asked now, numbered, each with a recommended answer. The Step 16 files describe it as "one decision at a time", which is not what the skill does. A round can be long.

[DONE] **Settled (David).** The skill runs as it is designed: each round asks every question that can be asked at that point. PDLF never limits or reshapes a skill's questions, because they were built into the skill for a reason. Applied to `b16-build-plan.md` and `b16-reference.md`.

#### B.2.7 Security in Phase B: Sentinel and `secure-software-engineering` [DONE]

[DONE] **Designed.** Sentinel (`mb-sentinel-review`) runs at Step 16 only, at Low/Medium scrutiny, asking whether sensitive data or security-relevant entities are being created. A Flag or Escalate stops the step and goes to David. A Clear writes its own resolved row. The gate does not begin until a `triage_findings` row proves Sentinel actually ran.

[DONE] **Finding.** Sentinel's step table covers Steps 16, 17, 19, 20, 21, 34, 35, 37, 38, 39, 45 and 46. It has no row for Steps 14 or 15, and the `triage_findings.source_step` check only allows those step numbers. A step that is not in the table gets an immediate Clear with no analysis and no record. So adding Sentinel to Steps 14 and 15 is not only a PDLF change: Sentinel's table and the ledger's check must change too.

[DONE] **Finding.** `sec-requirements-architecture-review.md` requires that, before architecture is locked, every trust boundary is named, each is matched to the security document that governs it, and responsibility for each is assigned. Its Sentinel row is Step 34. But PDLF locks the technical plan at Step 15, nineteen steps earlier. Nothing in Phase B produces the trust-boundary list, so Step 34 would have nothing to check against.

[DONE] **Proposal: security across Phase B.**

| Step | What is done                                                                                                                                                                | With what                                                                 | Why here                                                                               |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| 12   | The design doc's Constraints section states the platform's security facts: one app and one database per client, server-side authority, public client code.                  | The Anvil context pack                                                    | The concept must not assume anything the platform forbids.                             |
| 14   | Security requirements at the level of the business: what data the app holds, whose it is, who may see or change it, what must never leak. Written into the CEO plan.        | `secure-software-engineering` (requirements part), given the context pack | Requirements belong with scope: they change what is built.                             |
| 14   | Sentinel review, Medium: "Does the chosen scope create data or capabilities that need protection, and are they in the security requirements?"                               | `mb-sentinel-review`                                                      | A scope that adds payments or personal data must be seen before engineering begins.    |
| 15   | Threat model and the explicit trust-boundary list required by `sec-requirements-architecture-review.md`, each boundary matched to its governing `security-global` document. | `secure-software-engineering` (threat-model part)                         | This is where the architecture is locked.                                              |
| 15   | Sentinel review, High: "Where are the trust boundaries, and is each one governed and assigned?"                                                                             | `mb-sentinel-review`                                                      | Step 34 then verifies the built skeleton against this list, instead of discovering it. |
| 16   | Existing Sentinel review, Low/Medium: sensitive data or security-relevant entities in the vocabulary.                                                                       | `mb-sentinel-review`                                                      | Unchanged.                                                                             |

[DONE] **Settled (David): Sentinel is applied wherever security applies.** In Phase B that is every step: 11 (High: public app repositories, secrets and access), 12 (Medium), 14 (Medium), 15 (High) and 16 (Low/Medium). Applied to `mb-sentinel-review.md` (step table and document map) and to the build rules of Steps 11, 12, 14 and 15; the ledger's `source_step` check is widened in B.2.9. Originally three changes outside Phase B were listed: rows for Steps 14 and 15 in Sentinel's step table; 14 and 15 added to the `source_step` check in the ledger; and the gate proof (a real `triage_findings` row) extended to Steps 14 and 15. The `secure-software-engineering` skill names "design multi-tenant trust boundaries" among its uses, so it must always receive the context pack: in PDLF there is no multi-tenant boundary to design.

#### B.2.8 Anvil's own skills in Phase B [DONE]

[DONE] **Finding.** No Phase B step uses any of Anvil's skills (`anvil-agent-references`), although the build plan calls Anvil compliance "the central tenet". The review (finding 1.7) named `data-models` for Steps 15 and 16.

[DONE] **Proposal.**

- **Step 15 uses `data-models` as its method for persisted data.** The skill says to use it "before choosing an architecture for persisted domain data". In Phase B there is no code yet, so the skill's design steps apply (identify domain objects, table ownership and trust boundaries; choose the data shape; decide where behaviour belongs) and its code steps (editing modules, `anvil --json validate`, the testing skill) do not. Its defaults become rules of the data design: tables default to no client access; data rules live on model classes or in server code, not in forms; any client-visible view is deliberately restricted.
- **Step 16 uses `data-models` to check that the vocabulary and the data design agree** (see Step 16).
- **The Material 3 documents in the Anvil reference set** (`docs/m3/`) are part of what Step 12 and Step 14 consult for anything about the interface. The design system itself is made at Step 20.
- **Anvil's `client-forms`, `client-modules`, `server-code` and `anvil-yaml` skills are not used in Phase B**: no form, module or manifest is written in Phase B. `anvil-yaml` edits `anvil.yaml`, which PDLF never lets an agent write; that conflict belongs to Phase C (Step 17) and is noted here only so it is not lost.

#### B.2.9 The ledger in Phase B [DONE]

[DONE] **Designed.** Each step writes its `steps` row, its BFT record and its receipt from the row. Step 12 records `synthesized`. Step 16 writes the gate row. Deviations are written to `deviations`.

[DONE] **Finding: the step files write values the ledger rejects.** The reference files write `type = 'SKILL'`. The real column is `step_type`, and its check allows only the lowercase values `skill`, `manual`, `optional` and `gate`. The `skill_family` check allows `gstack`, `matt-skills`, `opencode`, `manual`; Phase B also uses Anvil skills, Sentinel and `secure-software-engineering`, which fit none of them.

[DONE] **Finding: the INPUT NOTICE cannot work unless `inputs_used` is filled.** The notice that warns later steps about a synthesized Step 12 is driven by each step's `inputs_used`. No Phase B step says to fill it.

[DONE] **Finding: the ledger cannot hold the feature path.** The `steps` table allows one row per project and step number (`UNIQUE (project_slug, step_number)`). The feature path runs Steps 12 to 16 again for every feature, so the second feature's Step 12 row would be refused.

[DONE] **Finding: the ledger cannot hold the five-app project.** The `projects` table has one `code_path` and one `gbrain_source_code`. A business now has four code repositories (`{slug}-app-1`, `-app-2`, `-app-3`, `-app-5`).

[DONE] **Proposal: one ledger change, made before Phase B is built.** (a) Add a `run` column to `steps` (`app` for the whole application, or the feature slug) and make the unique rule `(project_slug, step_number, run)`; the feature loop's `35.1`, `35.2` numbering can use the same column. (b) Add `app_number` to `steps`, so every row says which app it concerns. (c) Replace the single code path in `projects` with one path and one Anvil address per app (`app1_path`, `app3_path`, `app5_path`, with App 2 recorded at release), keeping the ledger at seven tables. (d) Widen `skill_family` to include `anvil`, `mybizz` (Sentinel and the mybizz-os skills) and `security`. Every Phase B step then fills `inputs_used`. Why: the ledger is what lets the orchestrator refuse a step whose inputs are not done, and it can only do that if it can record what really happened.

[DONE] **Applied (2026-10-13).** The live ledger was backed up (`C:\pdlf-backups\pdlf-ledger-2026-10-13-before-change.dump`) and changed in one transaction: `steps` has `run` and `app_number`, its unique rule is (`project_slug`, `step_number`, `run`), and `skill_family` allows `anvil`, `mybizz` and `security`; `projects` has one path and one Anvil address per app and no code path or code source; `triage_findings.source_step` allows Steps 11, 12, 14 and 15. `spec-postgres-ledger.md` and point 8 of `spec-execution-discipline.md` describe the new ledger and require `inputs_used` to be filled.

#### B.2.10 Thinking checkpoints (BFT) [DONE]

[DONE] **Designed.** Every Phase B step is at **Full** BFT: all six questions, each answered specifically about what just happened. Step 16 is a gate, which is always Full. A blank, generic or copied answer counts as no answer and the step is not done.

[DONE] **Proposal.** Each Phase B step's BFT names the `project-library-global` files it read and applied (in MUSCLE, "which channels were used"), so that compliance can be checked rather than claimed, as the global-content ADR requires. Each step's HEALTH answer states the one consequence downstream that worries the agent most. Why: in Phase B the main risk is a decision whose cost appears only in Phase C or later, and HEALTH is where that is looked at.

#### B.2.11 Learning in Phase B [DONE]

[DONE] **Designed.** Each lesson is written once, into the source the next build reads: a lesson about Anvil or good applications into `project-library-global`; a lesson about PDLF into the step, rule or specification concerned; a lesson about one application into its `docs-local`. Lessons reach GBrain only through the memory governor and `mb-submit-memory`, at close-out.

[DONE] **Proposal: what each Phase B step learns from.** When David corrects a step's work, the step proposes the lesson and its home before it stops. Examples by step: a correction of the canonical and consequential split (Step 12) is an application lesson; a GStack section that did not fit Anvil (Steps 14 and 15) is a lesson for the context pack's "not applicable" list; a term the vocabulary needed that the design doc never named (Step 16) is a lesson for Step 12's questioning. The lesson is then saved at close-out through `mb-submit-memory`.

### B.3 Step 11, Init: lay the foundation

**What it must achieve.** A sound foundation for the business and the app being started: its repositories exist and are linked to GitHub, its project library has the standard structure and step folders, it is registered where it must be, and its record is in the ledger, so that every later step can rely on all of it without checking again.

**What it starts from.** The entry record (B.1); David's answers; the project template at `C:\dev\project-template\dev-(SLUG)\`; the ledger; GBrain.

**What it produces.** The project folder and its repositories, linked to GitHub; the project library with its folders and the step folders `pdlf-outputs\a01\` to `pdlf-outputs\f46\`; for a new application, the three blank pre-project files; the GBrain registration of the project library; the `projects` row; the receipt and BFT record in `pdlf-outputs\b11\`.

**Carried out by.** OpenCode. Two actions belong to David and are never done by the agent: creating the app in Anvil (which creates its code repository), and every commit and push.

#### How it runs today, in order (Designed)

1. Ask whether the application is new or existing, and ask for the slug.
2. Check the ledger is reachable through the PowerShell bridge on port 5433, with all its tables.
3. **New application.** Ask for the code repository's GitHub address. If there is none, tell David to create the app in Anvil first, because Anvil creates the code repository; ask again until an address is given. Copy the project template into `C:\dev\dev-{slug}\` with the slug substituted in folder names and file contents. Link the code repository. Ask permission to create the documentation repository on GitHub; on approval create and link it. Ask David to supply the three pre-project files.
4. **Existing application.** Ask for both GitHub addresses and both local paths. Compare the documentation repository's folders with the template's; create only folders that are missing, change nothing that exists, and add no `Instructions.md` to a new folder (a standing freeze). Check both GitHub links and both GBrain registrations; correct anything broken only with David's permission. Ask David to confirm the data in both repositories is sound.
5. **Both.** Update the project's `AGENTS.md` (created, when missing, from the global template in `docs-standard-global`); set up `.gitignore`, `.opencode`, the GStack configuration and the Matt Pocock skills configuration. Register the project's GBrain sources. Check `project-library-global` is registered. Write the `projects` row.
6. Self-audit everything: report every error at once, and correct nothing without David's permission.

The rules behind it, and why (Designed): the agent never creates a code repository, because an Anvil app's repository must come from Anvil; no Git operation ever runs without permission; global reference files are never copied into a project, because a copy drifts from its source; for an existing application nothing that exists is changed, because the existing material is David's.

#### Findings

1. **Retired items still in Step 11.** The early "commit and push now?" and "use `mb-submit-memory` now?" questions (items 18 and 19), the end-of-step five-action sequence (item 22), the project registry (`C:\pdlf\registry\projects.json`), the project inventory (`C:\dev\dev-root\project-inventory.md`), the devlog and judgement trail, and every `makepdlf` path are retired. The ledger has seven tables, not six (item 3 still lists six and omits `triage_findings`).
2. **Step 11 predates the four-repository scaffold.** It creates one code repository named `{slug}`. The build plan now gives every business `{slug}-app-1`, `-app-2`, `-app-3`, `-app-5`, one `{slug}-project-library` and a `wip` folder. The project template must be brought to the same shape.
3. **The step folders are not created.** The build plan says Step 11 creates `pdlf-outputs\` with one folder per step for a new project. Step 11 does not mention them.
4. **A new documentation repository is not covered by the commit hook.** `commit-all.sh` and the commit hook (`mb-doc-check`) act only on the repositories in their lists (`mb-doc-check.sources`). A new project library that is not added is committed without the hook: no document identities, no link repair, and no GBrain update. Step 11 never adds it.
5. **The pre-project file names are numbered** (`01-project-brief`, `02-scoping-ideas`, `03-constraints-and-notes`). `adr-filename-and-frontmatter-numbering-policy.md` decides that files are not numbered anywhere. The blank set must also ship with PDLF (build plan section 4) rather than with the template.
6. **The Matt Pocock setup is a conversation, not a file copy.** `setup-matt-pocock-skills` (read in source) explores the repository, then asks David three questions (where issues are tracked, the triage labels, the layout of the domain documents), shows its drafts, and writes `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md` and an "Agent skills" block in `AGENTS.md`. Its defaults put the glossary and decisions at `GLOSSARY.md` or `CONTEXT.md` and `docs/adr/`, which is not where PDLF keeps them. Step 11 says only "set up Matt Pocock skills configuration".
7. **Entry points 07 and 08 do not fit Step 11 as written.** Step 11 builds a business from nothing or adopts an existing one. Creating App 3 or App 5 for a business that already exists is neither.

#### Proposals

**P11.1 Step 11 is reshaped around the entry record, with three routes and one common end.**

*Route A, a new business (entry 02).*

1. Ask for the slug (lowercase, no hyphens), the business's name, its domain (for example `mb3cs.site`) and the mode (`full` or `test`).
2. Run the foundation checks (P11.4).
3. Create the project folder `C:\dev\dev-{slug}\` from the template, with the whole scaffold: `README.md`, the four app folders, `{slug}-project-library` and `wip`. David prefers the full structure in place from the start; the app folders for Apps 2, 3 and 5 stay empty placeholders until those apps exist.
4. App 1: David creates the app in his Anvil account and connects it to GitHub. The agent gives him exact numbered instructions, generated with the `wizard` skill, which exists for "steps only a human can perform" and opens each page for him. He gives the address; the agent clones it into `{slug}-app-1` and checks the clone holds an Anvil app (`anvil.yaml` present). The agent never writes to `anvil.yaml`.
5. App 1's `.gitignore` is set to the PDLF baseline: `.env`, credentials, `__pycache__`, test output and development files, as `pol-anvil-platform.md` requires, because everything committed is pushed to Anvil.
6. The project library: ask permission to create the private repository `{slug}-project-library` on GitHub; create and link it; lay out its folders from the template, including `pdlf-outputs\a01\` to `pdlf-outputs\f46\` (with `b13\` and `c25\`), `docs-local\`, `adr-local\` and `pre-project\`; place the blank pre-project files from the set that ships with PDLF.
7. The Matt Pocock setup (P11.3).
8. Register the project library in GBrain as a federated source named `{slug}-project-library`.
9. Ask David to add the new project library to the commit hook's source list and to `commit-all`, giving him the exact lines and the WSL terminal command. The agent cannot do this itself: it is a change to mybizz-os scripts. The step does not finish until David confirms, because without it the project's first commit bypasses the hook.
10. The common end (P11.5).

*Route B, an application with context (entry 03).* As today's existing-project route, extended to every repository the business has: ask for each one's GitHub address and local path, check each link, create only missing folders, change nothing that exists, correct nothing without permission, and ask David to confirm each repository's data is sound. The step folders are created only where missing. If the business still uses an old name (such as `mb-3-cs` before its rename to `mb3cs`), the step reports it and does not rename anything: renaming is its own job.

*Route C, a new app in an existing business (entries 07 and 08, if David agrees they join here).* Run the health check on the business first. Then only the app's own part of Route A: David creates the Anvil app, the agent clones and links it into its app folder, sets its `.gitignore`, and records it in the `projects` row. The project library already exists and is not touched.

**P11.2 Where entries 07 and 08 join.** App 3 (`blank_client_template`) holds the full table schema, one startup module and `master_template` as its dependency, and nothing else. It can only be built once App 2 exists and the schema is settled, which is after the first release. So entry 07 belongs with the remaining-apps steps in `phase-g`, not at Step 11. App 5 (the management app) is a different application with its own concept and scope, inside the same business. So entry 08 runs Step 11 by Route C and then the whole of Phase B for App 5, at full size. **Open for David.**

**P11.3 The Matt Pocock setup, with PDLF's answers fixed in advance.** Step 11 runs `setup-matt-pocock-skills` in the project library and gives it PDLF's answers, so David is asked only to confirm. Issue tracker: GitHub Issues on the private project library, because App 1's code repository is public and tickets describe internal plans. Triage labels: the five defaults, which are also exactly the values the ledger's `triage_findings` table accepts. Domain documents: single context, with the glossary at `{slug}-project-library\CONTEXT.md` and decisions in `{slug}-project-library\adr-local\`. Why: once `docs/agents/domain.md` records PDLF's locations, every Matt Pocock skill (`to-tickets` at Step 19, `triage` at Step 39, `improve-codebase-architecture` at Step 40) reads the glossary and decisions from the right place, and Step 16 no longer has to override the skill's defaults at every run. The "Agent skills" block is written into the project library's `AGENTS.md`, which already exists; the skill is told never to create a `CLAUDE.md`. **Open for David:** where tickets live (recommendation above).

**P11.4 The foundation checks, at the start.** The ledger answers on port 5433 with all seven tables; GBrain answers and the sources `default` and `pdlf` are registered; the clone of Anvil's skill set is present; the installed Phase B skills are present (`office-hours`, `plan-ceo-review`, `plan-eng-review`, `grilling`, `grill-with-docs`, `domain-modeling`, `setup-matt-pocock-skills`, `data-models`, `secure-software-engineering`, `mb-sentinel-review`, `wizard`). Any failure stops the step with a deviation before anything is created. Why: a broken tool found at Step 15 costs a half-finished review; found at Step 11 it costs nothing.

**P11.5 The common end, which is also the health check.** For every route: the self-audit checks that each repository exists locally, is linked to the right GitHub repository, and holds what it should (an Anvil app for an app folder; the standard folders and step folders for the project library); the project library is registered in GBrain and covered by the commit hook; the `projects` row matches what is on disk; the Matt Pocock configuration exists and points at PDLF's locations. Every mismatch is reported and nothing is corrected without permission. Then the receipt, the Full BFT, the explanation, and the request for `/mb-close-out`. This same self-audit is the health check used by entries 04 to 10 (B.1).

**P11.6 The project's own `AGENTS.md`.** The project library's `AGENTS.md` comes from the global template, as today. Anvil publishes an `AGENTS.md` template for app repositories (in `anvil-agent-references`) whose rules (validate files with `anvil --json validate`, never edit `.anvil/` dependency material, use Anvil's five skills) are exactly what an agent working on App 1 needs. **Open for David:** whether App 1's code repository receives an `AGENTS.md` built from Anvil's template. It would be pushed to Anvil and stored there unused, which is harmless, but it is a document in a code repository. Recommendation: yes, because it is instructions for agents, not project documentation, and it makes Anvil's rules apply whenever any agent opens App 1.

**Ledger and BFT.** One `steps` row (`step_type = 'skill'`, because the ledger has no separate type for OpenCode's own work, and `skill_family = 'opencode'`), the `projects` row, and a Full BFT, because Step 11 makes the structural decisions everything else stands on.

**Failure handling.** A missing tool, an unreachable ledger, a GitHub address that does not hold an Anvil app, or a repository linked to the wrong remote stops the step with a deviation. David's refusal of the documentation repository stops the step: there is no project without it.

### B.4 Step 12, Office hours: write the design doc

**What it must achieve.** The design doc: what problem the application (or the feature) solves, for whom and how, stated well enough for every later step to build on, and challenged before it is accepted.

**What it starts from.** The entry record; for a new application, the three pre-project files; for an application with context, its existing documentation; for a feature, the feature statement and the application's existing design doc, glossary and decisions; the Anvil context pack.

**What it produces.** `docs-local\design-doc-first-concept.md`, written once and never changed; `docs-local\design-doc.md`, the working copy; the `/office-hours` result if it ran; copies of all three, and the receipt, in `pdlf-outputs\b12\`.

**Carried out by.** OpenCode, with `grilling` for the questioning, and GStack `/office-hours` if David chooses it.

#### How it runs today, in order (Designed)

1. Search GBrain.
2. **New application.** Read the three pre-project files. Question David until the scope is adequately described.
3. **Existing application.** Read the whole project library through GBrain. Separate the canonical (the lasting concept) from the consequential (what merely followed from it). Show David plainly any document that already claims to state the concept, never folding it silently into the reading. Propose the split side by side with that document, showing where they agree and differ. David confirms or corrects. This is propose-and-confirm, not an interrogation. The application is redeveloped around its concept, not audited.
4. **Both.** Write the design doc in a fixed structure: Problem Statement, Demand Evidence, Status Quo, Target User and Narrowest Wedge, Constraints, Approaches Considered, Recommended Approach, Open Questions, Success Criteria. Save it twice: the first concept, never touched again, kept to detect drift later; and the working copy.
5. Ask David whether to run `/office-hours`.
6. **Declined.** The ledger records `synthesized = true`; later steps that use this doc show an INPUT NOTICE on their receipts.
7. **Accepted.** Paste the source material and the full text of the first concept into `/office-hours`. The skill (confirmed in its source) treats a fully formed plan by skipping its interview but still running its premise challenge and alternatives. It saves to `~/.gstack/projects/sassycomapp-{slug}-project-library/{user}-{branch}-design-{datetime}.md`. Capture that path, copy the file over the working copy, record `synthesized = false`, and never move or edit the skill's own file.
8. Verify the outputs exist; otherwise a deviation.
9. Hand four items to Step 14: both design docs, the `/office-hours` result if any, and the receipt.

Rules and why (Designed): the design doc is always written before `/office-hours` is offered, so a decline still leaves a real doc; the first concept is frozen, because drift can only be seen against something that does not move; the draft is pasted in full, because `/office-hours` reads only `CLAUDE.md`, `TODOS.md`, Git history and its own earlier design docs, never PDLF's folders. Step 12 is not eligible for test-mode shortening; its only choice is whether `/office-hours` runs (`pol-step-conditional-state.md`).

#### Findings

1. **Step 12 improvises a task a skill covers.** "Query the developer diligently" is improvised questioning. The catalogue's `grilling` does exactly this, and the build plan says skills take precedence (review finding 1.9).
2. **No platform context reaches the concept.** Neither the synthesis nor `/office-hours` is told the application is an Anvil application in the five-app structure with no shared database. A concept that assumes, for example, one shared customer list across clients, would pass Step 12 unchallenged.
3. **Step 12 has no feature mode.** The build plan sends the feature path to Step 12 ("describes the feature and checks it against the application's existing design"). The step files describe only new and existing applications.
4. **`/office-hours` has two modes and PDLF does not choose.** Its source describes a startup mode (six forcing questions about demand, status quo, specificity, the narrowest wedge, observation and future fit) and a builder mode (design brainstorming for side projects). Step 12 leaves the choice to the skill's own question.
5. **Some downstream steps still expect documents Phase B does not produce.** Step 21's inputs name a Step 13 specification that no longer exists. `project-library-global` holds standards for a product requirements document, a business requirements document and a software requirements specification (`docstd-...`) that no step produces. This is noted so that Phase C does not wait for them; whether those standards are still wanted is outside this version's scope.

#### Proposals

**P12.1 `grilling` does the questioning.** For a new application, Step 12 invokes `grilling` with the pre-project files and the context pack pasted in, and the instruction to work toward the nine sections of the design doc. The interview's tree ends when every section can be written without guessing. For an existing application, `grilling` is used only for what the propose-and-confirm leaves unsettled. Rounds are limited to three questions (B.2.6). Facts the agent can look up are never asked of David; `grilling` itself requires this.

**P12.2 The Constraints section always states the platform.** The design doc's Constraints section names, in plain words: built on Anvil.works; one app and one database for each client, never shared; all business logic and data rules on the server; Material 3 interface; and the app's place in the five-app structure. Each constraint names the global document it comes from. No new section is added, so the structure `/office-hours` recognises is unchanged.

**P12.3 The feature mode.** For entries 04, 05 (a change to what the app does), 09 and 10: Step 12 reads the application's design doc, glossary and decisions, then uses `grilling` to describe the feature in the same nine sections, at the size of the feature. It then compares the feature with the application's canonical concept, section by section. A feature that contradicts the concept is not a feature: the step stops with a deviation, because changing the concept means re-running Phase B for the whole application. The feature's design doc and its frozen first concept are saved as `docs-local\features\{feature-slug}\design-doc.md` and `design-doc-first-concept.md`; the application's own design doc is not changed by a feature until David approves that change.

**P12.4 `/office-hours` runs in startup mode for a Mybizz business.** Every application PDLF builds is a business with paying clients, so demand, status quo and the narrowest wedge are the right questions. Builder mode fits only the test application, and only if David wishes. The invocation states the mode, so the skill does not ask. **Open for David:** which mode for `mb5pdlf`.

**P12.5 How the existing-application split is shown.** The canonical and consequential split is presented as a two-column list, one row per document or decision, with the agent's reason for each placement in one sentence. David corrects rows, not prose. A correction is a lesson for that application's `docs-local` (B.2.11).

**P12.6 A recorded approval of the concept.** Whether or not `/office-hours` ran, the step ends by asking David to approve the working design doc as the concept the reviews will challenge. His yes is recorded in the ledger as a decision. Whether this should be a full gate is **Open for David** (see Step 14, P14.7).

**Ledger and BFT.** `step_type = 'skill'`, not `optional`: Step 12 always produces a doc, and its `/office-hours` choice is recorded through `synthesized`. `skill_family` is `gstack` when `/office-hours` ran, otherwise `matt-skills` (for `grilling`). `inputs_used` names the pre-project files or the existing documents. Full BFT, because the concept shapes everything after it.

**Failure handling.** A missing pre-project file stops the step: the agent asks David for it, never writes it itself. An `/office-hours` run that reports no saved file, or a file that is not where it said, is a deviation. A feature that contradicts the concept is a deviation (P12.3).

### B.5 Step 14, CEO review: settle scope and ambition

**What it must achieve.** The design's scope and ambition challenged and settled, with David choosing how far the scope goes. The result is the CEO plan, which also names what must be tested and why, and states the security requirements the scope creates.

**What it starts from.** The four items from Step 12; the context pack; the `project-library-global` standards the review touches.

**What it produces.** The CEO plan with its review report, captured in every scope mode; its copy and the receipt in `pdlf-outputs\b14\`.

**Carried out by.** GStack `/plan-ceo-review`, with `secure-software-engineering` for the security requirements and `mb-sentinel-review` (if agreed).

#### How it runs today, in order (Designed)

1. Search GBrain. Check Step 12's `synthesized` flag; if true, this receipt carries the INPUT NOTICE.
2. Assemble Step 12's four items.
3. The local and global comparison: OpenCode compares what the review touches with `project-library-global`. The global standard wins unless David approves a deviation. (Confirmed in source: the skill itself has no knowledge of `project-library-global`, so this is OpenCode's own work.)
4. Invoke `/plan-ceo-review` with all four items pasted in full and a plain statement that a design doc already exists. This is load-bearing: the skill looks for a design doc in its own folder; when Step 12 declined `/office-hours` it finds none and would offer to run `/office-hours` inside Step 14, reopening Step 12's decision.
5. The skill runs its system audit, then Step 0 (premise challenge, existing-code leverage, dream state, implementation alternatives, and the choice of mode), then its review sections, each finding put to David one at a time.
6. David chooses the mode: scope expansion, selective expansion, hold scope, or scope reduction. Once chosen, the skill commits to it (it does not argue for less work in expansion, nor sneak scope back in reduction).
7. Capture the plan in every mode. The skill saves its own file only in the two expansion modes (`~/.gstack/projects/sassycomapp-{slug}-project-library/ceo-plans/{date}-{feature-slug}.md`); in hold and reduction it saves nothing, so OpenCode saves the conversation's review itself.
8. Verify; write the row; receipt; BFT; hand the CEO plan, both design docs and the receipt to Step 15.

#### Findings

1. **Steps 14 and 15 review the same subjects twice.** `/plan-ceo-review`'s eleven sections include architecture, error and rescue, security, data flow, code quality, tests, observability, database and state, interfaces (API design), performance, and design. `/plan-eng-review` reviews architecture, code quality, tests and performance again. Both put every finding to David. He would be asked about the same subjects twice, which is how a tired reviewer starts agreeing to everything (review finding 2.2).
2. **The plan is not handed to Step 15 reliably in hold and reduction modes.** Step 15 is told to find the CEO plan by Step 14's mode, "recorded in the ledger", but the ledger has no column for the mode.
3. **The CEO review also has an outside voice.** `/plan-ceo-review` offers the same independent second opinion as `/plan-eng-review` (its dashboard notes both). Only Step 15's files account for it.
4. **The local and global comparison names no standard.** "Compare what the review touches" gives the agent no list, so what it compares is improvised.

#### Proposals

**P14.1 Separate remits for Steps 14 and 15.** Step 14 owns: the problem and premise, the users and their journeys, the scope and its mode, ambition and alternatives, the data and interaction edge cases as users experience them, the security requirements at the business level, and what must be tested and why (the user journeys that must work). Step 15 owns: architecture, error and rescue paths, code quality, the concrete tests, observability, data design and state, the server-call interface, performance, and the threat model. The Step 14 invocation tells the skill to record the sections that belong to Step 15 as "deferred to Step 15 (engineering review), by PDLF design", and to ask David nothing about them. Why: each question is asked once, by the review best placed to ask it. The skill's own rules may resist leaving sections unreviewed; whether it honours the instruction is checked on the first run, and if it does not, the instruction becomes "review briefly, record findings, ask nothing; Step 15 decides".

**P14.2 The mode is recorded.** The mode David chooses is written to the `steps` row (in `notes_for_next_session` until the ledger change in B.2.9 gives it a home), and the capture is always saved as `{slug}-b14-{run}-ceo-plan.md` in `pdlf-outputs\b14\`. Step 15 always reads that copy, so it never has to know the mode.

**P14.3 Guidance for the mode choice.** Before David chooses, the step gives a one-line recommendation from the entry record: a new business, selective expansion (hold the core, choose expansions one by one); a feature or an update, hold scope; the test application, scope reduction, because its purpose is to test PDLF, not to be a product. David decides; the recommendation is only to save him working it out.

**P14.4 Security requirements.** After the review sections, Step 14 applies `secure-software-engineering` (its requirements part) with the context pack: for each kind of data the scope creates, whose it is, who may read and change it, what must never reach a browser, and what must never be shared between clients (always "nothing", by construction). The result is a section of the CEO plan, "Security requirements".

**P14.5 Sentinel at Step 14** (if David agrees B.2.7), after the security requirements, before the step is verified.

**P14.6 A named list for the local and global comparison.** The comparison always covers: the five-app model, the no-multi-tenancy decision, `adr-client-instance-architecture.md`, `adr-anvil-platform-constraints.md`, `adr-data-access-patterns.md`, `adr-tiers-model.md` (where the app has tiers), `spec-m3-design-standards.md`, and `spec-security.md`; plus whatever GBrain returns for the scope's own subjects. Each conflict is shown to David with the global document's line; the global wins unless he approves a deviation.

**P14.7 A gate on scope.** The review (finding 2.4) noted that the concept and the scope, the commitments everything rests on, are not gated; the first gate is at Step 16. **Open for David**, with four options: a gate at Step 12, a gate at Step 14, both, or neither. Recommendation: one gate, `scope-approved`, at the end of Step 14, with Full BFT. By then the concept has been challenged twice (by `/office-hours` and by the CEO review) and the scope mode is chosen, which is the decision that sets the cost of everything after it. Step 12 keeps its recorded approval (P12.6). Adding a gate also means adding it to the run plan, to Cupcake's enforcement, and to `spec-gate-procedure.md`'s list.

**P14.8 The outside voice at Step 14** is treated exactly as at Step 15: informational only; each point where it disagrees with the review goes to David as its own question; nothing from it is adopted without his yes.

**Ledger and BFT.** `step_type = 'skill'`, `skill_family = 'gstack'`, `inputs_used` = Step 12's items; Full BFT, because scope is a strategic decision.

**Failure handling.** If the skill still offers `/office-hours` despite the statement that a design doc exists, the step stops with a deviation: the preemption failed and Step 12's decision must not be reopened inside Step 14. A capture that is empty, in any mode, is a deviation.

### B.6 Step 15, Engineering review: lock the technical plan

**What it must achieve.** The technical plan locked: architecture, data design, error handling, code quality, tests and performance decided for an Anvil application; a concrete test plan for the build steps; and the explicit list of trust boundaries.

**What it starts from.** Step 14's CEO plan (always its copy in `pdlf-outputs\b14\`); both design docs; the `/office-hours` result if any; the context pack; Anvil's `data-models` skill; the global standards the review touches.

**What it produces.** The reviewed engineering plan, with its review report; the Test Plan Artifact; the data design; the trust-boundary list; copies of each and the receipt in `pdlf-outputs\b15\`.

**Carried out by.** GStack `/plan-eng-review`, with `data-models`, `secure-software-engineering` and `mb-sentinel-review` (if agreed).

#### How it runs today, in order (Designed, confirmed against the skill's source copy in `b15-build-plan.md`)

1. Search GBrain. Assemble the CEO plan, both design docs and the `/office-hours` result. The same local and global comparison as Step 14.
2. Invoke `/plan-eng-review` with everything pasted in full and the same statement that a design doc already exists.
3. The skill's Step 0, its scope challenge, which is different from Step 14's: what existing code already does; the minimum change; a complexity trigger (eight or more files, or two or more new classes or services) that stops the review for David to consider a smaller version; search before building; `TODOS.md`; completeness; distribution.
4. Four review sections, each finding put to David one at a time, the skill stopping until he answers: architecture; code quality; tests; performance. Every finding carries a confidence score from 1 to 10, and a finding whose motivating line cannot be quoted is held back as unverified.
5. In the test section the skill draws a coverage diagram of every code path and user journey, decides for each whether a unit test or an end-to-end test fits, adds a regression test without asking for anything that previously worked and would break, and writes the one separate file it produces: the Test Plan Artifact, `{user}-{branch}-eng-review-test-plan-{datetime}.md`, with affected pages, key interactions, edge cases and critical paths. GStack's `/qa` (Step 38) reads it as its main input.
6. Required outputs, written into the plan, not as separate documents: not in scope; what already exists; `TODOS.md` items, each its own question; diagrams; failure modes, with any untested, unhandled and silent failure flagged as critical; worktree parallelisation.
7. The outside voice: an independent review by another AI (Codex if installed, otherwise a Claude sub-agent), informational only; each disagreement goes to David; nothing is adopted without his yes.
8. The review report, which ends with either "NO UNRESOLVED DECISIONS" or the list of open ones.
9. OpenCode captures the findings from the conversation itself, because whether the skill can find "the active plan file" to write into, inside OpenCode, is unconfirmed. Verify; row; receipt; BFT.

Rules and why (Designed): there is no "five-document cluster"; the skill never produces architecture, integration, security, globals or schema documents (an earlier assumption, corrected by reading the full source). The second opinion never decides anything.

#### Findings

1. **Step 17 needs a data design that Step 15 does not produce.** Step 17's input still names the imaginary five-document cluster. What Step 17 really needs is a table-by-table data design that David can build by hand in the Anvil editor. The eng review discusses data access and state, but produces no data design.
2. **The trust-boundary list is required here and not produced** (B.2.7).
3. **The complexity trigger always fires for a whole application.** A new application is always more than eight files and two services, so the skill will always stop to propose a minimal version, although Step 14 has just settled the scope with David.
4. **Several parts of the review assume ordinary web development:** distribution and its pipeline, worktree parallelisation, and test-framework detection that looks for Jest, Vitest, Playwright, Cypress, RSpec or a `pytest.ini`. None of these describes how an Anvil application is built or tested.
5. **PDLF's own test method is not given to the review.** PDLF tests every feature at three levels (pure logic with no Anvil code, then connected to the live development app through Anvil Uplink, then by hand), and requires business rules to live in pure logic modules so that level one is possible (`pol-testing-and-quality.md`). The review designs tests without knowing this.
6. **The newer skill writes outputs PDLF does not use:** an "Implementation Tasks" list and a JSON lines file for `/autoplan`, and at the end it offers to chain into `/plan-design-review` or `/ship`. PDLF's tickets come from Step 19, its design review is Step 23, and nothing ships from Phase B.
7. **`TODOS.md` has no agreed place.** The step files assume the project library's root, "pending confirmation".

#### Proposals

**P15.1 The data design, made with Anvil's `data-models`.** After the review sections, Step 15 applies `data-models` (its design steps, B.2.8) to produce `docs-local\data-design.md`, following the global template `tmp-authoritative-schema.md`. For each table: its purpose; each column with its type; links to other tables; which roles may read and which may write it; client access (none, by default); whether any column holds a secret (which then goes through the Vault, never a plain column); and the model class, if any, that carries its rules. It also records the template's architectural patterns: times stored in UTC, data isolation by separate client apps, and secret management. Each design choice David has not already made in the review is put to him as its own question. Why: this is exactly what `sec-requirements-data-table-creation.md` requires to be decided before a table exists, and exactly what Step 17 builds from. It also closes Phase C's open point about the "TDD cluster" from the Phase B side.

**P15.2 The trust-boundary list and threat model.** Step 15 applies `secure-software-engineering` (its threat-model part) to the locked architecture and produces `docs-local\trust-boundaries.md`: every place data crosses from one trust level to another (browser to server, the app to an outside service such as payments or email, one role's data to another's), each matched to the `security-global` document that governs it, or flagged where none exists, and each assigned to the platform or to the application. Then Sentinel (if agreed, B.2.7).

**P15.3 PDLF's test method is stated in the invocation**, replacing the skill's framework detection: level one tests use pytest on pure logic modules; level two tests use Anvil Uplink against the development app; level three is David by hand in the browser. The test section must map every code path to its level, and treat any business rule placed in a form or in server code (rather than in a pure logic module) as a finding. The Test Plan Artifact keeps the skill's own format, because Step 38's `/qa` reads it in that format.

**P15.4 The scope challenge respects Step 14.** For a whole application, the invocation states that the scope was settled with David at Step 14 in a named mode, that the complexity trigger is therefore expected, and that the skill should record it and continue unless it finds a part of the scope that could be built more simply without losing anything David chose. For a feature, the trigger works as designed. To be confirmed on the first run.

**P15.5 What the review leaves out, by instruction.** The invocation marks as "not applicable: Anvil application" the distribution check, the distribution architecture and the worktree parallelisation; asks the skill not to chain into further reviews; and tells it that its implementation-task list is for information only, because PDLF's tickets are made at Step 19. The performance section is pointed at what matters on Anvil: the number of round trips between browser and server for each screen, how Data Tables are searched, and what belongs in background tasks.

**P15.6 `TODOS.md` lives at the root of the project library.** That is where the skill looks (it runs in the project library, B.2.4), and the project library is where deferred work belongs. Every item added is shown to David as its own question, as the skill already requires. Nomenclature records the location.

**P15.7 Outputs and handoff.** Saved and copied to `pdlf-outputs\b15\`: `{slug}-b15-{run}-eng-plan.md`, `{slug}-b15-{run}-test-plan.md` (copy of the Test Plan Artifact), `{slug}-b15-{run}-data-design.md` and `{slug}-b15-{run}-trust-boundaries.md` (copies of the canonical files in `docs-local\`). Step 16 receives all four, with the design doc.

**Ledger and BFT.** `step_type = 'skill'`, `skill_family = 'gstack'`, `inputs_used` = Steps 12 and 14; Full BFT, because architecture and data are the decisions most expensive to reverse.

**Failure handling.** A Test Plan Artifact that the skill reports and that is not on disk is a deviation. An empty capture is a deviation. An outside-voice failure is not: the skill itself treats it as non-blocking.

### B.7 Step 16, Domain modelling: fix the vocabulary, then the gate

**What it must achieve.** The application's vocabulary fixed, so that a term means the same thing in every later step and every later session; the decisions that are hard to reverse recorded; the data design agreeing with the vocabulary; the application's definition of "done" created; and the whole of Phase B approved at the gate `domain-locked`.

**What it starts from.** Step 15's four outputs and the design doc; for an existing application, its existing glossary, decision records and code, marked as prior material; the context pack.

**What it produces.** `CONTEXT.md` (the glossary) and any decision records in `adr-local\`, in the project library; the reconciled data design; the ISA; the Sentinel record; the gate row; copies and the receipt in `pdlf-outputs\b16\`.

**Carried out by.** Matt Pocock's `/grill-with-docs`, which runs a `grilling` interview using `domain-modeling`; then `data-models`; then `mb-sentinel-review`; then the gate.

#### How it runs today, in order (Designed)

1. Search GBrain. Assemble Step 15's outputs; for an existing application add its existing glossary, decision records and code, marked as prior material.
2. Invoke `/grill-with-docs`, with the material pasted in full and PDLF's file locations stated, in place of the skill's defaults. (`domain-modeling` cannot run on its own; it is a discipline other skills use. `/grill-with-docs` is the skill to invoke.)
3. The interview walks the plan as a tree of decisions. Along the way `domain-modeling` challenges each term against the glossary, sharpens vague or overloaded terms, tests relationships with concrete edge-case scenarios, and, where code exists, checks what David says against the code and shows any contradiction. That last check is idle for a new application and does the reconciliation for an existing one, so no separate mode is needed.
4. Each settled term is written into `CONTEXT.md` at once, never in a batch, as a glossary only, with no implementation detail.
5. A decision record is offered only when a decision is hard to reverse, surprising without context, and the result of a real trade-off. Most decisions will not qualify.
6. Sentinel reviews the terms and records (Low/Medium: sensitive data or security-relevant entities?). A Flag or Escalate stops the step and goes to David before the gate, because it is part of what he approves.
7. Verify `CONTEXT.md` and any decision records exist. Confirm a real `triage_findings` row exists for this step (labelled `clear`, `needs-triage` or `needs-info`), proving Sentinel ran; no row, no gate.
8. The gate `domain-locked`: Full BFT, the gate summary, and David's explicit yes or no. On yes, the gate row with its approval time; on no, the gate is blocked, the blocker recorded, and the pipeline does not move.

Why this step exists (Designed, accepted by David): an agent has no memory between sessions; GBrain gives it facts, and `CONTEXT.md` gives it a fixed vocabulary, so a term cannot quietly change meaning twenty sessions later in the build loop.

#### Findings

1. **The interview asks in rounds, not one at a time** (B.2.6).
2. **The installed and current versions of the skill disagree on the glossary's name.** The installed, pinned version (commit `84fdeff`) writes `CONTEXT.md`. The current upstream version writes `GLOSSARY.md`. PDLF's own documents use `CONTEXT.md`. An upgrade of the Matt Pocock skills would silently change where the skill writes, unless PDLF's location is stated (as Step 16 already does) and recorded in `docs/agents/domain.md` (P11.3).
3. **Decision records would break the global naming rule.** `domain-modeling` numbers its decision records (`0001-slug.md`), and Step 16 keeps that. `adr-filename-and-frontmatter-numbering-policy.md` decides that no file is numbered anywhere, and every global decision record is named `adr-{name}.md`. David wants one rule everywhere.
4. **The ISA is never created.** `pol-memory-and-knowledge.md` and the ISA template say the ISA, the application's definition of "done", is created at Step 16, with its criteria in the ledger's `isc` table. No Step 16 file mentions it.
5. **The gate's description is stale.** The gate table says `domain-locked` locks "PRD reviewed". There is no PRD.
6. **The gate procedure Step 16 relies on still commits and pushes** (B.2.1).
7. **The feature path collides with the gate.** `domain-locked` means "no new terms without reopening the gate". Every feature that runs Step 16 adds terms by design.
8. **`/grill-with-docs` is marked for the user to start** (`disable-model-invocation: true` in its source). The catalogue notes that OpenCode ignores this setting, so the agent can start it; PDLF's policy says a skill meant to be started by the user is asked of David. The step must say which applies.
9. **The vocabulary is fixed after the data design.** Step 15 names tables and columns before Step 16 settles the terms, so the data design can use words the glossary later rejects.

#### Proposals

**P16.1 Decision records follow the global naming rule.** The invocation states: decision records go in `{slug}-project-library\adr-local\`, named `adr-{name}.md` with no number, using the global decision-record front matter, and Matt Pocock's short format for the body (context, decision and why, in one to three sentences, with optional status, considered options and consequences). Why: one rule for every decision record in the whole estate.

**P16.2 Reconcile the data design with the vocabulary.** After the interview, OpenCode compares every table and column name in `data-design.md` with `CONTEXT.md`, using `data-models`, and puts each mismatch to David as its own question: rename in the data design, or settle a new term. The gate then locks the glossary and the data design together. Why: Step 17 builds tables from the data design, and Step 19 writes tickets in the glossary's words; if the two disagree, the build loop inherits two names for one thing.

**P16.3 Create the ISA.** Before the gate, Step 16 creates the ISA from the ISA template: Problem and Vision from the design doc; Out of Scope from Step 15's "not in scope"; Principles and Constraints from the design doc's Constraints and the context pack; the Goal in one sentence; and one ideal-state criterion (ISC) per success criterion in the design doc and per critical journey in the test plan, each written as a row in the `isc` table with how it will be verified. Its criteria and verification sections are generated from the ledger, never written by hand. The ISA's canonical place is `{slug}-project-library\docs-local\isa.md`; the template still names the retired `pdlf\` folder and is corrected with it. Why: the build loop and Step 46 measure "done" against the ISA, and a criterion that does not exist before the build cannot be checked after it.

**P16.4 What `domain-locked` locks, restated.** The glossary, the decision records, the data design, the trust-boundary list and the ISA criteria. After the gate, none of them changes without a recorded reopening of the gate.

**P16.5 The gate for a feature.** For a feature, Step 16 begins with a formal, recorded reopening of `domain-locked`, limited to the feature's new terms and decisions, and ends by locking it again with the feature's terms added. The application's existing terms can change only through the same reopening, explicitly, never as a side effect. Why: it keeps the rule "no new terms without reopening the gate" true, instead of breaking it quietly with every feature.

**P16.6 Who starts `/grill-with-docs`.** Recommendation: the agent invokes it, as the step files assume, because the step is the orchestrator's own work and David is present for every question. The policy on user-started skills is then made precise: it covers skills that act outside the conversation for David (such as a release), not interviews he takes part in. **Open for David.**

**P16.7 The gate, corrected.** Full BFT; the ledger integrity check (no orphaned rows) the run plan requires before every gate; the gate summary in plain words, listing what is being locked (P16.4), every open Sentinel finding and its status, any INPUT NOTICE inherited from Step 12, and any unresolved decision left by Steps 14 and 15; David's yes or no; the gate row; then the request to run `/mb-close-out`. The agent never commits or pushes at the gate.

**Ledger and BFT.** `step_type = 'gate'`, `skill_family = 'matt-skills'`, `inputs_used` = Steps 12, 14 and 15; the `gates` row; the `triage_findings` row from Sentinel; the `isc` rows. Full BFT, required at every gate.

**Failure handling.** No Sentinel row: a deviation, the gate does not begin. An open Flag or Escalate: the gate does not begin until David has decided it. `CONTEXT.md` missing after terms were settled: a deviation. David's no: the gate is blocked and nothing further happens; no close-out is asked for, because nothing has been approved.

### B.8 What Phase B hands to Phase C

| What                                                | Canonical place                                                      | Copy                | Read by                                  |
| --------------------------------------------------- | -------------------------------------------------------------------- | ------------------- | ---------------------------------------- |
| Design doc (working) and first concept              | `docs-local\design-doc.md`, `docs-local\design-doc-first-concept.md` | `pdlf-outputs\b12\` | 14, 15, 20, 21 (and 46, for drift)       |
| CEO plan, with test scope and security requirements | GStack's folder (expansion modes) or OpenCode's capture              | `pdlf-outputs\b14\` | 15, 19, 21                               |
| Engineering plan                                    | Captured by OpenCode                                                 | `pdlf-outputs\b15\` | 16, 19, 21, 31, 34                       |
| Test Plan Artifact                                  | GStack's folder                                                      | `pdlf-outputs\b15\` | 35, 38                                   |
| Data design                                         | `docs-local\data-design.md`                                          | `pdlf-outputs\b15\` | 17, 31, 34                               |
| Trust-boundary list                                 | `docs-local\trust-boundaries.md`                                     | `pdlf-outputs\b15\` | 17, 34, and Sentinel at every later step |
| Glossary                                            | `CONTEXT.md` (project library root)                                  | `pdlf-outputs\b16\` | every later step                         |
| Decision records                                    | `adr-local\adr-{name}.md`                                            | `pdlf-outputs\b16\` | 17, 21, 34                               |
| ISA and ISC rows                                    | `docs-local\isa.md`; `isc` table                                     | `pdlf-outputs\b16\` | 26, 35, 39, 46                           |
| Gate `domain-locked`                                | `gates` table                                                        | —                   | the orchestrator, before Step 17         |

This resolves three of Phase C's open points from the Phase B side: Step 17's "TDD cluster" becomes the data design (P15.1); Step 21's "Step 13 specification" is not needed, because Step 21 compares the design doc, CEO plan, engineering plan, glossary and decision records; Step 19's "disposition table" for existing projects does not exist, because an existing application runs every step. Phase C's own files are corrected when Phase C is scoped.

### B.9 David's known gaps, and where each is answered

| Gap                                                         | Where in Phase B                                                                                                                      |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Sentinel throughout the pipeline                            | B.2.7: Steps 14, 15 and 16 (P14.5, P15.2)                                                                                             |
| `secure-software-engineering` throughout                    | B.2.7: Step 14 (requirements, P14.4) and Step 15 (threat model, P15.2)                                                                |
| Anvil's own skills throughout                               | B.2.8: `data-models` at Steps 15 and 16 (P15.1, P16.2); the Material 3 documents at 12 and 14; the Anvil `AGENTS.md` template (P11.6) |
| The no-shared-database rule given to every skill            | B.2.5, the Anvil context pack, pasted at every invocation                                                                             |
| Step 11 reshaped for all entry points                       | B.1 (entry record, health check) and P11.1 to P11.5                                                                                   |
| Apps 2 to 5                                                 | B.1; P11.1 Route C; 07 and 08 through Step 11, Steps 12 to 16 not run for App 3; B.2.9 (ledger holds every app)                                |
| Learning through the memory governor and `mb-submit-memory` | B.2.11 (Phase B's part); Step 46 is Phase F's scope                                                                                   |

### B.10 Decisions for David

Each is a question of intent. The recommendation and its reason are given so that each can be answered with a yes or a no.

1. **Code repositories in GBrain** (B.2.2). Settled: no application code in GBrain; agents read app code directly from the app folder.
2. **Interview rounds** (B.2.6). Settled: the skill runs as designed, with every question it needs.
3. **Sentinel** (B.2.7). Settled: wherever security applies; in Phase B, every step (11, 12, 14, 15, 16).
4. **The ledger change** (B.2.9). Settled and applied, 2026-10-13.
5. **Where entries 07 and 08 join.** Settled in B.1: both join at Step 11; Steps 12 to 16 do not run for App 3.
6. **Where tickets live** (P11.3). Recommendation: GitHub Issues on the private project library.
7. **An `AGENTS.md` from Anvil's template in App 1's code repository** (P11.6). Recommendation: yes.
8. **`/office-hours` mode for the test application** (P12.4). Recommendation: builder mode for `mb5pdlf`, startup mode for every real business.
9. **A gate on concept or scope** (P14.7). Recommendation: one gate, `scope-approved`, at the end of Step 14; a recorded approval at Step 12.
10. **Who starts `/grill-with-docs`** (P16.6). Recommendation: the agent, with the policy on user-started skills made precise.

### B.11 What only a run on the test application can prove

These cannot be settled by reading. Each is checked on the first run of Phase B on `mb5pdlf`, and the answer is written into the step it concerns:

1. That the statement "a design doc already exists" stops `/plan-ceo-review` and `/plan-eng-review` from offering `/office-hours`.
2. That `/plan-ceo-review` honours "deferred to Step 15" without asking David (P14.1).
3. That `/plan-eng-review`'s complexity trigger accepts Step 14's settled scope (P15.4).
4. Whether `/plan-eng-review` finds a plan file to write into inside OpenCode; PDLF does not depend on it either way.
5. That `grilling` honours the three-question limit (B.2.6).
6. That `setup-matt-pocock-skills` accepts PDLF's locations and that `/grill-with-docs` then writes `CONTEXT.md` and `adr-local\adr-{name}.md` without per-run overrides (P11.3, P16.1).
7. That `mb-sentinel-review` writes its row at Steps 14 and 15 once its table and the ledger check are widened.
8. That the ISA's criteria sections generate correctly from the `isc` table.
9. That Cupcake blocks an attempt to pass `domain-locked` without David's approval (the Cupcake proof, build plan section 9).

### B.12 Order of work to make Phase B buildable

Proposal, in dependency order: (1) correct `spec-execution-discipline.md` and `spec-gate-procedure.md` (B.2.1); (2) the ledger change (B.2.9); (3) write `spec-skill-context-pack.md` (B.2.5); (4) the Sentinel table and check, if agreed (B.2.7); (5) bring the project template and the blank pre-project set to the four-repository scaffold, unnumbered (Step 11 findings 2 and 5); (6) correct `spec-nomenclature.md`'s Phase B names; (7) write each step's build-plan entry from this scope, David approving each, Step 11 first; (8) run Phase B on `mb5pdlf` (B.11); (9) only then compile the five modules.

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

## Files read for this version

Every file below was read in full, unless a note says otherwise.

**Phase B step files** (`app-factory/phase-b-discover-and-define/`): `b11-build-plan.md`, `b11-config.md`, `b11-reference.md`, `b11-explainer.md` (empty), `b11-module.md` (empty), `b11-decision-tree.html`; the same six files for `b12`, `b14`, `b15` and `b16`, including the copy of the `/plan-eng-review` skill source and manifest inside `b15-build-plan.md`; `b13-placeholder.md`.

**Phase A step files** (`app-factory/phase-a-init/`): `a01-build-plan.md` (the run plan), `a01-config.md`, `a01-reference.md`, `a01-explainer.md`, `a01-decision-tree.html`, `a01-module.md`; the build plans of `a02` to `a10` (each holds only the shared entry-point entry).

**PDLF system documents:** `app-factory/pdlf-build-plan.md`; `AGENTS.md`; `pdlf-library/pdlf-explainer-docs/pdlf-explainer.md`; `pdlf-library/pdlf-explainer-docs/app-factory-explainer.md`; `pdlf-library/docs-local/pdlf-todo.md`.

**PDLF specifications:** `spec-execution-discipline.md`, `spec-gate-procedure.md`, `spec-artifact-handover.md`, `spec-bft.md`, `spec-postgres-ledger.md`.

**PDLF policies:** `pol-anvil-platform.md`, `pol-skill-invocation.md`, `pol-memory-and-knowledge.md`, `pol-step-conditional-state.md`, `pol-testing-and-quality.md`.

**PDLF decisions and templates:** `adr-local/global-content-discovery-and-application-discipline.md`, `adr-local/project-library-global-registration.md`, `templates-local/isa-template-v2.md`, `templates-local/bft-checkpoint-cheatsheet-v2.md` (its closing notes).

**mybizz-os and its components:** `os-reference-docs/skills-catalog.md` (every installed skill and its description, and the section on skills not used); `mb-sentinel-review/sentinel-config.md` (its step-intensity table and ledger section); `mb-sentinel-review/sentinel-explainer.md` (the step-intensity table and the review cycle); `matt-pocock-skills/matt-pocock-skills-config.md` (the installed version pin); the documents supplied with the handover: the handover of 2026-10-12, overview V4, the scope list, the repository table, the memory master explainer and the mybizz-os explainer.

**`project-library-global`:** `specifications-global/spec-five-app-architecture-model.md`; `policy-global/pol-anvil-first-development.md`; `security-global/requirements/sec-requirements-architecture-review.md`; `security-global/requirements/sec-requirements-data-table-creation.md`; `security-global/threat-models/sec-multi-tenant-assumption-leakage.md`; `adr-global/adr-filename-and-frontmatter-numbering-policy.md` (its decision); `templates-global/tmp-authoritative-schema.md` (its structure); `specifications-global/spec-nomenclature.md` (its Phase B names); the folder listings of every section.

**Anvil's `anvil-agent-references`:** `AGENTS.md` (the template for app repositories); `skills/data-models/SKILL.md`; `skills/server-code/SKILL.md` (its rules); the list of its skills and documents.

**Matt Pocock skills** (the installed version `84fdeff` where it differs from the current one): `grilling`, `grill-me`, `grill-with-docs`, `domain-modeling` with its `ADR-FORMAT.md` and `GLOSSARY-FORMAT.md`, `setup-matt-pocock-skills` with its `domain.md`, `wizard`.

**Phase C to F:** read in overview V4 only, for what Phase B must hand over; not changed.
