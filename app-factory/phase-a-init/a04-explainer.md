---
title: "a04-explainer"
doc-id: "mb-1d045f70"
updated: "2026-10-29"
---
# Step 4 — Feature for App 1: Explainer

## What it is

Step 4 is the entry point `add-feature-main-app`. Its job: a new feature for App 1 entered into PDLF with its statement and its own short name, after the business is shown healthy, so that Step 12 describes the feature against the application's approved design without re-scoping the application.

## How it works

David opens OpenCode in the business folder and runs `/pdlf-init`, then chooses this entry. The orchestrator runs the health check, asks its questions, runs the app's whole test suite once as the baseline, and writes the entry record. The run continues at Step 12, route C.

## Why it works this way

- **A feature, not a new application.** The application is already defined; the feature path describes only the feature, against the approved design.
- **A baseline first.** A failure found after the feature is built is only the feature's if the suite passed before it.
- **It only records.** An entry point asks and writes the entry record; every change to the business is made by the steps it joins, where it is checked.

## What has to happen

- David opens OpenCode in the business folder and runs `/pdlf-init`.
- David answers the entry's questions.
- David runs `/mb-close-out` when the entry stops, and says "continue".
