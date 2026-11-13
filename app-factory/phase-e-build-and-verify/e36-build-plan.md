---
title: "e36-build-plan"
doc-id: "mb-06eb6076"
updated: "2026-11-13"
---
# Step 36 — Design Review: Build Plan

## Step entry

### Phase E — Build and Verify

Phase E runs once for each ticket, in the build order of the ticket list; every `{run}` path below carries the ticket as `{ticket}`.

#### Step 36: Design review

**Must achieve:** a visual audit of the feature as it will ship: each of its forms, running, compared with its approved screen requirement on phone and desktop and in light and dark mode, its use of `m3-custom-theme` and its accessibility checked, with every finding recorded and a clean-pass statement when there is none.

**Starts from:** the feature after Step 40B; the approved screen requirements of the ticket's forms; `DESIGN.md`; the theme's component inventory.

**Produces:** the design findings; in `pdlf-outputs\e36\`: the screenshots, the findings, the test results and the Step Receipt; the ledger row and the BFT record.

**Carried out by:** OpenCode, with GStack's `browse`.

**Must be built so that:**
- `browse` opens each of the ticket's forms on hosted App {n}, signed in as each role that may use it, at phone (390 px) and desktop (1440 px) width, in light and dark mode, and saves a screenshot of each;
- each form is compared with its approved screen requirement: every element present, with the theme component, role, text and empty state the requirement gives, and nothing extra;
- theme usage is checked: no element shows a plainer component where the requirement names a better one, and no colour, font or spacing differs from the theme;
- accessibility is checked to [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) section 13: keyboard order, visible focus, names on icon buttons, error messages that say what to fix, and states not shown by colour alone;
- the always-available controls (tooltips switch, help videos, dashboard) work on every form;
- nothing sensitive appears in a page address or in browser storage;
- every finding is written to the findings file with its form, its evidence and its severity; with no finding, the file states a clean pass;
- no form is changed in this step; fixes are decided at Step 39 and made at Step 35;
- its ledger row carries the ticket, with `step_type = 'skill'`, `skill_family = 'gstack'`, `synthesized = false`, and `inputs_used` naming Step 40B.

**BFT level:** Full.

**Gate:** none.

**References:** [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md); [[[default:specifications-global/mo-ui-production|UI Production Method]]](C:/dev/project-library-global/specifications-global/mo-ui-production.md).

**Skills.** Every skill's output is used by the step named after the arrow.
- `browse` (GStack): each form running, in every width, mode and role → the comparison, then Step 39.

**Not used:** GStack's `/design-review`, because it commits each fix itself; agents never commit.

**Layers with no skill:** the comparison with the screen requirement and the theme inventory; no installed skill knows `m3-custom-theme`, so OpenCode makes it.

**Testing:** [[[pdlf:app-factory/phase-e-build-and-verify/e36-test-spec|Step 36 Test Specification]]](C:/pdlf/app-factory/phase-e-build-and-verify/e36-test-spec.md).

**Standards:** [[[default:specifications-global/spec-ui-standards|UI Standards]]](C:/dev/project-library-global/specifications-global/spec-ui-standards.md) sections 3, 7, 12 and 13.

## Why it is built this way

- **Seen as it ships.** Only the running form, in every width and mode, shows what users will see.
- **Against the approved design.** The screen requirement David approved is the standard; anything different is a finding.
- **Review, not repair.** Findings go to triage, so every change is decided and recorded.
