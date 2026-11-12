---
title: "c18-explainer"
doc-id: "mb-481dfb07"
updated: "2026-11-12"
---
# Step 18 — Pull to Local: Explainer

## What it is

Step 18 brings David's local copy of the app level with Anvil after work in the Anvil editor. The same procedure runs again as Step 33.

## How it works

David runs one `git pull` command in the app's folder. The agent then checks the result: nothing is left uncommitted, the local copy equals the copy on GitHub, the change the previous step made is there, nothing else changed, and Anvil's own validator accepts the app. For Step 17, the expected change is the schema in `anvil.yaml`, which must equal the authoritative schema.

## Why it works this way

- **Later steps read the local copy.** Every later step reads the app from David's computer, so that copy must be exactly what Anvil holds.
- **Only the expected change.** A file that changed without a reason is a sign of work nobody planned; the step stops so that David sees it.
- **One procedure.** Two steps need the same pull and the same checks, so the procedure is written once.

## What has to happen

- David runs the pull command the agent gives him.
- David decides each deviation the checks raise.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
