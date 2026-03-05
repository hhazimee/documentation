# Artifacts Checklist

| Field | Value |
|-------|-------|
| **Reference ID** | REF-AC-001 |
| **Use When** | Verifying completeness of deliverables at each phase gate |
| **Last Updated** | 2026-03-05 |

---

All deliverables across the 4 SDLC phases in one view. Use this to verify completeness at each phase gate.

## Phase 1: Define

Covers business analysis, requirements engineering, and requirements baseline.

| Artifact | Owner | Required | Phase Gate Check |
|----------|-------|----------|-----------------|
| [Business Case](../templates/business-case.md) | Business Analyst | All | Approved by Project Sponsor |
| [Project Charter](../templates/project-charter.md) | Product Owner | All | Signed by Project Sponsor |
| Problem Statement | Business Analyst | All | Reviewed by Product Owner |
| [Stakeholder Register](../templates/stakeholder-register.md) | Business Analyst | All | Reviewed by Product Owner |
| Business Value Assessment | Business Analyst | Medium/Large | Approved by Project Sponsor |
| Communication Plan | Business Analyst | All | Reviewed by Product Owner |
| [Business Requirements Document (BRD)](../templates/business-requirements-document.md) | Business Analyst | All | Approved by Project Sponsor |
| Stakeholder Requirements Specification | Business Analyst | All | Included in BRD |
| [Software Requirements Specification (SRS)](../templates/software-requirements-specification.md) | Tech Lead | All | Approved by Tech Lead |
| [Use Case Document](../templates/use-case.md) | Business Analyst | Conditional | Required if user-facing interactions exist |
| [Requirements Traceability Matrix (RTM)](../templates/requirements-traceability-matrix.md) | Business Analyst | All | BR-to-SWR traceability complete |
| Requirements Validation Report | Business Analyst | All | Requirements confirmed complete, consistent, feasible, testable |
| Requirements Baseline Sign-off | Project Sponsor | All | Signed by Project Sponsor |

---

## Phase 2: Design

Covers system architecture and detailed component design.

| Artifact | Owner | Required | Phase Gate Check |
|----------|-------|----------|-----------------|
| [Architecture Description Document (ADD)](../templates/architecture-description-document.md) | Tech Lead | All | All viewpoints documented |
| System Context Diagram | Tech Lead | All | All external interactions shown |
| Component Diagram | Tech Lead | All | All modules, responsibilities, and interfaces |
| Deployment Diagram | Tech Lead | All | Infrastructure topology complete |
| Process/Sequence Diagrams | Tech Lead | Medium/Large | Top 5 critical scenarios covered |
| Development View | Tech Lead | Medium/Large | Repo structure and build pipeline documented |
| [Architecture Decision Records (ADRs)](../templates/architecture-decision-record.md) | Tech Lead | All | Minimum 5 decisions documented |
| Technology Stack Document | Tech Lead | All | All technologies justified |
| Architecture Review Record | System Architect | Medium/Large | Review findings addressed |
| [Detailed Design Document (DDD)](../templates/detailed-design-document.md) | Developer / Tech Lead | Per component | Internal structure and logic documented |
| [API Specification](../templates/api-specification.md) | Developer / Tech Lead | If REST API | Endpoints, schemas, auth defined |
| [Data Model](../templates/data-model-document.md) | Developer / Tech Lead | If owns data | Tables, relationships, indexes, migrations |
| UI Wireframes | UX Designer / Developer | If user-facing | Layout and interaction flows approved |
| Design Sequence Diagrams | Developer / Tech Lead | If 3+ component interactions | Runtime flows documented |
| Design Review Record | Tech Lead | All | Review conducted, findings addressed |
| Updated RTM (architecture + design refs) | Business Analyst | All | Design references traced to requirements |

---

## Phase 3: Build & Verify

Covers development, code review, testing, and quality gates.

### Per Feature / Ticket

