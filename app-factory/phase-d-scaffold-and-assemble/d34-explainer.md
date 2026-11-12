---
title: "d34-explainer"
doc-id: "mb-97fe5e3e"
updated: "2026-11-12"
---
# Step 34 — Architecture Audit: Explainer

## What it is

Step 34 checks the app's skeleton against every decision locked so far, before a single line of real code is written, and asks David to lock the result at the gate `architecture-verified`. It closes Phase D.

## How it works

The audit checks the app from every side. Anvil's validator and the test scanner run every static check. Anvil's `data-models` compares the tables with the authoritative schema. `graphify` maps the code and compares it with the scaffold plan and the architecture diagram, so that every module is planned and nothing unplanned exists. Every server function the approved screens need must exist with its access rule. Magnus919's security skills check that each trust boundary of the threat model has its control, and run the architecture part of the security assessment plan. GStack's `/cso` scans the skeleton. The parts every Mybizz app shares are checked against the common aspects.

A fault in what PDLF built is fixed at the step that built it. In an app that already had code, an old fault is accepted only when a named ticket will replace that code; anything else blocks the gate. Sentinel then reviews the audit at its highest level. When everything passes, David sees the gate summary and decides whether coding may begin.

## Why it works this way

- **Cheapest point to fix.** A wrong table or a missing access rule is quick to fix now and expensive once code is built on it.
- **Nothing unchecked.** Each part of the app is checked against the document that locked it.
- **Old code is tracked, not excused.** Existing faults pass only with a ticket that removes them.
- **David decides.** Coding begins only on his yes.

## What has to happen

- David decides each finding he is asked about.
- David answers the gate: yes to start the build loop, or no to stop. On yes, he runs the `pdlf-gate.sh` command the agent gives him.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
