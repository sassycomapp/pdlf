---
title: "e36-explainer"
doc-id: "mb-d2f905fa"
updated: "2026-11-13"
---
# Step 36 — Design Review: Explainer

## What it is

Step 36 looks at the feature's forms as users will see them and checks them against the designs David approved.

## How it works

GStack's `browse` opens each form on the hosted app, as each role that may use it, on a phone-sized and a desktop-sized screen, in light and dark mode, and saves a screenshot of each. The agent compares each form with its approved screen requirement, element by element. It checks that the best theme component is used everywhere, that colours and type come from the theme, that the form can be used by keyboard and screen reader, and that the tooltips switch, help videos and dashboard button work. Every difference is a finding; with none, the step records a clean pass. Nothing is changed here.

## Why it works this way

- **What users see.** Only the running form shows the real result.
- **The approved design is the standard.** Anything that differs from it is found and decided at triage.

## What has to happen

- David runs the GStack permission command the agent gives him.
