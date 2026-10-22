---
title: "pdlf-todo"
doc-id: "mb-13a3fbc9"
updated: "2026-10-22"
---
# Active PDLF To-Do List

Action items only. Completed and closed items are not tracked here.

> **Review note (2026-10-08):** This list merges the earlier and the revised versions of this file into one, grouped by subject. It was written before many later decisions, so each item carries a note where a later system, method or decision has made part or all of it obsolete. Notes marked **Superseded** mean that part no longer applies. Notes marked **Changed since** mean the item still stands but must be re-planned against the newer setup. Items with no note are still current as written. This file is resolved in steps work.

---

## A. Rebuilding the steps

### A1. Rebuild Steps 17–46, one at a time

Steps 17–46 are audited and rebuilt one at a time as each phase is reached, with the same rigour as Steps 11/12/14/15/16.

> **Changed since:** This was previously listed as "deferred by explicit agreement, not tracked as an action item." It is the main PDLF task and is now an action item. Each step is rebuilt with the build rules in section B and ends with `/mb-close-out`.

---

## B. Rules for building every step

### B1. Global-content query-fetch-apply sequence

Rule and enforcement mechanism decided 2026-07-19 — see
[[[pdlf:pdlf-library/adr-local/global-content-discovery-and-application-discipline|ADR Global Content Discovery and Application Discipline]]](C:/pdlf/pdlf-library/adr-local/global-content-discovery-and-application-discipline.md) and
[[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Pol Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md). `project-library-global`'s GBrain registration is confirmed
working, so the mechanism is usable, not just designed. Remaining work: build the
five-step sequence and citation requirement into each relevant step file (17, 20, 22, 26,
27, 35, 35A, 37, 38, 41–45 at minimum) as that step is written or rebuilt. Deferred to
Phase C onward.

> **Changed since:** This is a rule for building each step, not a separate task; it is applied as part of A1. Since it was written, GBrain was upgraded to 0.59.18.0, every documentation repository became a federated source so one search covers everything, and cross-repository links now use the standard form `[[[source-id:slug]]](C:/full/path.md)`, written by agents as `[[name]]` and converted by the `mb-doc-check` commit hook. The five-step sequence must be checked against that setup before it is built into any step.

### B4. End-to-end proof of the governed memory pipeline

The final, real end-to-end proof that the governed memory pipeline works together in practice requires PDLF itself to be a real, running system before it can be tested. It was previously tracked in Deferred and Unresolved Matters, Entry 2.

> **Changed since:** The one-time live test still stands. Its natural setting is the first real step run on `mb5pdlf`, the test project for PDLF.

---

## C. Testing

### C2. Prove the test suite on `mb-5-pdlf`

`mb-5-pdlf` holds no application until the Daily Intentions Tracker is built through PDLF. When it is, Step 11 runs PR-09 to prove the local runtime, both Uplink connections, the `TEST_` users with second factors and the mail catcher; each later step then runs its test specification. Correct any test, template or tool that does not work as written before another application relies on it.

### C3. Apply the rule soundness register's source changes

Each entry of `project-library-global\test-suite\ts-rule-soundness-register.md` names a source document to correct. Each is corrected with the developer's approval and its entry removed. They include widening the ledger's `triage_findings.source_step` check (RS-11), and pointing `pol-testing-and-quality.md` and `spec-testing-methodology-standards.md` to the test suite (RS-02, RS-07, RS-08, RS-13).

---

## D. Code checking

### D1. Deterministic server-code dependency checker — hard gate

`GBrain`'s own symbol resolution only resolves same-file references by design — it cannot trace cross-file calls, the majority case in any real codebase. Decision already made: implement via `Graphify`, scoped to `server_code/` only (`client_code/` explicitly out of scope — Anvil's RPC/event-handler wiring is string-based and invisible to any static analyzer regardless). Build as a standing gate inside the existing `code-plan-build` workflow's "Mandatory checks before edits" step, authored once in PDLF so every future PDLF-managed project inherits it automatically. Not yet done: actual gate implementation and wiring into PDLF's step/gate definitions.

> **Changed since:** The developer has since stated doubt about Graphify's benefit, and the decision is deferred. He also takes the view that code sources should not be in GBrain. The "decision already made" above no longer stands as settled and must be reopened before any gate is built.

---

## E. Skills scoping (Pass 1)

### E1. Verify Pass 1 against the installed copies

Phases B and C were scoped from the issuers' published sources (GStack `c580561`, Matt Pocock `5beb35b`, Anvil `14b1967`, Magdoub wireframe at its GitHub head). Run the verification command from the Phase B session, compare the installed copies, the two Magnus919 skill files, the Anvil CLI and the GBrain results with Steps 01–46, and correct any step that does not match. Step 17 depends on the Anvil CLI (`anvil --json validate`) being installed.

### E2. Anvil's `$app-testing` skill

Anvil's `data-models` and `server-code` skills call `$app-testing`, and `anvil-yaml` calls `anvil db apply-schema --force`, to test against the agent's temporary database. `$app-testing` is not yet published in `anvil-agent-references`. When Anvil publishes it, it is assessed as a complement to the local runtime of the test suite, and examined whenever `anvil-agent-references` is updated.

