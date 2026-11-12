---
title: "c21-explainer"
doc-id: "mb-44aa7497"
updated: "2026-11-12"
---
# Step 21 — Concept Check: Explainer

## What it is

Step 21 checks every concept document against every other for contradictions, has David resolve each one, and then asks David to lock the concept at the gate `concept-locked`.

## How it works

The concept is spread over several documents: the reviewed plan, the test plan, the access matrix, the threat model, the glossary, the decision records, the authoritative schema, the tickets and flows, and `DESIGN.md`. The agent compares every pair. It also runs fixed checks: every table a ticket uses exists in the schema, every form and server function is in the access matrix or listed for Step 22 to add, every word is the glossary's word, every test a ticket names exists, and every decision record is followed.

Each contradiction is shown to David with the agent's recommended correction, and the document at fault is corrected. When nothing contradicts anything, the agent checks that the receipts of Steps 17 to 20 match their evidence, shows David the gate summary, and asks whether to proceed. On his yes, David records the gate with `pdlf-gate.sh`.

## Why it works this way

- **Contradictions hide between documents.** Each document can be right on its own and still disagree with another; only comparing every pair finds that.
- **Fixed at the source.** Correcting the document itself stops the contradiction coming back in a later step.
- **No new features after this.** Screens are designed next. Locking the concept here keeps every screen designed against the whole application.

## What has to happen

- David decides each contradiction's correction.
- David answers the gate: yes to proceed to the screen requirements, or no to stop. On yes, he runs the `pdlf-gate.sh` command the agent gives him.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
