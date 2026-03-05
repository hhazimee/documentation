# Implement Feature

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-DEV-001 |
| **Owner** | Developer |
| **Accountable** | Developer |
| **SLA** | 1-5 business days per feature (varies by complexity) |
| **Escalation** | Tech Lead (technical blockers), Product Owner (scope questions) |
| **Last Verified** | 2026-03-05 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Ticket/story assigned and in "In Progress" status
- [ ] Related Detailed Design Document (DDD) reviewed and approved
- [ ] Development environment set up and verified (see [Setup Development Environment](./setup-dev-environment.md))
- [ ] Acceptance criteria defined in ticket

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Acceptance criteria unclear or missing | STOP. Request clarification before writing code. | Product Owner |
| DDD not approved | STOP. Do not implement against unapproved design. | Tech Lead |
| Design conflicts with existing architecture | STOP. Raise architecture concern. | Tech Lead |
| Scope change discovered mid-implementation | STOP. Reassess effort and ticket scope. | Product Owner |

---

## PROCEDURE

### Step 1: Review Requirement and Design

| Action | Owner | SLA |
|--------|-------|-----|
| Read ticket description and acceptance criteria | Developer | 30 min |
| Read related DDD, API spec, and data model | Developer | 30 min |
| Identify which SWR requirements the ticket fulfills | Developer | 15 min |

- [ ] Ticket description and acceptance criteria understood
- [ ] DDD, API spec, and data model reviewed
- [ ] SWR requirement traceability confirmed

> **IF** requirement is unclear **THEN** ask Tech Lead or Business Analyst before proceeding
> **ELSE** proceed to Step 2

### Step 2: Create Feature Branch

| Action | Owner | SLA |
|--------|-------|-----|
| Check out and pull latest develop branch | Developer | 5 min |
| Create feature branch using naming convention | Developer | 5 min |

```bash
git checkout develop
git pull origin develop
git checkout -b feature/TICKET-XXX-short-description
```

- [ ] Branch created from latest develop
- [ ] Branch name follows convention: `feature/TICKET-XXX-description`

### Step 3: Write Failing Tests (TDD Red Phase)

| Action | Owner | SLA |
|--------|-------|-----|
| Write unit tests for expected behavior | Developer | 1-4 hours |
| Run tests and confirm all fail | Developer | 10 min |

- [ ] Tests cover happy path from design
- [ ] Tests cover error cases from design
- [ ] All new tests fail (red phase confirmed)

> **IF** expected behavior is ambiguous **THEN** refer to DDD; escalate to Tech Lead if still unclear
> **ELSE** proceed to Step 4

### Step 4: Implement Code (TDD Green Phase)

| Action | Owner | SLA |
|--------|-------|-----|
| Write minimum code to pass tests | Developer | 2-8 hours |
| Run tests and confirm all pass | Developer | 10 min |

- [ ] All new tests pass (green phase confirmed)
- [ ] Implementation matches DDD specification
- [ ] No hardcoded values that should be configuration

> **IF** implementation requires deviating from DDD **THEN** STOP. Escalate to Tech Lead for design amendment.
> **ELSE** proceed to Step 5

### Step 5: Add Edge Case Tests

| Action | Owner | SLA |
|--------|-------|-----|
| Write tests for boundary conditions and error cases | Developer | 1-2 hours |
| Run tests and confirm all pass | Developer | 10 min |

- [ ] Negative/invalid input tests added
- [ ] Boundary value tests added
- [ ] Precision/rounding tests added (if applicable)
- [ ] All edge case tests pass

### Step 6: Run Full Test Suite

| Action | Owner | SLA |
|--------|-------|-----|
| Execute full test suite | Developer | 15 min |

```bash
npm test
```

- [ ] All tests pass
- [ ] No skipped tests

> **IF** unrelated tests fail **THEN** investigate; escalate to Tech Lead if caused by environment or shared dependency
> **ELSE** proceed to Step 7

### Step 7: Run Linter

| Action | Owner | SLA |
|--------|-------|-----|
| Execute linter on codebase | Developer | 10 min |
| Fix all linting errors | Developer | 30 min |

```bash
npm run lint
```

- [ ] Zero linting errors

> **IF** a lint rule must be disabled **THEN** get Tech Lead approval before suppressing
> **ELSE** proceed to Step 8

### Step 8: Perform Self-Review

| Action | Owner | SLA |
|--------|-------|-----|
| Run diff against develop and review all changes | Developer | 30 min |
| Verify each file against design document | Developer | 30 min |

```bash
git diff develop
```

- [ ] Code matches DDD specification
- [ ] Error handling covers all design scenarios
- [ ] Naming follows [coding standards](../standards/coding-and-git.md)
- [ ] No hardcoded values that should be configuration
- [ ] No console.log or debug code left behind
- [ ] No secrets or sensitive data in code
- [ ] No commented-out code

### Step 9: Commit Changes

| Action | Owner | SLA |
|--------|-------|-----|
| Stage relevant files | Developer | 5 min |
| Commit with conventional commit message | Developer | 10 min |

```bash
git add <files>
git commit -m "feat(module): short description

Implements SWR-XXX. <Brief explanation of what and why>.

Refs: TICKET-XXX"
```

- [ ] Commit message follows conventional commit format
- [ ] Commit references ticket and SWR IDs

