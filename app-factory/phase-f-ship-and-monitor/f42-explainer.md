---
title: "f42-explainer"
doc-id: "mb-5e27c1ac"
updated: "2026-11-13"
---
# Step 42 — Release to App 2: Explainer

## What it is

Step 42 turns App 1's tagged release into the release image every client instance will run, and puts it on the test client instance first.

## How it works

Every client instance first backs up its data to its own locked bucket. David pushes App 1's tag into App 2 and writes the release's table changes into App 3. The image workflow in App 4's repository builds the release image, scans it, refuses end-of-life software or old serious findings, and signs it. The test suite runs on the image. App 5 then checks the signature and moves the test client instance to the image. The agent checks each result; any failure stops the release and can be rolled back. For App 5's own release, this step is skipped.

## Why it works this way

- **Clients are safe.** Data is backed up before anything changes.
- **What was tested ships.** The image holds exactly the tagged code.

## What has to happen

- David follows the agent's instructions for each part, in order.
