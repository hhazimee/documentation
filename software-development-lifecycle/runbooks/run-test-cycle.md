# Run Test Cycle

## Purpose

This runbook guides a QA Lead through a complete test cycle, from environment preparation and test execution through regression testing and defect tracking. Follow each step in order to ensure thorough coverage and a reliable release decision.

---

## Prerequisites

- [ ] Code merged to `develop` with passing CI (Phase 5 exit criteria met)
- [ ] Test environment (staging) available and configured
- [ ] [Test plan](../templates/test-plan.md) reviewed and approved
- [ ] Test data prepared and loaded; test accounts with appropriate roles provisioned
- [ ] API specification and acceptance criteria available
- [ ] Access to project tracker for defect logging

---

## Step 1: Execute Test Cycle

### 1.1 Prepare the Test Environment

1. Deploy latest `develop` (or release branch) to staging.
2. Run database migrations on the staging database.
3. Load or reset test data to the standard data set.
4. Verify all services via health checks (API, database, Redis, MQTT, external sandboxes).

- [ ] Health check endpoint returns 200
- [ ] Database, Redis, and MQTT broker connectivity verified
- [ ] External sandboxes responding (payment gateway, email, SMS)

> **IF** any health check fails **THEN** raise an infra ticket, notify Tech Lead, and do not proceed.

### 1.2 Run Smoke Tests

Execute the smoke test suite against staging:

| Test | Expected Result |
|------|-----------------|
| Health check endpoint | 200 OK |
| Login with test credentials | JWT token returned |
| List rentals (authenticated) | 200 with rental data |
| Create a rental | 201 Created |
| View dashboard | 200 with data |

- [ ] All smoke tests pass

> **IF** any smoke test fails **THEN** STOP. Fix the deployment issue and escalate to Tech Lead.

### 1.3 Review Defects and Obtain Sign-Off

After all testing steps are complete, return here to finalize:

1. Compile all defects found during the cycle.
2. Review the defect list with Tech Lead and Product Owner.
3. Complete the [Test Summary Report](../templates/test-summary-report.md).
4. Obtain QA sign-off, then [UAT sign-off](../templates/uat-sign-off.md) from Product Owner.

---

## Step 2: Write Integration Tests

Use this step when new or changed features require integration test coverage.

### 2.1 Identify Test Cases per Endpoint

| Category | What to Test |
|----------|-------------|
| Happy path | Valid request returns expected response |
| Authentication | Missing or invalid token returns 401 |
| Authorization | Cross-user access returns 403 |
| Validation | Invalid input returns 400 with error details |
| Not found | Non-existent resource returns 404 |
| Conflict | Duplicate operation returns 409 |

### 2.2 Set Up Test Infrastructure

1. Create or update the test file: `src/modules/<module>/__tests__/<module>.integration.test.ts`.
2. Configure `beforeAll`/`afterAll` for database setup and teardown.
3. Configure `beforeEach` to truncate tables so tests are isolated.
4. Create seed helpers in `src/test/seeds.ts` for each entity under test.

### 2.3 Write Tests

1. **Happy path** -- Arrange-Act-Assert: seed data, call the endpoint, assert status, body, and DB state.
2. **Error paths** -- cover 400, 401, 403, 404, and 409 scenarios.
3. **Authorization** -- verify User A cannot access or modify User B's resources (IDOR prevention).
4. **Pagination** -- confirm `page`, `per_page`, totals, and empty result sets.

### 2.4 Run and Verify

```bash
npm run test:integration -- --coverage
```

- [ ] All tests pass and coverage meets threshold
- [ ] No shared state between tests (random order passes)
- [ ] Tests execute in CI on every PR

> **IF** coverage is below threshold **THEN** flag to Tech Lead for developer action.

---

## Step 3: Write System Tests

Validate end-to-end user journeys against staging.

### 3.1 Identify Critical User Journeys

Map journeys from requirements to SRS IDs (e.g., create and manage a rental, process an overdue rental, equipment lifecycle).

### 3.2 Write Test Cases

Use the [Test Case Template](../templates/test-case.md). Each case needs: Test ID (`SYS-TC-XXX`), title, priority, preconditions, numbered steps with exact actions, expected result per step, and cleanup procedure.

### 3.3 Prioritize and Execute

Execute in priority order (Critical/High = 100% every cycle, Medium = release cycles, Low = quarterly). Record actual results alongside expected results. Place automated tests in `tests/system/<journey>.system.test.ts`.

> **Pass** -- mark and proceed. **Fail** -- capture evidence, log defect via [Defect Report](../templates/defect-report.md), continue. **Blocked** -- document blocker, revisit when unblocked.

### 3.4 Clean Up Test Data

