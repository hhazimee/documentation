# Code Review Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-CR-001 |
| **Compliance** | Mandatory |
| **Owner** | Tech Lead |
| **Last Updated** | 2026-03-05 |

---

## 1. Purpose

Code review is a mandatory quality gate that catches defects, enforces design adherence,
and spreads knowledge across the team before code reaches a shared branch. Every pull
request must be reviewed and approved by at least one qualified reviewer before merge.
This standard defines the policy, process, and expectations for all code reviews.

---

## 2. Code Review Policy

### When Reviews Are Required

All code merging to `develop` or `main` requires at least one approval. No exceptions.

### Scaling by Team Size

| Team Size | Approvals for `develop` | Approvals for `main` | Notes |
|-----------|------------------------|---------------------|-------|
| 1-2 devs | 1 | 1 | Tech Lead reviews architecture and security changes only |
| 3-5 devs | 1 | 2 | Standard requirements apply |
| 6+ devs | 2 | 2 | Domain-specific reviewers assigned |

### Who Reviews What

| Change Type | Required Reviewer(s) |
|-------------|---------------------|
| Architecture (new component, new dependency, schema change) | Tech Lead + Senior Developer |
| Security (auth, input validation, crypto) | Tech Lead (required) |
| Standard feature or bug fix | Any peer developer |
| Documentation only | Any team member |

### Turnaround Time

| Metric | SLA |
|--------|-----|
| First review from PR submission | 4 hours |
| Full review completion | 1 business day |
| Re-review after changes | 2 hours |

### PR Size Limits

| Lines Changed | Action |
|---------------|--------|
| < 100 | Submit as-is |
| 100 - 400 | Submit as-is |
| 400+ | Split into multiple PRs (data model, service, API, integration) |

---

## 3. Review Process

Follow these steps in order. Use the [Code Review Checklist](../templates/code-review-checklist.md)
to track progress.

### Step 1: Validate the PR

Before reviewing any code, confirm the PR is ready:

- [ ] PR submitted with completed [PR template](../templates/pull-request.md)
- [ ] Description includes: what changed, why, and how it was tested
- [ ] CI pipeline passing on the PR branch
- [ ] Reviewer is not the PR author

**If the PR description is incomplete or CI is failing, stop. Send it back to the author.**

### Step 2: Read the Context

- [ ] Read the PR title, description, and linked ticket (15 min)
- [ ] Open related design document or API spec (10 min)
- [ ] Note expected behavior, data model, and error handling (15 min)

If no design document exists for a significant change, escalate to Tech Lead.

### Step 3: Review the Diff

Review in this order -- tests first, then implementation:

1. **Test files first** -- understand expected behavior (20 min)
2. **Implementation files** -- verify against tests and design (30 min)
3. **Configuration and infrastructure** -- migrations, CI, env changes (15 min)

### Step 4: Evaluate Against Review Criteria

Walk through Section 4 (What to Check) below. Use the checklist template to record findings.

### Step 5: Write Feedback

- [ ] Use severity prefixes on every comment (see Section 5)
- [ ] Explain "why" for each comment, not just "fix this"
- [ ] Offer alternatives for every blocking issue
- [ ] Acknowledge good code -- call out clean solutions

### Step 6: Submit Decision

| Decision | When to Use |
|----------|-------------|
| **Approve** | No blocking issues. Code is ready to merge. |
| **Request Changes** | One or more blocking issues that must be fixed. |
| **Comment** | Questions or observations only. Not blocking. |

### Step 7: Follow Up (if changes requested)

- [ ] Verify all blocking feedback was addressed (2 hours SLA)
- [ ] Re-review only the changed code (30 min)
- [ ] Approve when all blocking issues are resolved

If the author disagrees with blocking feedback, discuss first. Escalate to Tech Lead
if unresolved within one round of discussion.

---

## 4. What to Check

### Correctness

- [ ] Code does what the design specifies
- [ ] Edge cases from the design are handled
- [ ] Acceptance criteria from the ticket are satisfied
- [ ] Error paths return meaningful messages

### Security

- [ ] Input validation at all boundaries
- [ ] Parameterized queries -- no SQL injection
- [ ] Auth checks on every protected endpoint
- [ ] No secrets, tokens, or credentials in code
- [ ] OWASP Top 10 risks considered

