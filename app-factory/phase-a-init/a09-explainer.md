---
title: "a09-explainer"
doc-id: "mb-37bd0ef7"
updated: "2026-10-29"
---
# Step 9 — Feature for App 3 or App 5: Explainer

## What it is

Step 9 is the entry point `add-feature-management-app`. Its job: a new feature for App 3 or App 5 entered into PDLF with its statement and its own short name, after the business is shown healthy, so that Step 12 describes it against that app's approved design.

## How it works

David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`, then chooses this entry. The orchestrator runs the health check, asks its questions, runs the app's whole test suite once as the baseline, and writes the entry record. The run continues at Step 12, route C.

## Why it works this way

- **The same feature path for every app.** A feature is described, reviewed and modelled the same way whichever app it belongs to.
- **It only records.** An entry point asks and writes the entry record; every change to the business is made by the steps it joins, where it is checked.

## What has to happen

- David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`.
- David answers the entry's questions.
- David runs `/mb-close-out` when the entry stops, and says "continue".
