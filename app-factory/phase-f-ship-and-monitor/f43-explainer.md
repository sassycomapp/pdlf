---
title: "f43-explainer"
doc-id: "mb-e972f522"
updated: "2026-11-13"
---
# Step 43 — Client Instance Check: Explainer

## What it is

Step 43 proves the test client instance is healthy on the new release, and records its health so later problems can be spotted.

## How it works

The test client's heartbeat must report the new release and schema. GStack's `/qa-only` runs a quick smoke test, and `/canary` records the instance's health baseline. Clients are checked to be unable to reach each other's data, and at the first release a new client is checked to start secure. For App 5's own release, this step is skipped.

## Why it works this way

- **One client first.** Every client moves only after one has proven the release.

## What has to happen

- David runs the GStack permission command, and rolls back if a check fails.
