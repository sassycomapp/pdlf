---
title: "e38a-explainer"
doc-id: "mb-4393301e"
updated: "2026-11-13"
---
# Step 38A — Package Check: Explainer

## What it is

Step 38A records Anvil's own security check of the server packages, when the feature changed them.

## How it works

David copies Anvil's package report from the Anvil editor into the step folder. The agent compares it with the local `pip-audit` result from Step 35A and records every finding for triage. When the feature did not change the server packages, the step is skipped.

## Why it works this way

- **The live packages.** Anvil checks what it actually runs, which a local tool cannot see.

## What has to happen

- David copies Anvil's package report when the agent asks.
