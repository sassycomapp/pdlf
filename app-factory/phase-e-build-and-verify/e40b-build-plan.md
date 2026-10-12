---
title: "e40b-build-plan"
doc-id: "mb-b74e415a"
updated: "2026-10-12"
---

## From `pdlf-build-plan.md`: step entry

### Phase E — Build and Verify

Steps 35 to 40B run once per feature, one feature at a time; the run plan governs the loop. Each feature ends with the gate `build-verified` (Step 39).

#### Step 40B: Approved fixes

**Must achieve:** Applies only the fixes the developer approved from Step 40. Skipped if Step 40 did not run or found nothing to fix.

**Carried out by:** OpenCode.

**Runs:** once per feature.
