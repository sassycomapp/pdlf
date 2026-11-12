---
title: "c19-explainer"
doc-id: "mb-740d0f81"
updated: "2026-11-12"
---
# Step 19 — Tickets: Explainer

## What it is

Step 19 breaks the locked plan into feature tickets: one file per feature, in the order the features can be built. The tickets are the build list the rest of PDLF works through.

## How it works

Matt Pocock's `to-tickets` skill reads the reviewed plan and the test plan and writes one ticket per feature into the project library's `pdlf-tickets` folder. The order is fixed by the UI production method: the layouts and shared parts first, then sign-in, then every other feature as its dependencies allow. A custom component shared by several features gets its own ticket, ahead of the features that use it.

Each ticket names everything its feature needs: each form by its module path, each server function, each table as the authoritative schema names it, the acceptance tests from the test plan, and the security criteria from the threat model. Archify draws the user flows and the flow of each feature that crosses more than one form. David approves the ticket list before the step ends.

## Why it works this way

- **Every form is known.** Step 22 designs one form at a time from the tickets, so naming each form here means none is missed.
- **Buildable order.** Building in dependency order means nothing is built before what it rests on.
- **Done is defined.** A ticket that names its tests says exactly when its feature is finished.

## What has to happen

- David approves the scope of each flow diagram.
- David approves the ticket list.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
