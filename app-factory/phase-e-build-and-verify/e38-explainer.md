---
title: "e38-explainer"
doc-id: "mb-92dfa9e1"
updated: "2026-11-13"
---
# Step 38 — Quality Testing: Explainer

## What it is

Step 38 tests the feature the way users will use it, checks that nothing earlier has broken, and measures how fast its pages are.

## How it works

GStack's `/qa-only` carries out every action listed in each of the feature's spec sheets, on the hosted app with test data only, as each kind of user and signed out, and checks each gives the stated result. It then runs every flow of every earlier feature again and checks the browser shows no error. GStack's `benchmark` measures each page's speed against its budget. Every problem is recorded; nothing is fixed here. Sentinel reviews the findings.

## Why it works this way

- **The spec sheet is the promise.** Each action it lists must work as stated.
- **Old features stay working.** Every earlier feature is tested again each time.

## What has to happen

- David runs the GStack permission command the agent gives him, and decides any Sentinel escalation.
