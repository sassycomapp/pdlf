---
title: "c28-build-plan"
doc-id: "mb-1873894a"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase C — Design and Plan

Ends with the gates `concept-locked` (Step 21) and `wireframes-approved` (Step 26).

#### Step 28: Screen to PNG

**Must achieve:** Converts the screens to images. Deferred: runs only if the developer asks for it.

**Carried out by:** An external tool.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to screen conversion
2. Check deferral status — Skip unless explicitly requested by developer
3. If active: Convert screen HTML from Step 27 to PNG via external rendering tool
4. Verify output — Screen PNG in same folder as Step 27; STOP if missing
5. Write Step 28 ledger row — `completed_at` (or `deferred`)
6. Generate Step Receipt — `<project-library>/pdlf/outputs/step-28-receipt.md`
7. Apply BFT — None
8. Follow execution sequence — Housekeeping, stop, wait for continue
