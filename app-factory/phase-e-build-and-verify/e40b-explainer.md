---
title: "e40b-explainer"
doc-id: "mb-bb185d9c"
updated: "2026-11-13"
---
# Step 40B — Approved Fixes: Explainer

## What it is

Step 40B applies the architecture fixes David approved at Step 40, and nothing else. It is skipped when there is nothing to fix.

## How it works

Each approved fix is made with Matt Pocock's `codebase-design` and Anvil's skill for the part of the code it touches. Then every test of the feature and the whole suite runs again. David commits the app.

## Why it works this way

- **Only what was approved.** No unasked change slips in.
- **Nothing broken.** A structural change is proven safe by running every test again.

## What has to happen

- David commits the app with the command the agent gives him.
