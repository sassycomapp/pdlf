---
title: "b11-build-plan"
doc-id: "mb-4f446919"
updated: "2026-10-13"
---
# Step 11 — Init: Build Plan

## Step entry

### Phase B — Discover and Define

Ends with the gate `domain-locked` (Step 16).

#### Step 11: Init

**Must achieve:** a sound foundation for the business and the app being started: its folders and repositories exist and are linked to GitHub, its project library has the standard structure, it is registered in GBrain and covered by the commit tools, and its record is in the ledger, so that every later step can rely on all of it without checking again.

**Starts from:** the entry record from the orchestrator (build plan section 4); David's answers; the project template at `C:\dev\project-template\dev-(SLUG)\`; the blank pre-project files at `C:\pdlf\pdlf-library\templates-local\pre-project\`; the ledger; GBrain.

**Produces:** the business folder `C:\dev\dev-{slug}\` with `README.md`, the app folders `{slug}-app1`, `{slug}-app2`, `{slug}-app3`, `{slug}-app5`, the project library `{slug}-project-library` and `wip`; App 1 (or, for entries 07 and 08, App 3 or App 5) cloned from GitHub into its folder; the project library with its standard folders, its `pdlf-outputs\` step folders and `pdlf-tickets\`; for a new application, the three blank pre-project files in `pre-project\`; the Matt Pocock configuration in `docs\agents\`; the GBrain source `{slug}-project-library`; the `projects` row; the Step Receipt and BFT record in `pdlf-outputs\b11\`.

**Carried out by:** OpenCode. Two actions belong to David and are never done by the agent: creating each app in Anvil (which creates its code repository on GitHub), and every commit and push.

**Must be built so that:**
- it reads the entry record and runs one of three routes: **A**, a new business (entry 02); **B**, an application with context (entry 03); **C**, a new app in an existing business (entries 07 and 08);
- before anything is created, it runs the foundation checks: the ledger answers on port 5433 with its seven tables; GBrain answers and the sources `default` and `pdlf` are registered; the clone of Anvil's skills is present at `C:\mybizz\anvil-agent-references`; the skills Phase B uses are installed (`office-hours`, `plan-ceo-review`, `plan-eng-review`, `grilling`, `grill-with-docs`, `domain-modeling`, `setup-matt-pocock-skills`, `data-models`, `secure-software-engineering`, `mb-sentinel-review`, `wizard`); any failure stops the step with a deviation;
- the slug is the business's short name, all lowercase, with its hyphens kept;
- for a new business, the template is copied with `(SLUG)`, `(slug)`, `{slug}` and `{project-name}` replaced, and every `doc-id` line removed from the copied documents, so each project's documents get their own identity at their first commit;
- an app's code repository always comes from Anvil: David creates the app in his Anvil account and connects it to GitHub as `{slug}-app{n}`; the agent gives him exact numbered instructions made with the `wizard` skill, then removes the folder's placeholder and clones the repository into it; it checks the clone holds `anvil.yaml` and never writes to it;
- every app folder gets an `AGENTS.md` built from Anvil's own template (`C:\mybizz\anvil-agent-references\AGENTS.md`), with its resource paths pointed at that folder, and a `.gitignore` that keeps out `.env`, credentials, `__pycache__`, test output and development files, because everything committed is pushed to Anvil;
- the project library is created on GitHub as a private repository only with David's permission; David's refusal stops the step, because there is no project without it;
- the blank pre-project files are placed in `pre-project\` for a new application, and David is asked to fill them in;
- the Matt Pocock setup runs `setup-matt-pocock-skills` in the project library with PDLF's answers fixed in advance, so David only confirms: tickets are local markdown files in `pdlf-tickets\`; the five standard triage labels; single context, with the glossary at `docs-local\CONTEXT.md` and decisions in `adr-local\`; the skill never creates a `CLAUDE.md`;
- the project library is registered in GBrain as the federated source `{slug}-project-library`;
- the agent gives David the exact lines that add the project library to `mb-doc-check.sources` and to `commit-all.sh`, and the command that installs the commit hook; the step does not finish until David confirms, because otherwise the project's first commit bypasses the hook;
- for an application with context, nothing that exists is changed: only missing folders are created, broken links or registrations are corrected only with David's permission, David confirms each repository's data is sound, and an old name is reported, never renamed;
- for a new app in an existing business, the health check runs first, then only that app's part is done; the project library is not touched;
- the `projects` row records the slug, the business's name, the mode, the library path, the GBrain source and every app's path and Anvil address known so far;
- the security review `mb-sentinel-review` runs on the step's output at High scrutiny, because the app repositories are public and nothing secret may enter them; a Flag or Escalate stops the step; its `triage_findings` row is checked before the step finishes;
- the step ends with [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) as its self-audit: every failure is reported, nothing is fixed without David's permission;
- its ledger row is `step_type = 'skill'`, `skill_family = 'opencode'`, `run = 'app'`, with `app_number` the app worked on.

**BFT level:** Full, because Step 11 makes the structural decisions everything else stands on.

**References:** [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md), [[[default:specifications-global/spec-five-app-architecture-model|Five-App Architecture Model]]](C:/dev/project-library-global/specifications-global/spec-five-app-architecture-model.md), [[[pdlf:pdlf-library/specifications-local/spec-skill-context-pack|Spec: Skill Context Pack]]](C:/pdlf/pdlf-library/specifications-local/spec-skill-context-pack.md).

## Why it is built this way

- **Three routes, one end.** A new business, an existing one and a new app differ only in how their repositories are obtained and checked. The same closing health check proves each is sound, so every later step can rely on the same foundation.
- **Foundation checks first.** A missing tool found at Step 15 costs a half-finished review; found at Step 11 it costs nothing.
- **Anvil creates the code repository.** An Anvil app's repository must come from Anvil, or Anvil cannot synchronise with it.
- **The template is copied without document identities.** Otherwise every project would share the template's identities, and the commit hook would treat different projects' documents as one.
- **Tickets in the private library.** The app repositories are public; tickets describe internal plans.
- **Commit coverage confirmed before the end.** A project library outside the hook would be committed without identities, link repair or a GBrain update.
- **Nothing existing is changed.** An existing application's material is David's.