### Performance

- [ ] No N+1 queries
- [ ] Pagination on list endpoints
- [ ] Appropriate use of database indexes
- [ ] No unnecessary computation in hot paths

### Readability

- [ ] Clear, descriptive naming
- [ ] Reasonable function length (single responsibility)
- [ ] Understandable by a developer new to the codebase
- [ ] Comments where intent is not obvious from the code

### Tests

- [ ] Unit tests present and meaningful
- [ ] Tests cover happy path and error cases
- [ ] Tests verify behavior, not implementation details
- [ ] Coverage meets the project threshold

### Standards Compliance

- [ ] Naming follows project conventions
- [ ] Error handling follows the standard pattern
- [ ] Logging follows project guidelines
- [ ] Commits follow conventional commit format

---

## 5. Review Etiquette

### Comment Severity Prefixes

Every review comment must use one of these prefixes:

| Prefix | Meaning | Author Must |
|--------|---------|-------------|
| `[blocking]` | Must fix before merge | Fix it and reply with what changed |
| `[suggestion]` | Would improve code, not required | Implement or explain why not |
| `[nit]` | Minor style or preference | Fix if easy; acknowledge otherwise |
| `[question]` | Seeking clarification | Answer it |

### Do and Do Not

| Do | Do Not |
|----|--------|
| Be specific and constructive | Be vague ("this is wrong") |
| Focus on the code, not the person | Make it personal ("you always...") |
| Ask questions when you are unsure | Assume bad intent |
| Suggest concrete alternatives | Just say "fix this" |
| Praise clean, well-tested code | Only leave negative feedback |
| Respond within the SLA | Let PRs sit for days |
| Approve when satisfied | Withhold approval over nits or style preferences |

### Approval Guidance

| Situation | Action |
|-----------|--------|
| All blocking issues resolved, tests present | Approve |
| Style issue already enforced by linter | Approve -- do not block on linter-enforced style |
| Author declined a non-blocking suggestion with explanation | Approve |
| Correctness bug or security vulnerability found | Request Changes with a clear explanation |

---

## 6. Common Review Comments

Patterns that reviewers catch most often. Look for these first.

| Pattern | Example Comment |
|---------|----------------|
| Missing input validation | `[blocking] This endpoint accepts user input without validation. Add schema validation before processing.` |
| N+1 query | `[blocking] This loops over results and queries the DB each iteration. Use a JOIN or batch fetch.` |
| Hardcoded secret | `[blocking] API key is hardcoded. Move to environment variable and reference via config.` |
| Missing error handling | `[blocking] This async call has no error handling. Add try/catch and return a meaningful error response.` |
| Overly broad catch | `[suggestion] Catching all exceptions hides bugs. Catch the specific exception types you expect.` |
| Dead code | `[nit] This function is unused after the refactor. Remove it to keep the codebase clean.` |
| Magic number | `[suggestion] Replace 86400 with a named constant like SECONDS_PER_DAY for clarity.` |
| Missing test for error path | `[blocking] Happy path is tested but there is no test for the case where the service returns a 404.` |
| Large function | `[suggestion] This function is 80+ lines. Consider extracting the validation logic into a helper.` |
| Inconsistent naming | `[nit] The rest of the codebase uses camelCase for variables. This file mixes snake_case.` |

---

## 7. Metrics

Track these to improve review quality over time. Measurement is optional for small teams
but recommended once the team reaches 3+ developers.

| Metric | Target | How to Measure |
|--------|--------|----------------|
| Time to first review | < 4 hours | PR submission timestamp to first comment |
| Review turnaround (full cycle) | < 1 business day | PR submission to final approval |
| PR size | < 400 lines changed | CI check or PR analytics |
| Defect catch rate | Trending upward | Bugs found in review vs. bugs found in QA/production |
| Review comment resolution | 100% blocking resolved | PR merge gate |
| Re-review cycle time | < 2 hours | Time from author update to re-review |

---

## Related Templates

- [Code Review Checklist](../templates/code-review-checklist.md)
- [Pull Request Template](../templates/pull-request.md)
- [Conduct Reviews Runbook](../runbooks/conduct-reviews.md)
