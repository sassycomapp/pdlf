---
title: "d31-explainer"
doc-id: "mb-9ddc7703"
updated: "2026-11-12"
---
# Step 31 — Scaffold Plan: Explainer

## What it is

Step 31 plans the structure of the app before any code is written: every module, every function, where each one lives, who may call it, what it will do and which test proves it. The plan is written into the project's `scaffold-spec.md`.

## How it works

Matt Pocock's `codebase-design` shapes the modules from the architecture locked in Phase B: a few deep modules with clean edges, and the business rules kept in pure modules that do not depend on Anvil. Anvil's own skills decide where each table's behaviour lives and where each module must sit. The approved screen requirements already name every server function the forms will call, so each of those gets its planned function, under the same name. Every planned function carries its access rule from the access matrix and the test that will prove it.

The parts every Mybizz application shares (the Vault, payments, webhooks, email, storage and exit export, the heartbeat and the management endpoints) are planned in the one structure set for all applications. The step also works out the settings the test scanner needs for this app.

For an app that already has code, the step maps that code and marks every existing module and function as keep, rework or remove, each rework and removal tied to the ticket whose build will do it. Nothing is changed yet. David approves the plan before the step ends.

## Why it works this way

- **Structure before code.** A planned structure, checked at Step 34, stops each feature from inventing its own.
- **One document.** Every project library already has `scaffold-spec.md` for the app's structure, so the plan goes there and nowhere else.
- **Forms and server code meet.** Using the function names the screens already give means the forms built later call functions that exist.
- **Existing code is not lost.** Marking every existing module against a ticket means an existing app moves through PDLF step by step, with nothing forgotten.

## What has to happen

- David approves `scaffold-spec.md` and, for an existing app, the disposition list.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
