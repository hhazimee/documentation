# Phase 3: Build & Verify (Development + Testing)

> **Purpose:** Transform approved designs into working, tested code through disciplined implementation following TDD practices. Verify that the built software meets the requirements defined in earlier phases and provide the evidence needed to approve a release.

---

## Entry Criteria

- [ ] Phase 2 (Design) gate passed
- [ ] ADD and DDD approved
- [ ] API specifications and data models finalized
- [ ] Development environment set up → [runbooks/setup-dev-environment.md](../runbooks/setup-dev-environment.md)
- [ ] Test environment available and configured
- [ ] Test data prepared

---

## Deliverables

| # | Document | Template | Required | Runbook |
|---|----------|----------|----------|---------|
| 1 | Source Code + Unit Tests | N/A (code) | All projects | [runbooks/implement-feature.md](../runbooks/implement-feature.md) |
| 2 | Pull Requests (using template) | [templates/pull-request.md](../templates/pull-request.md) | All projects | [runbooks/implement-feature.md](../runbooks/implement-feature.md) |
| 3 | Code Review Records | [templates/code-review-checklist.md](../templates/code-review-checklist.md) | All projects | [standards/code-review.md](../standards/code-review.md) |
| 4 | Test Plan | [templates/test-plan.md](../templates/test-plan.md) | Medium+ | [runbooks/run-test-cycle.md](../runbooks/run-test-cycle.md) |
| 5 | Test Cases | [templates/test-case.md](../templates/test-case.md) | All projects | [runbooks/run-test-cycle.md](../runbooks/run-test-cycle.md) |
| 6 | Defect Reports | [templates/defect-report.md](../templates/defect-report.md) | As needed | [runbooks/run-test-cycle.md](../runbooks/run-test-cycle.md) |
| 7 | Test Summary Report | [templates/test-summary-report.md](../templates/test-summary-report.md) | Medium+ | [runbooks/run-test-cycle.md](../runbooks/run-test-cycle.md) |
| 8 | UAT Sign-Off | [templates/uat-sign-off.md](../templates/uat-sign-off.md) | All projects | [runbooks/run-test-cycle.md](../runbooks/run-test-cycle.md) |
| 9 | Technical Debt Register | [templates/technical-debt-register.md](../templates/technical-debt-register.md) | Ongoing | [runbooks/implement-feature.md](../runbooks/implement-feature.md) |

**PlantUML diagrams:** None new required (update existing diagrams if design changed during implementation)

---

## Key Activities

### Development

1. **Pick ticket** from sprint backlog; read ticket, DDD, API spec, and data model
2. **Create feature branch** from `develop`
3. **Write failing tests first** (TDD: Red-Green-Refactor)
4. **Implement** the minimum code to pass tests, then add edge-case tests
5. **Run full test suite + linter** (`npm test` and `npm run lint`)
6. **Self-review** the diff, commit with conventional message
7. **Open PR** (one ticket = one PR, under 400 lines of diff)
8. **Address review feedback** with new commits (no force-push during review)
9. **Squash merge** to `develop`; verify CI passes after merge

Detailed steps: [Implement Feature Runbook](../runbooks/implement-feature.md)

### Testing

1. **Write test plan** -- scope, approach, environments, test data, schedule
2. **Write test cases** linked to SWR requirements (traceability via RTM)
3. **Execute integration tests** -- API contracts, data flow, auth enforcement
4. **Execute system tests** -- end-to-end user workflows in staging environment
5. **Report defects** formally using the defect report template (steps to reproduce, request/response, environment)
6. **Run regression suite** before every merge and before release
7. **Perform performance and security testing** (for releases)
8. **Conduct UAT** with Product Owner against acceptance criteria
9. **Write test summary report** with go/no-go recommendation

Detailed steps: [Execute Test Cycle Runbook](../runbooks/run-test-cycle.md)

---

## Standards

- [Coding & Git Standard](../standards/coding-and-git.md)
- [Code Review Standard](../standards/code-review.md)
- [Testing Standard](../standards/testing.md)

---

## Testing Pyramid (Quick Reference)

| Level | Target Ratio | Quantity | Speed | Catches |
|-------|-------------|----------|-------|---------|
| Unit | ~70% | 200-500 tests | < 30s total | Logic errors, edge cases, calculation bugs |
| Integration | ~20% | 50-100 tests | < 5min total | API contract issues, data flow, auth gaps |
| System/E2E | ~10% | 20-30 tests | < 30min total | Workflow breaks, cross-module issues |

**Where should this test go?**

| Question | If Yes | If No |
|----------|--------|-------|
| Can I test with just the function/class? | Unit test | Continue below |
| Does it need a real database or API? | Integration test | Continue below |
| Does it span multiple modules or API calls? | System test | Unit or integration |
| Does it need external services (payment, email)? | System test (staging) | Integration with mocks |

---

## Top 5 Pitfalls

| # | Pitfall | One-Line Fix |
|---|---------|-------------|
| 1 | **Coding without reading the design** -- eagerness to start leads to rework | Read the DDD, API spec, and data model before writing any code |
| 2 | **Writing tests after code** -- tests become afterthought, coverage gaps appear | Write the failing test first (TDD: Red-Green-Refactor) |
| 3 | **Testing only the happy path** -- error scenarios missed until production | Write at least one error-path test for every happy-path test |
| 4 | **Large PRs (400+ lines)** -- slow reviews, hidden bugs, merge conflicts | One ticket = one PR; split by layer if needed |
| 5 | **Flaky or ignored test failures** -- erodes trust in the test suite | Fix flaky tests immediately; zero tolerance for skipped failures |

---

## Exit Criteria / Phase Gate

- [ ] All features implemented per SRS
- [ ] Implementation matches DDD specifications
- [ ] Code review completed for all PRs (at least one reviewer)
- [ ] Unit test coverage >= 80% (business logic), >= 90% (critical paths)
- [ ] Linter passes with no warnings
- [ ] All planned test cases executed
- [ ] All critical and high-severity defects resolved
- [ ] Regression tests pass
- [ ] Performance benchmarks met
- [ ] Security scan passes with no critical/high findings
- [ ] Test summary report approved by QA Lead
- [ ] UAT signed off by Product Owner
- [ ] Technical debt logged in register
- [ ] CI pipeline green on `develop`

---

## Scaling Notes

| Project Size | Skip/Simplify |
|-------------|---------------|
| Small (< 2 weeks) | Skip formal test plan. Test cases can be checklist. Informal code review OK. |
| Medium (2-8 weeks) | Full test plan. Formal code reviews. Test summary report required. |
| Large (8+ weeks) | All deliverables required. Dedicated QA involvement. Performance and security testing mandatory. |

---

## Roles

| Role | Development Responsibility | Testing Responsibility |
|------|---------------------------|----------------------|
| Developer | Implements features via TDD, creates PRs, addresses feedback | Writes unit/integration tests, fixes defects |
| Tech Lead | Reviews architecture-impacting changes, resolves disputes | Triages defects, approves risk acceptance |
| QA Engineer | Verifies testability requirements | Writes/executes system tests, reports defects |
| QA Lead | Defines testability requirements | Approves test plans, signs off on testing |
| Product Owner | Clarifies requirements | Verifies acceptance criteria, provides UAT sign-off |

---

## Next Phase

→ [Phase 4: Ship & Run](4-ship-and-run.md)

---

## Previous Phase

← [Phase 2: Design](2-design.md)
