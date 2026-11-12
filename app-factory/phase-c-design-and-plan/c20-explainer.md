---
title: "c20-explainer"
doc-id: "mb-6cdcd637"
updated: "2026-11-12"
---
# Step 20 — Design System: Explainer

## What it is

Step 20 writes the application's design system, `DESIGN.md`. It records the design choices that belong to this application, so that every screen and every form follows one design.

## How it works

The look of every Mybizz application comes from `m3-custom-theme`. The theme already holds every colour, type size, shape and spacing, in eight palettes, each with a light and a dark version. So an application does not design colours or fonts; it chooses. GStack's `/design-consultation` helps David make those choices: the starting palette and mode, whether users may switch them, the menu style, the logo and imagery, and the tone of the text.

`DESIGN.md` also states two fixed things: every form meets the rules of `spec-ui-standards`, and every element of every screen uses the theme component that serves it best, chosen from the theme's whole component set. It names the components the application never uses. The chosen palette is checked for readable contrast in light and dark mode. David approves `DESIGN.md` before the step ends.

## Why it works this way

- **Choose, never invent.** Values taken from the theme stay correct in light and dark mode and in every palette; invented values would not.
- **Rules in one place.** The rules every form meets live in `spec-ui-standards`, so `DESIGN.md` never repeats or contradicts them.
- **Full use of the theme.** Stating the rule in the design system is the first of the checks that make every screen use the best component the theme has.

## What has to happen

- David makes the design choices with `/design-consultation` and approves `DESIGN.md`.
- In a test run, David chooses whether to run the step in full, in short, or to skip it.
- Only David commits the project library, with `commit-all`, after `/mb-close-out`.
