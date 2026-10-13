---
title: "pdlf-todo"
doc-id: "mb-13a3fbc9"
updated: "2026-10-13"
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
[[[pdlf:pdlf-library/policy-local/global-content-discovery-and-application-discipline|ADR Global Content Discovery and Application Discipline]]](C:/pdlf/pdlf-library/policy-local/global-content-discovery-and-application-discipline.md) and
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
