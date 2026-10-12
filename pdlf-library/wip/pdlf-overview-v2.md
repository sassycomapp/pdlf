---
title: "pdlf-overview"
updated: "2026-10-12"
doc-id: "mb-ef907ca9"
---
# PDLF Overview (work in progress)

Temporary working document. Built from the step files on 2026-10-12. Delete when the findings are dealt with.

## 1. Step by step

| Step | Name | Carried out by | Gate | BFT | State |
|---|---|---|---|---|---|
| a01 | Orchestrator | OpenCode, as the orchestrator. Designed in parts, alongside the steps it runs |  |  | empty |
| a02 | Entry points |  |  |  | empty |
| a03 | Entry points |  |  |  | empty |
| a04 | Entry points |  |  |  | empty |
| a05 | Entry points |  |  |  | empty |
| a06 | Entry points |  |  |  | empty |
| a07 | Entry points |  |  |  | empty |
| a08 | Entry points |  |  |  | empty |
| a09 | Entry points |  |  |  | empty |
| a10 | Entry points |  |  |  | empty |
| b11 | Init | OpenCode |  | Full | designed, not run |
| b12 | Office hours | OpenCode, with GStack `/office-hours` if the developer chooses |  | Full | designed, not run |
| b14 | CEO review | GStack `/plan-ceo-review` |  | Full | designed, not run |
| b15 | Engineering review | GStack `/plan-eng-review` |  | Full | designed, not run |
| b16 | Domain modeling | Matt Pocock `/grill-with-docs`, which runs a `/grilling` interview using `/domain-modeling` | domain-locked | Full (gate) | designed, not run |
| c17 | Create Anvil data tables | The developer, by hand in the Anvil editor |  | Light | drafted (valuable, needs updating) |
| c18 | Pull to local | The developer, by hand |  | None | drafted (valuable, needs updating) |
| c19 | To tickets | Matt Pocock, using `to-tickets` |  | Full | drafted (valuable, needs updating) |
| c20 | Design consultation | GStack, using `/design-consultation` |  | Full | drafted (valuable, needs updating) |
| c21 | Concept sanity audit | OpenCode | concept-locked | Full | drafted (valuable, needs updating) |
| c22 | Wireframes, phase 1 | The Magdoub wireframe skill |  | Full | drafted (valuable, needs updating) |
| c23 | Plan design review | GStack, using `/plan-design-review` |  | Full | drafted (valuable, needs updating) |
| c24 | Plan developer-experience review | GStack, using `/plan-devex-review` |  | Full | drafted (valuable, needs updating) |
| c26 | Wireframes, phase 2 | The Magdoub wireframe skill | wireframes-approved | Full | drafted (valuable, needs updating) |
| c27 | Screen production | OpenCode |  | Full | drafted (valuable, needs updating) |
| c28 | Screen to PNG | An external tool |  | None | drafted (valuable, needs updating) |
| d29 | Build UI forms | The developer with Anvil's AI, by hand in the Anvil editor |  | Light | drafted (valuable, needs updating) |
| d30 | Pull to local | The developer, by hand |  | None | drafted (valuable, needs updating) |
| d31 | Scaffold planning | OpenCode |  | Full | drafted (valuable, needs updating) |
| d32 | Physical scaffold build | The developer, by hand in the Anvil editor |  | Light | drafted (valuable, needs updating) |
| d33 | Pull to local | The developer, by hand |  | None | drafted (valuable, needs updating) |
| d34 | Architectural sanity audit | OpenCode | architecture-verified | Full | drafted (valuable, needs updating) |
| e35 | Build | OpenCode |  | Full | drafted (valuable, needs updating) |
| e35a | Testing | OpenCode |  | Light | drafted (valuable, needs updating) |
| e36 | Design review | GStack, using `/design-review` |  | Full | drafted (valuable, needs updating) |
| e37 | Code review | GStack, using `/review` |  | Full | drafted (valuable, needs updating) |
| e38 | Quality testing | GStack, using `/qa` |  | Full | drafted (valuable, needs updating) |
| e38a | Dependency check | OpenCode |  | None | drafted (valuable, needs updating) |
| e39 | Triage | Matt Pocock, using `triage` | build-verified, for this feature | Full | drafted (valuable, needs updating) |
| e40 | Architecture scan | Matt Pocock, using `improve-codebase-architecture` |  | Light | drafted (valuable, needs updating) |
| e40b | Approved fixes | OpenCode |  | Light | drafted (valuable, needs updating) |
| f41 | Ship | GStack, using `/ship` |  | Light | drafted (valuable, needs updating) |
| f42 | Publish to staging | The developer, by hand |  | None | drafted (valuable, needs updating) |
| f42a | Staging integration tests | GStack and OpenCode |  | Light | drafted (valuable, needs updating) |
| f43 | Staging smoke test | GStack, using `/qa` or `/canary` |  | Full | drafted (valuable, needs updating) |
| f44 | Release | The developer, by hand | production-released | Full | drafted (valuable, needs updating) |
| f45 | Production check | GStack, using `/canary` | released | Full | drafted (valuable, needs updating) |
| f46 | Learning | OpenCode | released | Full | drafted (valuable, needs updating) |

