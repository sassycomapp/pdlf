---
title: "f44-explainer"
doc-id: "mb-d4765848"
updated: "2026-11-13"
---
# Step 44 — Release: Explainer

## What it is

Step 44 is where David decides to release, at the gate `production-released`, and the release is carried out.

## How it works

The gate is offered only when no finding is open and the receipts of Steps 41 to 43 match their evidence. David sees the gate summary and says yes or no. On yes, he records the gate. For App 1, he then runs App 5's Release action, which moves clients to the new release in stages: the test client, then a tenth of clients, then everyone, each stage checked first and rolled back by itself if unhealthy. For App 5, David publishes its tagged version in Anvil.

## Why it works this way

- **David's decision.** No release reaches clients without his yes.
- **Small stages.** A problem shows up in a few clients before it can reach all of them.

## What has to happen

- David answers the gate, records it with `pdlf-gate.sh`, and runs the release as the agent instructs.
