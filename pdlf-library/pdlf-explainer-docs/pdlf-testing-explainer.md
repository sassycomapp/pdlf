---
title: "pdlf-testing-explainer"
updated: "2026-10-22"
doc-id: "mb-2bb4ba8f"
---
# PDLF Testing — How It Works

This document explains how PDLF tests the applications it builds. The tests are defined in the test suite, `C:\dev\project-library-global\test-suite\`; how testing is done is in [[[default:test-suite/ts-method]]](C:/dev/project-library-global/test-suite/ts-method.md). Where the two disagree, the test suite is right and this document is corrected.

## 1. What testing proves

Every Mybizz application must be secure, work fully, keep its data intact and obey Mybizz's rules. Testing proves this step by step, with saved evidence, never with an agent's word.

Every application is designed and reviewed against OWASP ASVS 5.0 Level 2 principles, with Level 3 controls on payment, administration and high-value transaction paths. Mybizz never claims to be "ASVS certified", because ASVS has no certification. The Level 3 controls are: phishing-resistant sign-in for owners, a detailed audit trail of money and access changes, separation of customers, client staff and Mybizz administration, a yearly independent penetration test, and secure development controls. The evidence answers a business customer's questions on SOC 2 Type II readiness, PCI DSS SAQ A, POPIA and GDPR.

## 2. The parts

| Part | Where | What it does |
|---|---|---|
| The test suite | `project-library-global\test-suite\` | The method, the catalogue of 112 tests, the conformance checks, the rule soundness register, two tools and four templates. It serves every Mybizz application. |
| Each step's test specification | `{step}-test-spec.md`, the seventh file of every step | Names the catalogue tests the step runs and what happens on failure. |
| Each app's tests | `tests\` in each app's repository | The app's own logic, integration and security tests, built from the templates and its test plan. |
| The evidence | `pdlf-outputs\{step}\` in the project library | The saved output of every test; receipts take their counts from it. |

## 3. Where tests run

The Hobby plan gives App 1 one database and no test environment. Tests therefore run first on the Anvil App Server on the developer's computer, starting from an empty database each time, so nothing live is touched and attacks can be tried freely. Only what needs Anvil's hosted service (sign-up emails, real webhooks, scheduled tasks, headers) is tested on hosted App 1, with `TEST_` data that is removed afterwards. Access rules are always proven by signing in as each role through a client connection.

## 4. How each phase is tested

- **Phase A:** the orchestrator refuses unapproved gates and missing dependencies; each entry starts healthy.
- **Phase B:** the test environment works, and the plans are complete: measurable success, data and law settled, test plan, access matrix and threat model written.
- **Phase C:** the schema matches the design and obeys the data rules; tickets carry their tests; designs, wireframes and screens are readable and conform.
- **Phase D:** forms obey the UI rules; at Step 34 the skeleton passes every static check and implements the threat model before any code is written.
- **Phase E:** each feature is built test-first and proven through logic, integration, access, attack and browser tests, reviewed independently, and signed off by the developer.
- **Phase F:** the release is proven, backed up and reversible; every client instance is checked; health is watched; every escaped fault becomes a test.

## 5. When a test fails

At Step 35 a failure stops the work until it is fixed. From Step 35A on, it is recorded in the ledger, triaged at Step 39 and fixed at Step 35. Every fixed fault gets a permanent test. No gate passes while a finding is open.

## 6. What has to happen

1. The developer approves installing the test tools listed in [[[default:test-suite/ts-method]]](C:/dev/project-library-global/test-suite/ts-method.md).
2. The suite is proven on the first application PDLF builds, the Daily Intentions Tracker in `mb-5-pdlf`: test PR-09 at Step 11 proves the test environment, and each later step proves its own tests. No other application relies on the suite before then.
3. Each entry of [[[default:test-suite/ts-rule-soundness-register]]](C:/dev/project-library-global/test-suite/ts-rule-soundness-register.md) is corrected at its source with the developer's approval.

## Why it works this way

- **Level 2 with selected Level 3,** because the costliest failures (a stolen owner account, a forged payment, an unrecorded change to money) get extra protection and the rest gets the standard level.
- **Local first,** because the Hobby plan has no test database and attacks must never hit a hosted service.
- **Saved evidence,** because a claimed pass proves nothing, and because evidence kept over time is what audits and customers ask for.
- **One catalogue,** because a test used at many steps must be the same test everywhere.
