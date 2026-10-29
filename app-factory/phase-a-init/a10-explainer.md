---
title: "a10-explainer"
doc-id: "mb-edac8bf6"
updated: "2026-10-29"
---
# Step 10 — Update to App 3 or App 5: Explainer

## What it is

Step 10 is the entry point `update-management-app`. Its job: an update to App 3 or App 5 entered into PDLF, after the business is shown healthy, as a feature when it changes what the app does and otherwise at the step David names, with the root cause of a fault found first.

## How it works

David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`, then chooses this entry. The orchestrator runs the health check, asks its questions, runs the app's whole test suite once as the baseline, and writes the entry record. The run continues at Step 12 for a Feature run; otherwise the step David names.

## Why it works this way

- **A change of behaviour is a feature.** It needs describing and reviewing; a correction goes straight to the step that makes it.
- **The root cause first.** A fix made before the cause is found treats the symptom.
- **It only records.** An entry point asks and writes the entry record; every change to the business is made by the steps it joins, where it is checked.

## What has to happen

- David opens `projects/{slug}-app1` in OpenCode and runs `/pdlf-init`.
- David answers the entry's questions.
- David runs `/mb-close-out` when the entry stops, and says "continue".
