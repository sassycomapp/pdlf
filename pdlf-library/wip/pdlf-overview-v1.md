---

title: "pdlf-overview"
updated: "2026-10-12"

doc-id: "mb-1f2514c9"
---

# PDLF Overview (work in progress)

Temporary working document. Built from the step files on 2026-10-12. Delete when the findings are dealt with.

## 1. Step by step

| Step | Name                             | Carried out by                                                                              | Gate                             | BFT         | State             |
| ---- | -------------------------------- | ------------------------------------------------------------------------------------------- | -------------------------------- | ----------- | ----------------- |
| a01  | Orchestrator                     | OpenCode, as the orchestrator. Designed in parts, alongside the steps it runs               |                                  |             | empty             |
| a02  | Entry points                     |                                                                                             |                                  |             | empty             |
| a03  | Entry points                     |                                                                                             |                                  |             | empty             |
| a04  | Entry points                     |                                                                                             |                                  |             | empty             |
| a05  | Entry points                     |                                                                                             |                                  |             | empty             |
| a06  | Entry points                     |                                                                                             |                                  |             | empty             |
| a07  | Entry points                     |                                                                                             |                                  |             | empty             |
| a08  | Entry points                     |                                                                                             |                                  |             | empty             |
| a09  | Entry points                     |                                                                                             |                                  |             | empty             |
| a10  | Entry points                     |                                                                                             |                                  |             | empty             |
| b11  | Init                             | OpenCode                                                                                    |                                  | Full        | designed, not run |
| b12  | Office hours                     | OpenCode, with GStack `/office-hours` if the developer chooses                              |                                  | Full        | designed, not run |
| b14  | CEO review                       | GStack `/plan-ceo-review`                                                                   |                                  | Full        | designed, not run |
| b15  | Engineering review               | GStack `/plan-eng-review`                                                                   |                                  | Full        | designed, not run |
| b16  | Domain modeling                  | Matt Pocock `/grill-with-docs`, which runs a `/grilling` interview using `/domain-modeling` | domain-locked                    | Full (gate) | designed, not run |
| c17  | Create Anvil data tables         | The developer, by hand in the Anvil editor                                                  |                                  | Light       | old draft         |
| c18  | Pull to local                    | The developer, by hand                                                                      |                                  | None        | old draft         |
| c19  | To tickets                       | Matt Pocock, using `to-tickets`                                                             |                                  | Full        | old draft         |
| c20  | Design consultation              | GStack, using `/design-consultation`                                                        |                                  | Full        | old draft         |
| c21  | Concept sanity audit             | OpenCode                                                                                    | concept-locked                   | Full        | old draft         |
| c22  | Wireframes, phase 1              | The Magdoub wireframe skill                                                                 |                                  | Full        | old draft         |
| c23  | Plan design review               | GStack, using `/plan-design-review`                                                         |                                  | Full        | old draft         |
| c24  | Plan developer-experience review | GStack, using `/plan-devex-review`                                                          |                                  | Full        | old draft         |
| c26  | Wireframes, phase 2              | The Magdoub wireframe skill                                                                 | wireframes-approved              | Full        | old draft         |
| c27  | Screen production                | OpenCode                                                                                    |                                  | Full        | old draft         |
| c28  | Screen to PNG                    | An external tool                                                                            |                                  | None        | old draft         |
| d29  | Build UI forms                   | The developer with Anvil's AI, by hand in the Anvil editor                                  |                                  | Light       | old draft         |
| d30  | Pull to local                    | The developer, by hand                                                                      |                                  | None        | old draft         |
| d31  | Scaffold planning                | OpenCode                                                                                    |                                  | Full        | old draft         |
| d32  | Physical scaffold build          | The developer, by hand in the Anvil editor                                                  |                                  | Light       | old draft         |
| d33  | Pull to local                    | The developer, by hand                                                                      |                                  | None        | old draft         |
| d34  | Architectural sanity audit       | OpenCode                                                                                    | architecture-verified            | Full        | old draft         |
| e35  | Build                            | OpenCode                                                                                    |                                  | Full        | old draft         |
| e35a | Testing                          | OpenCode                                                                                    |                                  | Light       | old draft         |
| e36  | Design review                    | GStack, using `/design-review`                                                              |                                  | Full        | old draft         |
| e37  | Code review                      | GStack, using `/review`                                                                     |                                  | Full        | old draft         |
| e38  | Quality testing                  | GStack, using `/qa`                                                                         |                                  | Full        | old draft         |
| e38a | Dependency check                 | OpenCode                                                                                    |                                  | None        | old draft         |
| e39  | Triage                           | Matt Pocock, using `triage`                                                                 | build-verified, for this feature | Full        | old draft         |
| e40  | Architecture scan                | Matt Pocock, using `improve-codebase-architecture`                                          |                                  | Light       | old draft         |
| e40b | Approved fixes                   | OpenCode                                                                                    |                                  | Light       | old draft         |
| f41  | Ship                             | GStack, using `/ship`                                                                       |                                  | Light       | old draft         |
| f42  | Publish to staging               | The developer, by hand                                                                      |                                  | None        | old draft         |
| f42a | Staging integration tests        | GStack and OpenCode                                                                         |                                  | Light       | old draft         |
| f43  | Staging smoke test               | GStack, using `/qa` or `/canary`                                                            |                                  | Full        | old draft         |
| f44  | Release                          | The developer, by hand                                                                      | production-released              | Full        | old draft         |
| f45  | Production check                 | GStack, using `/canary`                                                                     | released                         | Full        | old draft         |
| f46  | Learning                         | OpenCode                                                                                    | released                         | Full        | old draft         |

## 2. Requirements against steps

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
