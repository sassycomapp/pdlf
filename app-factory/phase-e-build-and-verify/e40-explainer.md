---
title: "e40-explainer"
doc-id: "mb-8f756d68"
updated: "2026-11-13"
---
# Step 40 — Architecture Scan: Explainer

## What it is

Step 40 is an optional, read-only scan of the feature's code for places where its structure could be cleaner. David decides for each ticket whether it runs, and which of its findings are fixed.

## How it works

`graphify` maps how the code's parts depend on each other, and Matt Pocock's `improve-codebase-architecture` reads that map against the planned modules. It changes nothing. Each finding goes to David, who approves or declines it. Approved fixes are made at Step 40B.

## Why it works this way

- **Cleaner before review.** A fix made now is reviewed with the rest of the feature.
- **Advice, not orders.** David decides what is worth changing.

## What has to happen

- David decides whether the scan runs, and decides each finding.
