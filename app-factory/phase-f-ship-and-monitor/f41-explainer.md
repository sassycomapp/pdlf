---
title: "f41-explainer"
doc-id: "mb-9ab97a59"
updated: "2026-11-13"
---
# Step 41 — Release Readiness: Explainer

## What it is

Step 41 proves the app is ready to release.

## How it works

The agent checks every feature of the release has passed its gate. Matt Pocock's `tdd` runs the whole test suite and every release test the app's test plan names. Magnus919's `security-audit-methodology` runs the pre-release security assessment planned at Step 15, and GStack's `/cso` scans the whole app. GStack's `benchmark` records how fast the public pages are, for later comparison. A schema change must only add, never remove. The release notes are written.

Before a first release, the legal documents are checked, and the exit export and consent system are proven on the test client. David then commits, tags and pushes.

## Why it works this way

- **Evidence before release.** The release gate at Step 44 decides on proven facts.

## What has to happen

- David commits, tags and pushes the app with the command the agent gives him.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
