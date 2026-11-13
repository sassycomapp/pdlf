---
title: "e39-explainer"
doc-id: "mb-b60e120f"
updated: "2026-11-13"
---
# Step 39 — Triage: Explainer

## What it is

Step 39 decides every finding the reviews and tests made for the feature, and asks David to lock the feature at the gate `build-verified`. The next feature starts only after that.

## How it works

Matt Pocock's `triage` labels every finding from Steps 35A to 38A. A finding that needs a fix sends the feature back to Step 35, where the root cause is found, the fix is made and a test is added for it; then the checks run again. A finding David declines is recorded with his reason. When nothing is left open, the whole test suite runs, the receipts are checked against their evidence, the ticket is closed and its old-code items are marked cleared. David then sees the gate summary and decides.

## Why it works this way

- **Nothing left open.** Every finding is fixed or declined with a reason.
- **One feature at a time.** Locking each feature before the next starts keeps problems from piling up.

## What has to happen

- David decides each finding he is asked about.
- David answers the gate; on yes, he runs the `pdlf-gate.sh` command the agent gives him.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
