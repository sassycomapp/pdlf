---
title: "d32-explainer"
doc-id: "mb-640a6cc7"
updated: "2026-11-12"
---
# Step 32 — Create the Scaffold: Explainer

## What it is

Step 32 creates, in the app, every module and function the scaffold plan names, as empty stubs. It adds nothing else. David then commits and pushes the app, so the stubs reach Anvil.

## How it works

The agent uses Anvil's own skills to write each planned module and function that does not exist yet, exactly as `scaffold-spec.md` names it: with its access rule, its rate limit where one is planned, and a one-line note of what it will do and which test proves it. Each stub's body raises an error, so it cannot pass a test before it is built. The agent also fills the test scanner's settings for this app from the plan.

In an app that already has code, existing modules are left alone. Their rework or removal happens later, with the ticket that needs it. Anvil's validator and the test scanner's structure check must pass before David commits and pushes.

## Why it works this way

- **Only the plan.** Creating exactly what was approved keeps the structure Step 34 checks equal to the one David approved.
- **Nothing looks finished early.** A stub that raises an error fails every test until it is built.
- **The app keeps working.** Existing code is changed only with the feature that needs the change.

## What has to happen

- David commits and pushes the app with the command the agent gives him.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
