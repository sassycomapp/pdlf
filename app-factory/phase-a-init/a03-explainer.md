---
title: "a03-explainer"
doc-id: "mb-038d00e9"
updated: "2026-10-29"
---
# Step 3 — New application with context: Explainer

## What it is

Step 3 is the entry point `new-app-with-context`. Its job: a Mybizz business that already has material (apps, documents, a reference platform) but has not run through PDLF, entered with that material named: which apps exist, where the project context is and which reference platform it follows, so that Step 11 sets it up around what exists and Step 12 reads the context.

## How it works

David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`. He chooses this entry and gives the business's name and the mode. He says which apps exist, whether the old project library holds the context, and whether a reference platform is followed. The orchestrator confirms each answer against the folders, lists the context's documents from GBrain for David to confirm, and writes the business's row and the entry record. The run continues at Step 11, which sets the business up around what exists.

## Why it works this way

- **The context named at the entry.** Step 11 sets the business up around what exists, and Step 12 redevelops the application around its context. Both read the same answers from the entry record, so neither has to ask again or guess.
- **Nothing moved at the entry.** An entry point only records; every change to the business is made by Step 11, where it is checked and recorded.
- **It only records.** An entry point asks and writes the entry record; every change to the business is made by the steps it joins, where it is checked.

## What has to happen

- David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`.
- David answers the entry's questions.
- David runs `/mb-close-out` when the entry stops, and says "continue".
