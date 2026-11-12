---
title: "d33-explainer"
doc-id: "mb-20bd6c13"
updated: "2026-11-12"
---
# Step 33 — Pull to Local: Explainer

## What it is

Step 33 brings David's local copy of the app level with Anvil after the scaffold was pushed. It runs the same pull procedure as Step 18.

## How it works

David runs one `git pull`. The agent checks that nothing is left uncommitted, that the local copy equals GitHub's, that every stub Step 32 created has arrived, that nothing else changed apart from Anvil's own formatting, and that Anvil's validator accepts the app.

## Why it works this way

- **The audit reads the real app.** Step 34 checks the app's structure; it must check exactly what Anvil holds.
- **Written once.** The procedure lives at Step 18, so three steps cannot drift apart.

## What has to happen

- David runs the pull command the agent gives him.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
