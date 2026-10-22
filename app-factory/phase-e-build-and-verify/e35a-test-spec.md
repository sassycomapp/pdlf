---
title: "e35a-test-spec"
updated: "2026-10-22"
doc-id: "mb-c4ff5468"
---
# Step 35A: Testing — Test Specification

**Proves:** The feature holds at its edges, under attack, at volume and through its dependencies.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e35a\`.

| Test | Applied here |
|---|---|
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
| SC-02 | Second factor; Owner FIDO2. |
| SC-03 | Step-up on high-value actions. |
| SC-04 | Sessions, when touched. |
| SC-07 | Files, links, redirects, when present. |
| SC-08 | Planes separate. |
| SC-11 | Refunds and discounts. |
| SC-12 | Audit trail. |
| SC-13 | Fail closed. |
| SC-14 | Client isolation. |
| ST-13 | Dependencies and static analysis clean. |

**On failure:** Each failure is recorded in `triage_findings` and goes to Step 39.
