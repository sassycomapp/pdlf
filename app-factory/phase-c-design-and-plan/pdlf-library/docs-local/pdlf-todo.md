---
title: "pdlf-todo"
doc-id: "mb-a879931e"
updated: "2026-10-20"
---
# Active PDLF To-Do List

Action items only. Completed and closed items are not tracked here.

> **Review note (2026-10-08):** This list merges the earlier and the revised versions of this file into one, grouped by subject. It was written before many later decisions, so each item carries a note where a later system, method or decision has made part or all of it obsolete. Notes marked **Superseded** mean that part no longer applies. Notes marked **Changed since** mean the item still stands but must be re-planned against the newer setup. Items with no note are still current as written. This file is resolved in steps work.

---

## A. Rebuilding the steps

### A1. Rebuild Steps 17–46, one at a time

Steps 17–46 (excluding 42/42A/43/44, see A2) are audited and rebuilt one at a time as each phase is reached, with the same rigour as Steps 11/12/14/15/16.

> **Changed since:** This was previously listed as "deferred by explicit agreement, not tracked as an action item." It is the main PDLF task and is now an action item. Each step is rebuilt with the build rules in section B and ends with `/mb-close-out`.

### A2. Rebuild Steps 42, 42A, 43, 44

Held in the build plans of Steps 42, 42A, 43 and 44.

---

## B. Rules for building every step

### B1. Global-content query-fetch-apply sequence

Rule and enforcement mechanism decided 2026-07-19 — see
[[[pdlf:pdlf-library/adr-local/global-content-discovery-and-application-discipline|ADR Global Content Discovery and Application Discipline]]](C:/pdlf/pdlf-library/adr-local/global-content-discovery-and-application-discipline.md) and
[[[pdlf:pdlf-library/policy-local/pol-memory-and-knowledge|Pol Memory and Knowledge]]](C:/pdlf/pdlf-library/policy-local/pol-memory-and-knowledge.md). `project-library-global`'s GBrain registration is confirmed
working, so the mechanism is usable, not just designed. Remaining work: build the
five-step sequence and citation requirement into each relevant step file (17, 20, 22, 26,
27, 35, 35A, 37, 38, 41–45 at minimum) as that step is written or rebuilt. Deferred to
Phase C onward, same treatment as A2.

> **Changed since:** This is a rule for building each step, not a separate task; it is applied as part of A1. Since it was written, GBrain was upgraded to 0.59.18.0, every documentation repository became a federated source so one search covers everything, and cross-repository links now use the standard form `[[[source-id:slug]]](C:/full/path.md)`, written by agents as `[[name]]` and converted by the `mb-doc-check` commit hook. The five-step sequence must be checked against that setup before it is built into any step.

### B4. End-to-end proof of the governed memory pipeline

The final, real end-to-end proof that the governed memory pipeline works together in practice requires PDLF itself to be a real, running system before it can be tested. It was previously tracked in Deferred and Unresolved Matters, Entry 2.

> **Changed since:** The one-time live test still stands. Its natural setting is the first real step run on `mb5pdlf`, the test project for PDLF.

---

## C. Testing

### C1. Integrate Suite A and Suite B into Steps 35A, 36, 37, 38, 39, and relook the testing suite

Held in the build plans of Steps 35A, 36, 37, 38 and 39.

---

## D. Code checking

### D1. Deterministic server-code dependency checker — hard gate

`GBrain`'s own symbol resolution only resolves same-file references by design — it cannot trace cross-file calls, the majority case in any real codebase. Decision already made: implement via `Graphify`, scoped to `server_code/` only (`client_code/` explicitly out of scope — Anvil's RPC/event-handler wiring is string-based and invisible to any static analyzer regardless). Build as a standing gate inside the existing `code-plan-build` workflow's "Mandatory checks before edits" step, authored once in PDLF so every future PDLF-managed project inherits it automatically. Not yet done: actual gate implementation and wiring into PDLF's step/gate definitions.

> **Changed since:** The developer has since stated doubt about Graphify's benefit, and the decision is deferred. He also takes the view that code sources should not be in GBrain. The "decision already made" above no longer stands as settled and must be reopened before any gate is built.

---

## E. Skills scoping (Pass 1)

### E1. Verify Phases B and C against the installed copies

Phases B and C were scoped from the issuers' published sources (GStack `c580561`, Matt Pocock `5beb35b`, Anvil `14b1967`, Magdoub wireframe at its GitHub head). Run the verification command from the Phase B session, compare the installed copies, the two Magnus919 skill files, the Anvil CLI and the GBrain results with Steps 11–28, and correct any step that does not match. Step 17 depends on the Anvil CLI (`anvil --json validate`) being installed.

### E2. Anvil's `$app-testing` skill

Anvil's `data-models` and `server-code` skills call `$app-testing`, and `anvil-yaml` calls `anvil db apply-schema --force`, to test against the agent's temporary database. `$app-testing` is not yet published in `anvil-agent-references`. It is the candidate standard for PDLF's testing; it is examined in Pass 3 and whenever `anvil-agent-references` is updated.

### E3. Anvil CLI `watch` for the shared pull procedure

Step 18 holds the one pull procedure that Steps 30 and 33 use. Examine whether the Anvil CLI's two-way sync (`anvil watch`) replaces it, when Phase D is scoped.

### E4. Delete Step 24's set of six

Step 24 is not used and has `c24-placeholder.md`. Delete `c24-build-plan.md`, `c24-config.md`, `c24-reference.md`, `c24-explainer.md`, `c24-decision-tree.html` and `c24-module.md` from `C:\pdlf\app-factory\phase-c-design-and-plan\`.

### E5. Pass 1, Phases D to F, then Phase A

Scope each phase by the skills scoping strategy, in the order D, E, F, then A.
