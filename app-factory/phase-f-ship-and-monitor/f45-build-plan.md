---
title: "f45-build-plan"
doc-id: "mb-1628cc4a"
updated: "2026-10-20"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is the clone of App 1's approved code into App 2, `master_template`, which every client instance depends on.

#### Step 45: Production check

**Must achieve:** Watches the released application for errors and performance problems.

**Carried out by:** GStack, using `/canary`.

**Skills.** Every skill's output is used by the step named after the arrow.
- `/canary` (GStack): watches App 2 and the test client instance against the baseline from Step 43 → Step 46.
- `mb-sentinel-review`, Medium → `triage_findings`.

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to post-deploy monitoring
2. Invoke GStack `/canary` — Targeted at Production URL from Step 44; watches for console errors, performance regressions
3. Verify output — Canary report with initial health check; STOP if critical failures
4. Write Step 45 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-45-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue
