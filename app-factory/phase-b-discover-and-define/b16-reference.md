---
title: "b16-reference"
doc-id: "mb-741c244a"
updated: "2026-10-13"
---

## From `16-domain-modeling.md`

## Task Execution Order

1. Query GBrain for context relevant to domain terminology and prior
   decisions (automatic, read-only), across the federated documentation sources:
   `{slug}-project-library`, `default` (`project-library-global`) and `pdlf`, plus
   `anvil-agent-references-code` for Anvil knowledge. Application code is read directly
   from the app folder.
2. Assemble context to paste into the invocation:
   - Step 15's plan artifact (`output-gstack\makepdlf-step-15-eng-plan.md` and/or the
     GStack-native file, per Step 15's own mode-dependent persistence)
   - Step 15's Test Plan Artifact
   - **Existing-project entry only:** existing `CONTEXT.md` and `adr-local\`
     contents, if present, plus current code — explicitly flagged as prior
     material, not fresh material
3. Invoke `/grill-with-docs`, pasting all of item 2 in full text. State the
   file destinations explicitly at invocation (see § File Placement) —
   `/grill-with-docs` defaults to `CONTEXT.md` + `docs/adr/` at repo root;
   PDLF overrides both locations rather than accepting the default.
4. `/grill-with-docs` runs `/grilling` (walks the plan as a tree of
   decisions, resolving one at a time, recommended answer given, waits for
   developer response before continuing) using [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md)'s
   disciplines inline: challenge terms against the existing glossary,
   sharpen vague/overloaded terms, stress-test relationships with concrete
   scenarios, and — **existing-project entry only** — cross-reference stated
   behavior against the actual code, surfacing contradictions as they're
   found. This cross-reference discipline is idle for new-project entry,
   since no code exists yet at this point in the pipeline; no separate
   reconciliation procedure is needed for that reason.
5. `CONTEXT.md` is updated inline as each term resolves — not batched.
   Glossary only; no implementation detail.
6. ADRs are offered only when a decision clears all three of: hard to
   reverse, surprising without context, result of a real trade-off. Most
   decisions from Step 15's review will not clear this bar — do not expect
   or require one ADR per decision.
7. Invoke the `mb-sentinel-review` skill, step number 16. Reviews the
   domain entities and terms just defined in `CONTEXT.md` (and any ADRs
   offered at item 6) against this step's own security question: are any
   sensitive data or security-relevant entities being created? On
   `CLEAR`: continue to item 8. On `FLAG` or `ESCALATE`: STOP. The
   finding is presented to the developer here, before the gate — it is
   part of what the developer is approving at `domain-locked`, not
   something discovered afterward. Do not proceed to item 8 with an open
   `FLAG` or `ESCALATE` still unresolved.
8. Verify `CONTEXT.md` exists at
   `dev-{slug}\{slug}-project-library\CONTEXT.md` and any ADRs exist at
   `dev-{slug}\{slug}-project-library\adr-local\000N-{slug}.md`. If missing
   when expected: STOP, present a deviation request per
   `[[spec-execution-discipline]]`.
9. Confirm a real row exists in `triage_findings` for this step's
   `step_id`, with `triage_label` in `('clear','needs-triage','needs-info')`
   — proof `mb-sentinel-review` genuinely ran at item 7, not merely that
   item 7's instruction exists in this file. No row: STOP, present a
   deviation request per `[[spec-execution-discipline]]`
   — the gate does not proceed on the assumption Sentinel was run.
10. → **GATE:** Execute gate procedure per `[[spec-gate-procedure]]`.
11. → **GATE:** `domain-locked` — developer approval required to proceed
    beyond Phase B. Full BFT override applies regardless of this step's
    assigned level.
12. Write Step 16 `steps` ledger row: `step_number = 16`, `type = 'SKILL'`,
    `status = 'complete'`, `synthesized = false`, `artifact_path` =
    `CONTEXT.md`'s path.
13. Save Step Receipt to `dev-{slug}\{slug}-project-library\pdlf\step-16-receipt.md`.
14. Present the gate summary block. Stop, wait for explicit developer approval
    (yes/no).
15. If approved: write the gate row and the ledger row with a gate-approval timestamp.
    Explain what was done and why, stop, and ask the developer to run `/mb-close-out`.
    Continue to Step 17.
16. If not approved: gate blocked, agent stops, records the blocker. Pipeline does not
    advance.

---

## Description

Locks the domain glossary and writes ADRs for the decisions from Step 15
that are genuinely hard to reverse. This is the point in the pipeline where
vocabulary gets fixed before Phase C (wireframes, scaffolding) builds on top
of it — after this gate, no new terms enter without formally reopening it.

**Correction, replacing the old draft's invocation:** [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) is
not a runnable session. Confirmed directly from its `SKILL.md`: it's an
inline discipline — "actively build and sharpen the project's domain model
*as you design*... don't batch these up, capture them as they happen" — used
by another skill, not invoked on its own. The actual user-invocable skill is
`/grill-with-docs`, whose own `SKILL.md` is one line: "Run a `/grilling`
session, using the [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md) skill." Step 16 invokes
`/grill-with-docs`.

**Correction, replacing the old draft's dual-mode structure:** the old draft
branched on Step 3's disposition table (SKIP/RE-RUN/RUN-AS-NEW), which no
longer exists — that model was retired system-wide. There is no separate
"reconciliation mode" here, and none is needed: [[[pdlf:app-factory/phase-b-discover-and-define/b16-reference|/domain-modeling]]](C:/pdlf/app-factory/phase-b-discover-and-define/b16-reference.md)'s own
cross-reference-with-code discipline already does this work automatically
whenever code exists to check against. New-project entry has no code yet at
this point in the pipeline, so that discipline is simply idle. Existing-
project entry has code, so it fires. One procedure; only the preloaded
context (item 2) differs by entry mode.

## File Placement

Matt Pocock's skill defaults to `CONTEXT.md` and `docs/adr/000N-{slug}.md`
at whatever repo root it runs in. PDLF overrides both, stated explicitly at
invocation, to match the global/local ADR folder pairing already used
everywhere else in this system:

| Artifact | Matt's default | PDLF location |
|---|---|---|
| Glossary | `CONTEXT.md` (repo root) | `dev-{slug}\{slug}-project-library\CONTEXT.md` |
| ADRs | `docs/adr/000N-{slug}.md` | `dev-{slug}\{slug}-project-library\adr-local\000N-{slug}.md` |

Matt's numbering-plus-descriptive-slug filename convention is kept
(`0001-event-sourced-orders.md`-style); only the parent folder changes.

## Why This Step Matters

Stated plainly, not as filler: PDLF's premise is a non-technical developer
running a multi-session pipeline with an agent that has no native memory.
GBrain solves that for facts. `CONTEXT.md` solves the same problem for
vocabulary — without a fixed glossary, a term can mean one thing in this
step's conversation and something else twenty sessions later at the build
loop, with no one positioned to catch the drift before it's built on. ADRs
extend the same verifiable-trail principle Step Receipts already give the
process, applied to hard-to-reverse architecture calls instead.

## Inputs Required

- Step 15's plan artifact and Test Plan Artifact, pasted in full into the
  invocation prompt
- **Existing-project entry only:** existing `CONTEXT.md`, existing
  `adr-local\` contents, and the current codebase (via GBrain source
  registered at Step 11)
- Developer's responses during the `/grilling` interview
- GBrain query at substep 1 (automatic, read-only, sources explicitly
  nominated)

## Outputs

| Artifact | Location | Notes |
|---|---|---|
| Domain glossary | `dev-{slug}\{slug}-project-library\CONTEXT.md` | Created if missing (new entry) or reconciled in place (existing entry). Glossary only — no implementation detail. |
| ADRs | `dev-{slug}\{slug}-project-library\adr-local\000N-{slug}.md` | Only for decisions clearing the three-part test. Not one per decision. |
| Gate `domain-locked` | `gates` table | Full BFT, gate summary, developer approval required, then the request for `/mb-close-out` |
| Step Receipt | `dev-{slug}\{slug}-project-library\pdlf\step-16-receipt.md` | No `outputs` subfolder |
| BFT record | — | Full (gate override) |

## Step Table

| Step | Type | Gate | Handled By |
|---|---|---|---|
| 16 | Skill | **GATE** `domain-locked` | GStack/Matt Pocock `/grill-with-docs` |

## Gate

| Gate | After Step | What is Locked |
|---|---|---|
| `domain-locked` | 16 | Domain glossary and ADRs locked. No new terms without formal gate reopening. |

---

## Handoff

Phase C (Steps 17–24, 26–28) begins only once `domain-locked` passes. Step
17 (Anvil data tables) and downstream steps reference `CONTEXT.md` and
`adr-local\` as the fixed vocabulary — neither should drift without
reopening this gate.

---

## Reference

OpenCode is always the orchestrator. Invoke skills only when they beat
OpenCode directly — confirmed here: the `/grilling` interview with
per-decision developer confirmation and inline glossary/ADR capture is not
something OpenCode would replicate natively.

For execution sequence: [[[pdlf:pdlf-library/specifications-local/spec-execution-discipline|Spec: Execution Discipline]]](C:/pdlf/pdlf-library/specifications-local/spec-execution-discipline.md)
For BFT procedure: [[[pdlf:pdlf-library/specifications-local/spec-bft|Spec: BFT]]](C:/pdlf/pdlf-library/specifications-local/spec-bft.md)
For gate procedure: [[[pdlf:pdlf-library/specifications-local/spec-gate-procedure|Spec: Gate Procedure]]](C:/pdlf/pdlf-library/specifications-local/spec-gate-procedure.md)

GBrain searching is automatic and read-only. New content reaches durable memory only at
close-out, through `/mb-close-out`, run when the developer asks for it.

The agent never commits or pushes; only the developer commits, with `commit-all`.

The ledger row, the BFT record and the Step Receipt are the complete checkpoint. No
separate state file, devlog file or completion report.
