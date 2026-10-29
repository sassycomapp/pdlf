---
title: "a06-explainer"
doc-id: "mb-2becc3e4"
updated: "2026-10-29"
---
# Step 6 — Release into App 2: Explainer

## What it is

Step 6 is the entry point `compile-master-template`. Its job: a release of App 1's approved code into App 2, `master_template`, entered into PDLF after the business is shown healthy and App 1's suite passes, so that the release steps start from a sound App 1.

## How it works

David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`, then chooses this entry. The orchestrator runs the health check, asks its questions, runs the app's whole test suite once as the baseline, and writes the entry record. The run continues at Step 41.

## Why it works this way

- **A passing App 1 only.** App 2 is the dependency of every client instance; a fault released into it reaches every client.
- **It only records.** An entry point asks and writes the entry record; every change to the business is made by the steps it joins, where it is checked.

## What has to happen

- David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`.
- David answers the entry's questions.
- David runs `/mb-close-out` when the entry stops, and says "continue".
