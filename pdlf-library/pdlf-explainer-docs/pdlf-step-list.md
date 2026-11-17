---
title: "pdlf-step-list"
doc-id: "mb-7c3e91b5"
updated: "2026-11-17"
---
# PDLF — Step List

Every phase and step of PDLF, with what each step is principally about. Each step's own explainer, in `C:\pdlf\app-factory\`, gives the full detail.

## Phase A — Init

| Step | Name | What it does |
|---|---|---|
| 1 | Orchestrator | Finds where a business's work stands, starts or resumes a run, and runs its steps one at a time |
| 2 | New application, no context | Enters a new business that has no earlier material |
| 3 | New application with context | Enters a business that already has material but has never run through PDLF |
| 4 | Feature for App 1 | Enters a new feature for App 1 |
| 5 | Update to App 1 | Enters a change or a correction to App 1 |
| 6 | Release into App 2 | Enters a release of App 1's approved code into App 2 |
| 7 | Create App 3 | Enters App 3, the client app every client instance runs |
| 8 | Create App 5 | Enters App 5, the management app |
| 9 | Feature for App 3 or App 5 | Enters a new feature for App 3 or App 5 |
| 10 | Update to App 3 or App 5 | Enters a change or a correction to App 3 or App 5 |

## Phase B — Discover and Define

| Step | Name | What it does |
|---|---|---|
| 11 | Init | Sets up the business's folders, repositories, project library and tools |
| 12 | Office hours | Writes the design doc: what is built, for whom and why |
| 14 | CEO review | Settles how far the scope goes, and the data, law and exit that follow from it |
| 15 | Engineering review | Turns the scope into an architecture and writes the test plan, access matrix and threat model |
| 16 | Domain modeling | Writes the glossary and locks the data design; closes Phase B |

## Phase C — Design and Plan

| Step | Name | What it does |
|---|---|---|
| 17 | Create Anvil data tables | Applies the authoritative schema to the app's tables in Anvil |
| 18 | Pull to local | Brings the local copy of the app level with Anvil |
| 19 | Tickets | Breaks the plan into feature tickets, in build order |
| 20 | Design system | Writes `DESIGN.md`, the app's one design |
| 21 | Concept check | Checks the concept documents against each other; locks the concept |
| 22 | Screen requirements | Writes the full design of every form, in words and tables |
| 23 | Design review | Reviews every screen requirement and `DESIGN.md`, and records the findings |
| 26 | Screens approved | Corrects the screen requirements and locks them; closes Phase C |

## Phase D — Scaffold and Assemble

| Step | Name | What it does |
|---|---|---|
| 31 | Scaffold plan | Plans every module and function of the app before any code is written |
| 32 | Create the scaffold | Creates every planned module and function as an empty stub |
| 33 | Pull to local | Brings the local copy of the app level with Anvil after the scaffold |
| 34 | Architecture audit | Checks the skeleton against every locked decision; closes Phase D |

## Phase E — Build and Verify

Steps 35 to 40B run once for every feature ticket.

| Step | Name | What it does |
|---|---|---|
| 35 | Build | Builds one feature from its ticket and proves it works |
| 35A | Testing | Tests the feature more widely, and checks the packages it brings in |
| 36 | Design review | Checks the feature's forms against the approved designs |
| 37 | Code review | Reviews everything the feature changed |
| 38 | Quality testing | Tests the feature as users use it, checks nothing earlier broke, measures speed |
| 38A | Package check | Records Anvil's security check of changed server packages |
| 39 | Triage | Decides every finding and locks the feature |
| 40 | Architecture scan | Optional scan for places where the code's structure could be cleaner |
| 40B | Approved fixes | Applies only the architecture fixes David approved |

## Phase F — Ship and Monitor

| Step | Name | What it does |
|---|---|---|
| 41 | Release readiness | Proves the app is ready to release |
| 42 | Release to App 2 | Builds the release image and puts it on the test client instance |
| 42A | Release regression | Tests every feature of the release on the test client instance |
| 43 | Client instance check | Proves the test client instance is healthy on the release |
| 44 | Release | David decides to release, and the release is carried out |
| 45 | Production check | Watches the released app in real use and finishes the security checks |
| 46 | Learning | Puts each lesson of the build where the next build reads it; closes the cycle |

Steps 13, 24, 25, 27, 28, 29 and 30 are not used.
