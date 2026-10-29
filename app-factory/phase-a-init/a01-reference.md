---
title: "a01-reference"
doc-id: "mb-a0973e59"
updated: "2026-10-29"
---
# Step 1 — Orchestrator: Reference

What the orchestrator does, in order. Agent-facing. Fixed values: [[[pdlf:app-factory/phase-a-init/a01-config|Step 1 Configuration]]](C:/pdlf/app-factory/phase-a-init/a01-config.md). Every step it runs follows [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md); every gate follows [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md). The ledger is read and written through the PowerShell bridge of [[[pdlf:pdlf-library/specifications-local/spec-postgres-ledger|Spec: Postgres Ledger]]](C:/pdlf/pdlf-library/specifications-local/spec-postgres-ledger.md).

## 1. Start

1. Check the working folder is a business folder, `/mnt/c/dev/dev-{slug}`, and take the slug from its name. If it is not: stop, and ask David to open OpenCode in the business folder and run `/pdlf-init` again.
2. Check the ledger answers. If it does not: stop and raise a deviation.

## 2. The resume check

3. Read the `projects` row of the slug. If there is none, the business has no runs: continue at item 6.
4. Read every entry-point row of the business (`step_number` `02` to `10`) and every `steps` row of each of their runs. Place each run in the resume check of the configuration: unfinished, paused or finished.
5. Present every unfinished run, with the step it would continue at, and every paused run, with the step it waits at and the phase that is not built. Ask David to choose an unfinished run to continue, or to take a new entry point. To continue: go to item 14 with that run's step. For a new entry point: continue at item 6.

## 3. Taking an entry

6. Present the entry points of the configuration. David chooses exactly one.
7. For entries 04 to 10: check the `projects` row exists, then run [[[pdlf:pdlf-library/operating-procedures/sop-health-check|SOP: Health Check]]](C:/pdlf/pdlf-library/operating-procedures/sop-health-check.md) on the business before anything else, and save its report under the name in the configuration (test PR-02). If any check fails: stop, and present each failure as a deviation.
8. Carry out that entry point's reference, `a{nn}-reference.md`, in full, with its configuration: its questions to David and the actions only it takes.
9. For a feature or an update: check its slug is lowercase letters, digits and hyphens, is never `app{n}`, and is not the `run` of any `steps` row of the business. If any check fails: ask David for another slug.
10. For entries 02 and 03: if a `projects` row exists for the slug, stop and raise a deviation: the business is already in PDLF. Otherwise write the `projects` row with the slug, the name and the mode.
11. Write the entry point's `steps` row with the ledger values of the configuration, holding the entry record in `inputs_used` (test PR-01), and its Light BFT record.
12. For entries 04 to 10: record the entry's tests in its checks file and write its Step Receipt, under the names in the configuration. For entries 02 and 03, Step 11 writes them.
13. Explain what the entry decided and why, present the Step Receipt, stop, and ask David to run `/mb-close-out`. On "continue": go to item 14 with the entry record's `start_step`.

## 4. Running the run

14. Take the step. If its phase is not built: report that the run is paused at this step until the phase is built, and stop.
15. Check its dependencies in the configuration are `complete` or `skipped`, and every gate before it in the route is passed for the run (test PR-01). If one is not: stop and raise a deviation.
16. Read the step's configuration, reference and test specification in its phase folder, or its module once it is written. Carry out its reference under the execution discipline, from substep 0, which opens the step's row.
17. When the step has ended and David says "continue": if the route has a next step, go to item 14 with it. Otherwise the run is finished: say so, and stop.

## 5. At a gate

18. When a step's reference reaches its gate, after its gate summary and David's yes: give David the command of the configuration for the gate, with the slug and the run, and wait until he confirms it ran. Never run it, and never write to the `gates` table.
19. Read the `gates` row for the gate and the run. If it is not there and passed: tell David and stop. Otherwise the step continues past its gate (test PR-03).
