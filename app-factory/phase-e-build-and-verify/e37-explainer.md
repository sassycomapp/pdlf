---
title: "e37-explainer"
doc-id: "mb-880a9e2d"
updated: "2026-11-13"
---
# Step 37 — Code Review: Explainer

## What it is

Step 37 reviews everything the feature changed, to find bugs and broken standards before the feature ships.

## How it works

Matt Pocock's `code-review` reads the feature's changes against two things: the standards, which are Anvil's own skills for code, forms, data and settings together with Mybizz's Anvil standards and common aspects, and the ticket, to check the change does what it should. Each form and spec sheet is checked against its approved screen requirement, and Anvil's agent is confirmed to have changed only the event handlers. The test scanner runs again. GStack's `/cso` reviews the changes for security, and Sentinel reviews them at its highest level. Each review runs on its own. Every finding is recorded; nothing is fixed here.

## Why it works this way

- **Anvil's rules.** Code written against Anvil's own rules is code Anvil handles correctly.
- **Independent reviews.** Separate sessions mean each reviewer judges for itself.
- **Decided at triage.** Every finding is weighed at Step 39 before anything changes.

## What has to happen

- David runs the GStack permission command the agent gives him, and decides any Sentinel escalation.
