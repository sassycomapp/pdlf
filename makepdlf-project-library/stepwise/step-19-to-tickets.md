---
title: "step-19-to-tickets"
doc-id: "mb-c3656148"
updated: "2026-10-09"
---
## Task Execution Order

1. Run Matt `to-tickets` against the locked plan (Steps 14–16 output) and current
   CONTEXT.md.
2. If existing-project entry: scope to work genuinely outstanding per Step 3's
   disposition table only — not a full re-breakdown of the whole application.
3. → Decision point: present the ticket breakdown for developer approval before writing
   to the tracker.
4. Write tickets to the location resolved via the `### Issue tracker` block in
   `CLAUDE.md`/`AGENTS.md` — never a hardcoded path.
5. Follow execution sequence in [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md).
6. Apply BFT per [[[pdlf:makepdlf-project-library/specifications-local/spec-bft]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md) at assigned level.

---

## Description

Decomposes the locked plan into a dependency graph of tickets — either ordinary
vertical-slice features or, for a wide mechanical refactor, an expand-migrate-contract
sequence. Each ticket corresponds to one feature cycle in Step 35's build loop. This is
the sole producer of Step 35's input; no other step feeds it.

## Inputs Required

- Locked plan from Steps 14–16 (CEO review, Eng review, domain model + ADRs)
- CONTEXT.md (domain vocabulary)
- For existing-project entry: Step 3's disposition table, to scope to outstanding work only

## Outputs

- Tickets written to the configured issue tracker (per `docs/agents/issue-tracker.md`)
- Each ticket scoped to one feature/package (auth, blog, CRM, etc.)

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 19 | Skill | | Matt `to-tickets` |

---

## Handoff to Step 20

Step 20 ([[[pdlf:makepdlf-project-library/stepwise/step-20-design-consultation|/design-consultation]]](C:/pdlf/makepdlf-project-library/stepwise/step-20-design-consultation.md)) does not consume this step's output directly — it
proceeds independently from the locked plan. Step 19's tickets are read only by Step 35,
which begins after the architecture-verified gate (Step 34).

---

## Reference

Skill path: `~/.agents/skills/to-tickets/SKILL.md`

`to-tickets` never hardcodes the tracker path — it resolves it through the
`### Issue tracker` block that `/setup-matt-pocock-skills` writes into `CLAUDE.md`/
AGENTS.md. If a tracker cannot be resolved, this is a deviation, not a silent fallback.

OpenCode is always the orchestrator. Invoke skills only when they beat OpenCode directly.

For execution sequence: [[[pdlf:makepdlf-project-library/specifications-local/spec-execution-discipline]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:makepdlf-project-library/specifications-local/spec-bft]]](C:/pdlf/makepdlf-project-library/specifications-local/spec-bft.md)

GBrain is queried automatically at substep 1. Syncing is asked at substep 10, never auto-run.
The two housekeeping questions are asked separately, every step, never combined, never auto-run.

The ledger row, Step Receipt, and devlog-index/judgement-trail are the complete checkpoint.
No separate state file, devlog file, or completion report.