Delete test-created data via API, reset modified records, and verify staging is clean.

---

## Step 4: Perform Regression Testing

### 4.1 Determine Regression Scope

| Trigger | Scope |
|---------|-------|
| Feature merged to develop | Targeted (related features) |
| Bug fix deployed | Targeted + fixed area |
| Release branch / major refactor / DB migration / major dep update | Full suite |

> **IF** unsure of scope **THEN** run the full suite -- missing a regression costs more than extra tests.

### 4.2 Run Automated Regression Tests

```bash
npm run test:regression                                    # Full suite
npm run test:regression -- --testPathPattern="<module>"    # Targeted
```

- [ ] Automated regression suite executed
- [ ] Results recorded and failures identified

### 4.3 Execute Manual Regression Tests

Focus on features adjacent to the changed area, features sharing data with it, and critical smoke-test paths.

### 4.4 Compare Results and Handle Failures

| Result | Action |
|--------|--------|
| All tests pass | Regression complete. Proceed. |
| Failure in changed area | Likely new bug. Log defect, fix before proceeding. |
| Failure in unchanged area | Regression. Log as High severity minimum. |
| Previously failing test now passes | Verify expected. Document. |
| Flaky test | Log defect. Investigate root cause. Do not ignore. |

- [ ] All regression failures logged (severity >= High)
- [ ] Developer who introduced the change notified

> **IF** regression failure found **THEN** block the release until resolved and re-tested.

### 4.5 Update the Regression Suite

Add tests for new features, remove or update tests for changed/removed features, flag flaky tests.

---

## Step 5: Report and Track Defects

### 5.1 Reproduce and Classify

1. Reproduce the failure at least twice; document reproduction rate.
2. Confirm it is a code bug, not an environment issue.
3. Classify severity per the [Defect Severity Reference](../references/defect-severity.md):

| Severity | Definition | SLA |
|----------|-----------|-----|
| Critical | System unusable, data loss, security breach | 4 hours |
| High | Major feature broken, no workaround | 1 business day |
| Medium | Feature broken, workaround exists | Current sprint |
| Low | Cosmetic or minor inconvenience | Next sprint / backlog |

> **IF** Critical **THEN** escalate to Tech Lead and PM immediately.

### 5.2 Write and Submit the Defect Report

Complete the [Defect Report Template](../templates/defect-report.md):

- [ ] Clear title, severity, environment (staging / test / local)
- [ ] Exact numbered steps to reproduce
- [ ] Expected result and actual result
- [ ] Test case reference, screenshots, API payloads, or logs attached

Submit in the project tracker. Link to the failing test case and related feature ticket.

### 5.3 Triage

| Decision | Criteria |
|----------|----------|
| Fix now | Critical or High. Blocks release or testing. |
| Fix this sprint | Medium. Can fix alongside other work. |
| Backlog | Low. Not blocking. |
| Won't fix | Not a bug, or cost exceeds impact. Document rationale. |
| Duplicate | Same issue already reported. Link and close. |

### 5.4 Track Progress and Re-Test

Lifecycle: `New > Triaged > Assigned > In Progress > Fixed > Re-test > Closed`

1. Monitor SLA compliance daily.
2. When a fix is deployed, execute the original reproduction steps and run related regression tests.

> **Fix works** -- close with verification note. **Fix fails** -- reopen with details. **Fix introduces new issue** -- log new defect, link to original.

---

## Outputs Checklist

- [ ] Staging environment deployed and smoke-tested
- [ ] Integration tests executed with passing coverage
- [ ] System test cases written, prioritized, and executed
- [ ] Regression tests executed (automated and manual)
- [ ] All defects logged using [Defect Report Template](../templates/defect-report.md)
- [ ] All Critical/High defects resolved and re-tested
- [ ] [Test Summary Report](../templates/test-summary-report.md) completed
- [ ] [UAT Sign-Off](../templates/uat-sign-off.md) obtained (if applicable)
- [ ] Release approval granted

---

## Tips

- **Run smoke tests first.** They catch deployment-level problems before you invest hours in deeper testing.
- **Log defects immediately.** Do not batch them -- context fades quickly.
- **Always include reproduction steps.** Reports without steps get sent back, wasting time.
- **Prioritize ruthlessly.** Critical and High test cases first. Time-box lower-priority work.
- **Keep tests isolated.** No shared mutable state. Use `beforeEach` resets and API-driven data creation.
- **Compare regression results to the previous baseline.** A new failure in an unchanged area warrants High severity.
- **Do not ignore flaky tests.** They mask real failures. Log them as defects.
- **Block the release on regressions.** Never ship with a known regression. When in doubt, run the full suite.
- **Clean up staging after every cycle.** The next tester will thank you.