### Step 10: Push and Create Pull Request

| Action | Owner | SLA |
|--------|-------|-----|
| Push feature branch to origin | Developer | 5 min |
| Create PR using PR template | Developer | 15 min |

```bash
git push -u origin feature/TICKET-XXX-short-description
```

- [ ] PR created using [PR template](../templates/pull-request.md)
- [ ] PR description includes: what changed, why, how tested
- [ ] PR linked to ticket

### Step 11: Address Review Feedback

| Action | Owner | SLA |
|--------|-------|-----|
| Read all review comments | Developer | 30 min |
| Fix blocking issues | Developer | 1-4 hours |
| Respond to each comment | Developer | 30 min |
| Push fixes as new commits | Developer | 15 min |

- [ ] All blocking comments resolved
- [ ] Each comment responded to
- [ ] Fixes pushed as new commits (no force-push during review)

> **IF** blocking changes were made **THEN** request re-review
> **ELSE IF** only non-blocking suggestions addressed **THEN** notify reviewer
> **ELSE** await approval

### Step 12: Merge to Develop

| Action | Owner | SLA |
|--------|-------|-----|
| Squash merge into develop | Developer | 5 min |
| Delete feature branch | Developer | 2 min |
| Verify CI pipeline passes on develop | Developer | 15 min |

- [ ] PR approved by reviewer
- [ ] Squash merged into develop
- [ ] Feature branch deleted
- [ ] CI pipeline green on develop

> **IF** CI fails after merge **THEN** investigate immediately; revert if not resolvable within 30 min
> **ELSE** proceed to exit criteria

---

## Managing Technical Debt

When technical debt is discovered during feature work (code review findings, shortcuts taken under deadline, structural issues uncovered), follow this process to ensure it is tracked and addressed.

### Identify and Classify

Common sources: code review findings, sprint retrospectives, bug root-cause analysis, dependency audits (`npm audit`), performance monitoring, and disproportionate effort on simple features.

**Impact (1-5):** 1 = cosmetic, 2 = minor slowdown, 3 = moderate productivity hit, 4 = bugs/security concerns, 5 = blocks features or data loss risk.
**Effort (1-5):** 1 = < 2 hours, 2 = half to full day, 3 = 2-3 days, 4 = 1 sprint, 5 = multiple sprints.
**Priority** = Impact / Effort.

> **IF** Impact = 5 and relates to security vulnerability **THEN** escalate to Tech Lead immediately.

### Record and Decide

1. Create an entry in the [Technical Debt Register](../templates/technical-debt-register.md) with: ID (TD-XXX), title, description, category, scores, affected components, date, identified by, status (Open).
2. Determine action:

| Priority Score | Action |
|---------------|--------|
| >= 3.0 | Schedule in current or next sprint |
| 1.5 - 2.9 | Add to backlog, schedule within 2-3 sprints |
| 1.0 - 1.4 | Add to backlog, address opportunistically |
| < 1.0 | Accept the debt. Document decision. Review quarterly. |

### Resolve

1. Create branch: `refactor/TD-XXX-short-description`
2. Write tests if none exist for the affected code.
3. Implement the fix. Run full test suite.
4. Create PR referencing TD-XXX using the [PR template](../templates/pull-request.md). Follow the standard code review process per the [code review standard](../standards/code-review.md).
5. After merge, update the register entry status to Resolved.

**Sprint allocation:** normal sprints 10-20% capacity for debt; debt-focused sprints (quarterly if debt grows) 50%+; pre-release sprints no debt work unless blocking release.

**Metrics (review in retrospectives):** total open items trending down, critical items (impact 4-5) zero older than 2 sprints, 1-2 items resolved per sprint.

---

## EXIT CRITERIA

- [ ] Feature implemented matching DDD specification
- [ ] All unit tests pass (including edge cases)
- [ ] Linter passes with zero errors
- [ ] Code reviewed and approved per [code review standard](../standards/code-review.md)
- [ ] Merged to develop branch
- [ ] CI pipeline green on develop
- [ ] Feature branch deleted
- [ ] Any technical debt discovered during implementation recorded in the [Technical Debt Register](../templates/technical-debt-register.md)

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Feature code | N/A | Source repository (develop branch) |
| Unit tests | N/A | Source repository (develop branch) |
| Pull request | [PR Template](../templates/pull-request.md) | GitHub |
| Conventional commit | N/A | Git history |
| Technical Debt Register entry (if applicable) | [Technical Debt Register](../templates/technical-debt-register.md) | Project documentation |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Pull Request Template | Template | [../templates/pull-request.md](../templates/pull-request.md) |
| Code Review Checklist | Template | [../templates/code-review-checklist.md](../templates/code-review-checklist.md) |
| Technical Debt Register | Template | [../templates/technical-debt-register.md](../templates/technical-debt-register.md) |
| Coding and Git Standards | Standard | [../standards/coding-and-git.md](../standards/coding-and-git.md) |
| Code Review Standard | Standard | [../standards/code-review.md](../standards/code-review.md) |
| Build and Verify Phase | Phase | [../phases/3-build-and-verify.md](../phases/3-build-and-verify.md) |
| Setup Development Environment | Runbook | [./setup-dev-environment.md](./setup-dev-environment.md) |
| Conduct Code Review | Runbook | [../standards/code-review.md](../standards/code-review.md) |
