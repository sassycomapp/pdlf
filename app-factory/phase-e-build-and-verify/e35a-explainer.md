---
title: "e35a-explainer"
doc-id: "mb-ca5481a1"
updated: "2026-11-13"
---
# Step 35A — Testing: Explainer

## What it is

Step 35A tests the feature more widely than Step 35 did, and checks the tools and packages it brings in.

## How it works

Matt Pocock's `tdd` adds every edge-case, integration and security test the test plan gives the feature. GStack's `test-audit` looks for tests that test little or repeat each other; each is put right with David's approval. `pip-audit` and GStack's `/cso --supply-chain` check the tools and packages for known risks, and every finding goes to triage.

## Why it works this way

- **Holds under pressure.** A feature that works on the normal path can still fail at its edges or under attack.
- **Honest tests.** A weak test looks like protection and is not.

## What has to happen

- David approves each correction of a weak or duplicate test.