### E3. Anvil CLI `watch` for the shared pull procedure

Step 18 holds the one pull procedure that Steps 30 and 33 use. Examine whether the Anvil CLI's two-way sync (`anvil watch`) replaces it, before the first build on the test application.

### E4. Delete Step 24's step files

Step 24 is not used and has `c24-placeholder.md`. Delete `c24-build-plan.md`, `c24-config.md`, `c24-reference.md`, `c24-explainer.md`, `c24-decision-tree.html` and `c24-module.md` from `C:\pdlf\app-factory\phase-c-design-and-plan\`.

### E5. Pass 3

Design the user help documentation and the video documentation. Testing is designed in the test suite (`project-library-global\test-suite\`).

### E7. Sort `mb-3-cs` decisions out of `project-library-global`

Decisions and specifications that apply to `mb-3-cs` alone (tiers, onboarding, payment gateway rules, the ClauseBuilder, the "Mybizz CS" screen and UI standards, the Vault build sequence) move to `mb-3-cs-project-library`; what applies to every Mybizz business, `mb-4-ecom` included, stays global. Done at Step 15 of the first `mb-3-cs` build, where Step 15 lists them.

### E8. Cloudflare R2

Each client has one or two R2 buckets of its own, in a Cloudflare account dedicated to it, and leaves with them on exit (`adr-client-r2-storage-and-exit-handover`). Cloudflare is registered Deferred in the skills catalog; document it with `mb-sysdoc-creator` before the first step that uses it, and confirm which S3-compatible library runs on Anvil's server Python.

### E6. Correct the release mechanism in the no-staging ADR

`adr-local/no-staging-environment-five-app-isolation.md` still names the `develop` → `stable` merge as the release. The release is the clone of App 1's tagged code into App 2 (Step 42). Correct the ADR's mechanism lines; its decision, no staging environment, stands.

---

## F. PDLF and its applications (`mb-3-cs`, `mb-4-ecom`)

### F1. Align both project libraries with the project template

`mb-3-cs-project-library` and `mb-4-ecom-project-library` were made before the project template. Bring each to the template's structure (`docs-local`, `adr-local`, `pdlf-outputs` with one folder per step, `pdlf-tickets`, `pre-project`, the Matt Pocock configuration in `docs\agents`) without changing any existing content. `mb-4-ecom` has `adr` and `docs` where the template has `adr-local` and `docs-local`. Done by Step 11, route B, when each application first enters PDLF; until then, nothing is moved.

### F2. Correct the stale `mb-3-cs` documents

These state things that are no longer true: `docs-local\CONTEXT.md` (folders under `C:\projects\`, the repository name `mb-3-cs`, the old to-do list, "currently 3 ADRs"); `docs-local\gstack-artifact-governance.md` (folders `gstack-outputs`, `docs`, `adr`, `wireframes`, which PDLF's step folders replace); `policy-local\development-policy.md` (VS Code with Continue.dev, the `master`/`dev` branching model); `docs-local\architecture.md` and `docs-local\INDEX.md` (the `develop` → `stable` release, `CONTEXT.md` described as empty). Correct each to the current setup, or retire it where PDLF replaces it.

### F3. Settle the `mb-3-cs` table count

`authoritative-schema.md` and App 1 have 44 tables; `adr-local\schema-scope-reduction.md` and `adr-local\blank-client-template.md` state 36; `architecture.md` states 43. The authoritative schema is the source of truth; correct the other documents to it, or record a decision where the count is meant to differ.

### F4. Settle the calendar's use of `HTMLTemplate`

`docs-local\calendar-feature-spec.md` builds the month grid with `HTMLTemplate`, which `adr-htmltemplate-use` bans. Redesign the month grid with M3 components, or record an approved deviation. Settled before the calendar's ticket reaches Step 22.

### F5. Add a schema migration log to the project template

Step 17 records every schema change in the project library's schema migration log, and Steps 41 and 42 read it. Add the log, empty, to `C:\dev\project-template\dev-(SLUG)\(slug)-project-library\docs-local\`, and to both existing project libraries.

### F6. A home for release specifications

`mb-3-cs` keeps its V2 and V3 specifications in folders `V2` and `V3`. Give release specifications one home in the project template (one folder per version under `docs-local\releases\`), so Step 04 and Step 19 always find a release's specification in the same place, and move V2 and V3 there.

### F7. Remove the source archives from `mb-4-ecom-project-library`

`docs\medusa-develop.zip` (61 MB) and `docs\rea-main.zip` (16 MB) are third-party source archives inside a documentation repository. Keep them outside the repository (for example in `C:\dev\dev-mb-4-ecom\wip`), and keep in the library only a note of where they are and what they are for, so the repository and GBrain hold documentation only. Step 12's `research` reads them from there.

### F8. Retire the Gemini report

`mb-4-ecom-project-library\docs\mb-4-ecom-architecture-report.md` replaces `docs\report from discussion with gemini.md`, whose statements on multi-tenancy, self-creating tables, PgBouncer and a central R2 account do not apply. Delete `docs\report from discussion with gemini.md` and the copy in `mb-3-cs-project-library\docs-local\See what can be used from this report.md`. The original transcript, `docs\important discussion with Gemini.md`, stays as source material.
