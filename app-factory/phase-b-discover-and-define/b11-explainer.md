---
title: "b11-explainer"
doc-id: "mb-afda1c7f"
updated: "2026-10-13"
---
# Step 11 — Init: Explainer

## What it is

Step 11 lays the foundation of a Mybizz business, or of a new app in one, before anything about the application is designed. It makes sure the business's folders and repositories exist and are linked to GitHub, that its project library has the standard structure, that GBrain and the commit tools know about it, and that the ledger has its record. Every later step relies on that foundation without checking it again.

## How it works

The orchestrator hands Step 11 the entry record, which says how the work entered PDLF. Step 11 then takes one of three routes.

- **A new business** (entry 02). David gives the slug, the business's name, its domain and the mode. The agent copies the project template into `C:\dev\dev-{slug}\`. David creates App 1 in Anvil and connects it to GitHub; the agent clones it into its folder. With David's permission the agent creates the private project library on GitHub, places the blank pre-project files and asks David to fill them in.
- **An application with context** (entry 03). The business already has some of its repositories. The agent checks each one, creates only what is missing and changes nothing that exists.
- **A new app in an existing business** (entries 07 and 08). The agent checks the business is sound, then does only the new app's part: David creates it in Anvil, and the agent clones it into its folder.

For routes A and B the agent then sets up the Matt Pocock skills with PDLF's answers fixed in advance, registers the project library in GBrain, and gives David the exact lines that bring it under the commit hook and `commit-all`. Every route ends the same way: Sentinel reviews what was created for security, the health check proves the setup is sound, and the step writes its ledger row and receipt, explains itself and asks David to run `/mb-close-out`.

## Why it works this way

- **One end for every route.** However a business enters PDLF, it leaves Step 11 having passed the same health check, so every later step can trust the same foundation.
- **The tools are checked first.** A missing skill or an unreachable ledger found at Step 11 costs nothing; found halfway through a review, it costs the review.
- **Anvil creates each app's repository.** An Anvil app's code repository must come from Anvil, or Anvil cannot keep it in step. So David creates the app, and the agent only clones it.
- **The template is copied without document identities.** The commit hook gives every document a permanent identity. If the template's identities were copied, every project would share them and the hook would confuse one project's documents with another's.
- **Tickets stay in the private library.** The app repositories are public, and tickets describe the business's plans.
- **Nothing existing is changed without permission.** An existing application's material is David's. Step 11 reports what is wrong; David decides.
- **Sentinel reviews Step 11.** The app repositories are public, so a secret that slips in at the start would be published with everything after it.

## What has to happen

- David creates each app in Anvil and connects it to GitHub when asked.
- David approves the creation of the project library on GitHub.
- David adds the project library to the commit tools with the lines the agent gives him, and confirms.
- David fills in the three pre-project files before Step 12.
- Only David commits, with `commit-all`, after `/mb-close-out`.