| Artifact | Owner | Required | Phase Gate Check |
|----------|-------|----------|-----------------|
| Feature Branch | Developer | All | Follows `feature/TICKET-NNN-description` convention |
| Unit Tests | Developer | All | Coverage >= 80%, TDD, AAA structure |
| Implementation Code | Developer | All | Matches DDD, passes linter, no secrets |
| Conventional Commit(s) | Developer | All | `type(scope): description` format, references ticket |
| [Pull Request](../templates/pull-request.md) | Developer | All | Description, test plan, linked ticket, under 400 lines |
| [Code Review Record](../templates/code-review-checklist.md) | Code Reviewer | All | All blocking comments resolved |

### Per Sprint

| Artifact | Owner | Required | Phase Gate Check |
|----------|-------|----------|-----------------|
| [Test Plan](../templates/test-plan.md) | QA Engineer | All | Scope, approach, entry/exit criteria defined |
| [Test Cases](../templates/test-case.md) | QA Engineer | All | Traceable to requirements, clear steps and expected results |
| Integration Test Code | Developer | All | Happy path + error paths, runs in CI |
| Test Execution Results | QA Engineer | All | Pass/fail per case documented |
| [Defect Reports](../templates/defect-report.md) | QA Engineer | All | Severity classified, reproducible steps, environment noted |
| [Test Summary Report](../templates/test-summary-report.md) | QA Engineer | All | Metrics and go/no-go recommendation |
| [Updated Technical Debt Register](../templates/technical-debt-register.md) | Developer / Tech Lead | All | New items added, resolved items closed |
| Sprint Demo | Development Team | All | Working software demonstrated to stakeholders |

---

## Phase 4: Ship & Run

Covers release preparation, final testing, and production readiness.

### Release Artifacts

| Artifact | Owner | Required | Phase Gate Check |
|----------|-------|----------|-----------------|
| Release Branch | Tech Lead | All | `release/X.Y.Z` with version bumps |
| Release Tag | Tech Lead | All | Semantic version tag on `main` |
| Changelog | Tech Lead | All | Summary of all changes, approved by Product Owner |
| Release Test Plan | QA Lead | All | All test levels covered |
| Regression Test Results | QA Engineer | All | Full suite passed |
| Performance Test Report | QA Engineer | All | Benchmarks met, bottlenecks identified |
| Security Test Report | QA Engineer / Security | All | OWASP Top 10 covered, no critical/high findings |
| [UAT Sign-Off](../templates/uat-sign-off.md) | Product Owner | All | All acceptance criteria verified, signed |
| Release Test Summary | QA Lead | All | Go/no-go recommendation approved by Tech Lead + Product Owner |

---

## Summary -- Artifact Counts by Phase

| Phase | Required (All) | Conditional | Total |
|-------|---------------|-------------|-------|
| Phase 1: Define | 11 | 2 | 13 |
| Phase 2: Design | 8 | 8 | 16 |
| Phase 3: Build & Verify | 14 | 0 | 14 |
| Phase 4: Ship & Run | 9 | 0 | 9 |
| **Total** | **42** | **10** | **52** |

---

## Decision Tree -- Is the Phase Gate Ready?

```
FOR each phase:
  IF all "Required = All" artifacts are complete
    AND all conditional artifacts are complete (or exclusion justified)
    AND all artifacts meet quality criteria
    AND all approvals obtained
    THEN phase gate is READY
  ELSE
    THEN identify missing/unapproved artifacts -> complete before gate review
```

### Which Conditional Artifacts Apply?

```
Phase 1: Define
  IF system has user-facing interactions
    THEN Use Case Document is REQUIRED
  IF project scale is Medium or Large
    THEN Business Value Assessment is REQUIRED

Phase 2: Design
  IF component exposes a REST API
    THEN API Specification is REQUIRED
  IF component owns database tables
    THEN Data Model is REQUIRED
  IF component has a user-facing interface
    THEN UI Wireframes are REQUIRED
  IF component interacts with 3+ other components
    THEN Design Sequence Diagrams are REQUIRED
  IF project scale is Medium or Large
    THEN Process/Sequence Diagrams, Development View, and Architecture Review Record are REQUIRED
```

---

## Cross-References

| Document | Type | Link |
|----------|------|------|
| Glossary | Reference | [glossary.md](./glossary.md) |
| Defect Severity Reference | Reference | [defect-severity.md](./defect-severity.md) |
