---
title: "f45-build-plan"
doc-id: "mb-1628cc4a"
updated: "2026-11-08"
---

## From `pdlf-build-plan.md`: step entry

### Phase F — Ship and Monitor

Ends with the gates `production-released` (Step 44) and `released` (Step 46). The release is App 1's approved code pushed into App 2, `master_template`, built with App 3 into the release image, and moved to every client instance by App 5's Release action ([[[default:specifications-global/spec-client-instance-hosting|Client Instance Hosting]]](C:/dev/project-library-global/specifications-global/spec-client-instance-hosting.md)).

#### Step 45: Production check

**Must achieve:** Watches the released application for errors and performance problems.

**Carried out by:** GStack, using `/canary`.

**Skills.** Every skill's output is used by the step named after the arrow.
- `/canary` (GStack): watches the test client instance against the baseline from Step 43 → Step 46.
- `mb-sentinel-review`, Medium → `triage_findings`.

**Must be built so that:**
- App 5 reads each client instance's heartbeat: every client instance reports the release version and schema fingerprint and passes its smoke test (test RL-05); App 5 flags any client nearing its container's memory and the business nearing its cluster's client limit (test RL-12);

**Carried over from the old workflow** (to be checked against the step file, then removed):

1. Query GBrain — Context relevant to post-deploy monitoring
2. Invoke GStack `/canary` — Targeted at the test client instance; watches for console errors, performance regressions
3. Verify output — Canary report with initial health check; STOP if critical failures
4. Write Step 45 ledger row — `completed_at`
5. Generate Step Receipt — `<project-library>/pdlf/outputs/step-45-receipt.md`
6. Apply BFT — Full level
7. Follow execution sequence — Housekeeping, stop, wait for continue
