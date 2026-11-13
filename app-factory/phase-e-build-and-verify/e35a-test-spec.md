---
title: "e35a-test-spec"
doc-id: "mb-c4ff5468"
updated: "2026-11-13"
---
# Step 35A: Testing — Test Specification

**Proves:** The feature passes every edge-case, integration and security test the test plan gives it, its tests are sound, and its tools and packages are checked.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md) and, for the PR tests, in [[[pdlf:pdlf-library/specifications-local/spec-pdlf-process-tests]]](C:/pdlf/pdlf-library/specifications-local/spec-pdlf-process-tests.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e35a\`; every result is recorded in `{slug}-e35a-{run}-{ticket}-checks.xml`, naming its evidence, as `ts-method` section 5 sets out.

| Test | Applied here |
|---|---|
| PR-01 | Step 35 is complete for the ticket. |
| IN-05 | Failure and contention safe. |
| IN-06 | Server sets amounts and order. |
| IN-08 | Outside services fail safely. |
| IN-09 | Emails right. |
| IN-10 | Storage right. |
| IN-12 | Heartbeat and management token. |
| IN-13 | Vault, when touched. |
| IN-14 | Exit export and data rights cover the feature's data. |
| IN-15 | Events logged; audit log unchangeable. |
| IN-16 | Rate limits and safe failure. |
| IN-17 | Volume at ten times a client. |
| SC-01 | Passwords and sign-in, when touched. |
| SC-02 | Second factor for every account holder; Owner FIDO2; the Vault's own authenticator code on every open. |
| SC-03 | Step-up on high-value actions. |
| SC-04 | Sessions, when touched. |
| SC-07 | Files, links, redirects, when present. |
| SC-08 | Planes separate. |
| SC-11 | Refunds and discounts. |
| SC-12 | Audit trail. |
| SC-13 | Fail closed. |
| SC-14 | Client isolation. |
| ST-13 | Dependencies and static analysis clean, or each finding in `triage_findings`. |
| PR-07 | No test weakened by the audit. |

**On failure:** A failing test returns the feature to Step 35; a finding goes to Step 39.
