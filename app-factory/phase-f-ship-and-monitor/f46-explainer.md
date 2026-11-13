---
title: "f46-explainer"
doc-id: "mb-2de0c675"
updated: "2026-11-13"
---
# Step 46 — Learning: Explainer

## What it is

Step 46 captures what the build taught and puts each lesson where the next build will read it. It closes the build cycle at the gate `released`.

## How it works

GStack's `/retro` reviews the build's history and `/learn` exports what GStack's skills learned. Each lesson is sorted: lessons about the app go to its project library; lessons about the machine go into PDLF, the global library or the skill concerned. With David's approval, each lesson is written into its source, and a fixed problem gets a test. `mb-submit-memory` then submits each lesson to GBrain. David closes the cycle at the gate.

## Why it works this way

- **Lessons change the next build.** Written into the sources, they are read automatically next time.
- **PDLF stays a general machine.** Nothing about one app is kept in PDLF.

## What has to happen

- David approves each lesson and answers the gate; on yes, he runs the `pdlf-gate.sh` command the agent gives him.