## 2. Requirements against steps

Which steps mention each requirement of the system build plan. A mention is not always a design: several mentions are only recommendations copied in from the Phase B review.

| Requirement | Steps that mention it |
|---|---|
| Orchestrator designed | a01 (empty) |
| Entry points 02 to 10 | none (all empty) |
| Health check for existing apps | none |
| App 1 built (development workspace) | b11 to f46 |
| App 2 release by cloning App 1 | none (f44 still describes staging to production) |
| App 3 blank client template | none |
| App 4 first client and provisioning procedure | none |
| App 5 management app | none |
| No multi-tenancy given to every skill | none |
| Anvil skills (anvil-agent-references) | none |
| Anvil data-models skill | recommended for b15, b16, c17, d29, d32; not designed in |
| Sentinel security review | designed in b16 only; recommended for b14, b15 |
| secure-software-engineering skill | recommended for b14, b15; not designed in |
| Material 3 design standard | b11, b12, b14, b15, b16, c20 (mostly as recommendations) |
| Three-level testing per feature | e35 only |
| Gates | b16, c21, c26, d34, e39, f44, f46 |
| Step outputs to pdlf-outputs folders | none (rule set today, steps not yet updated) |
| Learning into the right source; lessons through mb-submit-memory | b11 to b16 (old wording); not in f46 |
| Close-out by /mb-close-out, agent never commits | b11 to b16 only |
| Old material still to remove (makePDLF paths, devlog, end-of-step housekeeping) | 46 steps carry makePDLF paths; 38 carry devlog and housekeeping |

## 3. What the drafted steps already settle (keep)

Read from each step's reference and build plan. These are working design decisions, not just placeholders.

| Step | Design already settled | Out of date |
|---|---|---|
| c17 | Developer builds tables in the Anvil editor from the Step 16 ADRs and Step 15 schema | Input "Step 15 TDD cluster" (Step 15 never produces it) |
| c18, d30, d33 | Pull to local after each Anvil-editor step, so later steps see the real schema, forms and stubs | Three copies of one procedure |
| c19 | `to-tickets` turns the locked plan into a dependency graph of tickets, one ticket per feature cycle; sole input to the build loop; tracker resolved, never hard-coded | Refers to the retired Step 3 disposition table |
| c20 | `/design-consultation` builds DESIGN.md, preview page and design tokens; abbreviable in test mode | — |
| c21 | Concept audit across all earlier outputs; hard scope freeze; gate `concept-locked` | Inputs name Step 13 and old output folders |
| c22, c26 | Magdoub wireframes: five black-and-white options, then clean and polished variants; gate `wireframes-approved` | Paths of the skill's persistent context files |
| c23, c24 | Design review (0 to 10 ratings) and developer-experience review appended to the plan | Value of 24 for an Anvil app to be checked |
| c27, c28 | Screen production and PNG conversion, with fidelity and standards checklists | Marked deferred / out of scope |
| d29 | Developer with Anvil's AI builds the UI forms from the approved screens | — |
| d31, d32 | Scaffold plan (modules and functions as empty stubs), then built by hand in Anvil | Input "TDD cluster" |
| d34 | Architecture audit: tables, forms and stubs against the locked architecture; gate `architecture-verified` | Input "TDD cluster" |
| e35 | Feature-by-feature loop, one ledger row per feature; three-level testing with backups before and after integration; signoff = known-good baseline | — |
| e35a, e38a | Two-sided dependency scan: local tools (35A, `pip-audit`) and Anvil's own scan recorded (38A) (ADR-0011) | — |
| e40, e40b | Optional read-only architecture scan; fixes only for findings David approves; grilling routed to a deviation request | — |
| e36, e37, e38 | Visual review after fixes (ADR-0007), code review, QA with regression tests; findings files mandatory even on a clean pass (ADR-0009) | Findings path `pdlf/outputs/` (now `pdlf-outputs/`) |
| e39 | Triage into ledger rows; gate `build-verified` per feature, placed after retest; fail returns to the failed step | — |
| f41 | `/ship` narrowed for Anvil: tests, version, changelog, push | — |
| f42a | Whole-application integration test before release (closes the smoke-test gap) | Written against a staging environment |
| f42, f43, f44 | Publish, smoke test, promote; rollback by re-pointing, not reverting | Staging/production model; to become the App 1 to App 2 clone release |
| f45 | Post-release canary monitoring | Production URL model |
| f46 | Retrospective, learnings, ISA update; gate `released` | Registry (retired); lessons not routed through `mb-submit-memory` |
