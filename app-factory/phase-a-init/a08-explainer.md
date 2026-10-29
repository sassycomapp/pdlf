---
title: "a08-explainer"
doc-id: "mb-714f8928"
updated: "2026-10-29"
---
# Step 8 — Create App 5: Explainer

## What it is

Step 8 is the entry point `create-management-app`. Its job: App 5, the management app, entered into PDLF for a business whose existing apps are shown healthy, so that Step 11 sets it up and Steps 12 to 16 design it: it receives every client instance's heartbeat, flags clients that need a higher plan tier, and runs each client's exit handover.

## How it works

David opens OpenCode in the business folder and runs `/pdlf-init`, then chooses this entry. The orchestrator runs the health check, asks its questions, and writes the entry record. The run continues at Step 11, route C.

## Why it works this way

- **Designed, unlike App 3.** App 5 is an application of its own, with its own users and work, so it runs through the design steps.
- **It only records.** An entry point asks and writes the entry record; every change to the business is made by the steps it joins, where it is checked.

## What has to happen

- David opens OpenCode in the business folder and runs `/pdlf-init`.
- David answers the entry's questions.
- David runs `/mb-close-out` when the entry stops, and says "continue".
