---
title: "e35-test-spec"
updated: "2026-10-22"
doc-id: "mb-e4dc7f9d"
---
# Step 35: Build — Test Specification

**Proves:** The feature is built test-first and proven at Levels 0 to 3, and the developer signs it off.

Tests are defined in [[[default:test-suite/ts-catalogue]]](C:/dev/project-library-global/test-suite/ts-catalogue.md). Evidence is saved in `{slug}-project-library\pdlf-outputs\e35\`.

| Test | Applied here |
|---|---|
| LG-01 | Each behaviour test-first. |
| LG-02 | Edges, odd and hostile input. |
| LG-03 | Lifecycle transitions. |
| LG-04 | Money exact. |
| LG-05 | Time right. |
| LG-06 | Real code tested. |
| IN-01 | The app runs locally. |
| IN-02 | Every new function for every role. |
| IN-03 | Own records only. |
| IN-04 | Allowed fields only. |
| IN-07 | New webhooks verified and exactly-once. |
| IN-11 | New tasks correct. |
| SC-05 | Form checks enforced by the server. |
| SC-06 | Hostile input harmless. |
| DM-01 | When the ticket touches this domain rule. |
| DM-02 | When the ticket touches this domain rule. |
| DM-03 | When the ticket touches this domain rule. |
| DM-04 | When the ticket touches this domain rule. |
| DM-05 | When the ticket touches this domain rule. |
| DM-06 | When the ticket touches this domain rule. |
| DM-07 | When the ticket touches this domain rule. |
| DM-08 | When the ticket touches this domain rule. |
| DM-09 | When the ticket touches this domain rule. |
| DM-10 | When the ticket touches this domain rule. |
| BR-01 | Flows end to end, desktop and mobile. |
| BR-02 | Edge cases and errors. |
| BR-09 | The developer signs off. |
| IN-18 | Hosted test data removed. |
| PR-07 | No test weakened. |
| PR-04 | Sentinel ran at High. |

**On failure:** A failing test stops the build: root cause found, code fixed, level run again.
