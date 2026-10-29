---
title: "b16-explainer"
doc-id: "mb-7df11eae"
updated: "2026-10-29"
---
# Step 16 — Domain Modeling: Explainer

## What it is

Step 16 fixes the business's vocabulary and closes Phase B. It writes the glossary, the one place where each word the business uses is defined, so that a term means the same thing in every later step, every app and every feature. It records the decisions that would be hard to undo. It checks that the words and the data design agree. Then it checks that the whole of Phase B is complete, tested and approved, and asks David to lock it at the gate `domain-locked`. Only after that gate does Phase C start building in Anvil.

## How it works

The step runs Matt Pocock's `grill-with-docs`, which is two skills working together. `grilling` interviews David in rounds: it asks every question that can be asked at that point, each with its recommended answer, and waits for his answers before the next round. `domain-modeling` listens as the interview runs: it challenges a word that clashes with the glossary, proposes a precise word for a vague one, tests each relationship with a concrete example, and writes every settled term into `GLOSSARY.md` straight away. When a decision is hard to reverse, surprising and the result of a real choice, it offers a decision record, which is written only if David agrees.

The glossary belongs to the business, not to one app. App 1, App 5 and every feature share it, so a later run only adds to it. Words shared with other Mybizz applications keep the names `spec-nomenclature` gives them, and the five-app model is never called "multi-tenant". For an application that already exists, the step checks what its documents say against its code and shows David every contradiction; an old glossary is reconciled into the new one.

Anvil's `data-models` skill then checks the glossary against the data design from Step 15: every thing the glossary names must have an owner and a place in the data design, and the data design must use only the glossary's words. Each mismatch is put right with David. The domain map, a picture of the entities and how they relate, is drawn with Archify. Sentinel reviews the glossary for sensitive data, and `gitleaks` checks nothing secret is in it.

Finally the step closes Phase B. It checks every step of the phase for this run: each is complete, each receipt matches its evidence, every test passed, every security finding is decided, no open question remains, and everything Phase C needs is in place. Only then does it show David the gate summary and ask whether to proceed to Phase C. On his yes, the gate is recorded and Phase B is locked.

## Why it works this way

- **One word, one meaning.** An agent has no memory between sessions. Without a fixed glossary, a word drifts in meaning from step to step, and the drift is built into tables and code before anyone notices.
- **The skill's own design.** `grill-with-docs` is how Matt Pocock's skills are meant to build a glossary, and its files keep the skills' own names, so every later Matt Pocock skill reads them without being told where they are.
- **Words and data agree before tables exist.** Step 17 builds the tables next. A table named differently from the glossary would split the business's language at its very first build.
- **Phase B is checked as a whole.** The gate locks everything Phase B produced, so it is offered only when the whole phase is finished, tested and approved, and nothing is left open.
- **Only David passes the gate.** The gate is the last stop before work starts in Anvil. David records his own approval with `pdlf-gate.sh`, and Cupcake stops the agent from writing it. After it, nothing from Phase B changes unless David reopens it.

## What has to happen

- David answers the interview and confirms the shared understanding.
- David decides each decision record.
- David decides whether an old glossary file of an existing application is removed.
- David approves the domain map's scope.
- David answers the gate: yes to proceed to Phase C, or no to stop. On yes, he runs the `pdlf-gate.sh` command the agent gives him, which records his approval.
- Only David commits, with `commit-all`, after `/mb-close-out`.
