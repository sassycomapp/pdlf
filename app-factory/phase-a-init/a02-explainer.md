---
title: "a02-explainer"
doc-id: "mb-1f23d447"
updated: "2026-10-29"
---
# Step 2 — New application, no context: Explainer

## What it is

Step 2 is the entry point `new-app-no-context`. Its job: a new Mybizz business, with no earlier material, entered into PDLF: its business row and its entry record written, so that Step 11 can set the business up from the project template.

## How it works

David creates the business folder with an empty App 1 repository and its link, opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`. He chooses this entry and gives the business's name and the mode. The orchestrator writes the business's row and the entry record, and the run continues at Step 11, which copies the project template into the folder.

## Why it works this way

- **An empty folder only.** Material already in the folder is context, and context is entry 03's to read; taking entry 02 there would set it aside unread.
- **It only records.** An entry point asks and writes the entry record; every change to the business is made by the steps it joins, where it is checked.

## What has to happen

- David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`.
- David answers the entry's questions.
- David runs `/mb-close-out` when the entry stops, and says "continue".
