---
title: "pdlf-overview-v3"
updated: "2026-10-12"
doc-id: "mb-eed680e4"
---
# PDLF Overview, V3 (work in progress)

Temporary working document in `pdlf-library/wip/`. It sets out what PDLF's steps are planned to do, phase by phase, so that gaps and surplus can be judged. Delete when the findings are dealt with.

## The whole journey, as currently planned

An application goes through PDLF in six movements:

1. **Phase B (Steps 11 to 16): define what the application is.** Set it up, write down the idea, challenge its ambition and its engineering, then fix its vocabulary.
2. **Phase C (Steps 17 to 28): design it.** Build the data tables, break the plan into feature tickets, create the design system and wireframes, and freeze the concept and the visual direction.
3. **Phase D (Steps 29 to 34): build its skeleton in Anvil.** Forms, then empty code stubs, then a check that the skeleton matches the architecture.
4. **Phase E (Steps 35 to 40B): build it one feature at a time.** Each feature is built, tested, reviewed and signed off before the next begins.
5. **Phase F (Steps 41 to 46): release and learn.** Release, test the whole application, check it after release, and capture lessons.
6. **Seven gates along the way stop PDLF until David approves:** domain locked (16), concept locked (21), wireframes approved (26), architecture verified (34), build verified for each feature (39), released to production (44), and released (46).

Phase A (Steps 1 to 10, the orchestrator and the entry points) is not yet designed.

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

To be written.

## Phase D in detail: building the skeleton in Anvil

To be written.

## Phase E in detail: building feature by feature

To be written.

## Phase F in detail: release and learning

To be written.

## Phase A: the orchestrator and the entry points

To be written.

## Appendix: requirements against steps

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

