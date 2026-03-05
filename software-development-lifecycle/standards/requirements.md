# Requirements Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-REQ-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Business Analyst / Tech Lead / QA Lead |
| **Verification Method** | Requirements baseline review, RTM audit, attribute completeness check |
| **Last Updated** | 2026-03-05 |

---

## 1. Purpose

Define the rules for engineering, classifying, tracing, and managing requirements across the software development lifecycle. All project teams follow these rules to produce requirements that are complete, testable, and traceable from business need through to verified implementation.

---

## 2. Requirements Engineering Process

### 2.1 Requirements Hierarchy

Requirements decompose through four levels. Each level uses a fixed ID prefix:

| Level | Prefix | Example | Owner | Approver |
|-------|--------|---------|-------|----------|
| Business Requirement | BR-XXX | BR-001 | Product Owner | Project Sponsor |
| Stakeholder Requirement | STK-XXX | STK-001 | Business Analyst | Product Owner |
| System Requirement | SYS-XXX | SYS-001 | BA / Tech Lead | Tech Lead |
| Software Requirement | SWR-XXX | SWR-001 | Tech Lead / Developer | Tech Lead |

Decomposition direction: **BR --> STK --> SYS --> SWR**. Every non-BR requirement must link to a parent. IDs are sequential and never reused. Cross-project requirements add a project prefix: `PROJECT-LEVEL-NUMBER`.

### 2.2 Mandatory Attributes

Every requirement carries these ten attributes:

| Attribute | Rule |
|-----------|------|
| Unique ID | Level prefix + sequential number |
| Title | Short descriptive name |
| Description | Clear, unambiguous statement |
| MoSCoW Priority | Must / Should / Could / Won't |
| Source | Origin of the requirement |
| Rationale | Why the requirement exists |
| Acceptance Criteria | Conditions that prove satisfaction |
| Status | Current lifecycle state |
| Parent ID | Link to parent requirement (except BR) |
| Version | Incremented on every change |

### 2.3 Lifecycle States

Valid states and who can transition:

| State | Authorized Role |
|-------|----------------|
| Draft | Business Analyst |
| Under Review | Business Analyst |
| Approved | Approval authority for the requirement level |
| Rejected | Approval authority for the requirement level |
| Implemented | Developer |
| Verified | QA Lead |
| Deferred | Product Owner |
| Retired | Product Owner |

### 2.4 Scaling Gate

| Project Size | Minimum Compliance |
|-------------|-------------------|
| Small (1-2 devs) | User stories with acceptance criteria in lieu of BRD; SRS equivalent required; RTM via Jira epic-to-story links |
| Medium (3-5 devs) | BRD, SRS, and RTM required; validation may be a single review session |
| Large (6+ devs) | Full compliance with all rules in this standard |

### 2.5 Templates

- [Business Requirements Document](../templates/business-requirements-document.md)
- [Software Requirements Specification](../templates/software-requirements-specification.md)

---

## 3. Requirements Classification

### 3.1 Functional vs Non-Functional

Every requirement is classified as one of:

- **Functional** -- defines what the system must do (behavior, features, operations).
- **Non-Functional** -- defines how the system must perform (quality attributes, constraints).

### 3.2 Non-Functional Categories

Each non-functional requirement is assigned exactly one category:

| Category | Must Include |
|----------|-------------|
| Performance | Measurable thresholds: response time, throughput, resource usage |
| Security | Specific controls: authentication, authorization, data protection, audit |
| Usability | Measurable UX criteria |
| Reliability | Availability, fault tolerance, or recoverability targets (numeric) |
| Scalability | Load or growth capacity numbers |
| Maintainability | Modularity, testability, or modifiability targets |
| Compliance | Specific regulation, law, or contractual citation |

### 3.3 Constraints

Constraints are a subset of non-functional requirements that restrict solution options. They originate from:

- **Regulatory** -- law, regulation, or industry standard (cite the specific reference).
- **Technical** -- architecture decisions, platform limitations, integration boundaries (reference the ADR or technical document).
- **Business** -- budget caps, timeline mandates, organizational policy.

Constraints use the same NFR categorization but must explicitly state the constraining factor and its source.

### 3.4 Priority Classification (MoSCoW)

| Priority | Meaning | Guideline |
|----------|---------|-----------|
| Must Have (M) | Essential for release; cannot be descoped | ~60% of scope |
| Should Have (S) | Important but deferrable with PO approval | ~20% of scope |
| Could Have (C) | Included only if time and capacity allow | ~20% of scope |
| Won't Have (W) | Explicitly excluded; documented to prevent scope creep | Documented in backlog |

### 3.5 Risk Classification

| Level | Action Required |
|-------|----------------|
| High | Spike or proof-of-concept completed; architecture review mandatory |
| Medium | Tech lead review; mitigation plan documented |
| Low | Standard development process |

### 3.6 Source Classification

Every requirement has at least one source tag:

- **Stakeholder** -- named person or group.
- **Regulatory** -- specific regulation cited.
- **Technical** -- constraint or ADR referenced.
- **Business** -- business objective referenced.

---

## 4. Requirements Traceability

### 4.1 Traceability Matrix (RTM) Columns

| Column | Populated By Phase |
|--------|-------------------|
| Requirement ID | Phase 2 |
| Requirement Description | Phase 2 |
| Source | Phase 2 |
| Parent Requirement | Phase 2 |
| Design Reference | Phase 4 |
| Code Reference | Phase 5 |
| Test Case ID | Phase 6 |
| Test Result | Phase 6 |
| Status | All phases |

### 4.2 Traceability Direction

- **Forward**: BR --> STK --> SYS --> SWR --> Design --> Code --> Test
- **Backward**: Test --> Code --> Design --> SWR --> SYS --> STK --> BR

Both directions are maintained. No orphan tests allowed (every test traces to a requirement).

### 4.3 Coverage Thresholds

| Metric | Target | Gate |
|--------|--------|------|
| Must Have requirements with linked test cases | 100% | Release blocked |
| Should Have requirements with linked test cases | 90% | Gap documented; PO accepts risk |
| Forward trace completeness (Must Have, BR to test) | 100% | Release blocked |
| Backward trace completeness (no orphan tests) | 100% | Orphan tests justified or removed |
| Implementation coverage (approved reqs with code refs) | 100% | Release blocked |

### 4.4 RTM Update Triggers

Update the RTM when any of these occur:

- Requirement added, modified, retired, or deleted
- Design artifact created or updated
- Code implemented against a requirement
- Test case created or executed
- Change request approved

### 4.5 Review Checkpoints

| Checkpoint | Reviewer | Blocks |
|-----------|----------|--------|
| Requirements baseline | BA + Product Owner | Phase 2 gate |
| Design review | Tech Lead | Phase 4 gate |
| Code review | Tech Lead + Developer | Phase 5 gate |
| Test readiness | QA Lead | Test execution |
| Release readiness | Product Owner + QA Lead | Release |

### 4.6 RTM Governance

- One authoritative copy (single source of truth).
- Version-controlled.
- Accessible to all project team members.

---

## 5. Elicitation Techniques

### 5.1 Technique Reference

| Technique | When to Use | Effort |
|-----------|------------|--------|
| Structured Interviews | Deep individual stakeholder needs; sensitive topics | Medium |
| Workshops (JAD) | Cross-functional alignment; conflict resolution; cross-departmental systems | High |
| Observation | Actual vs. stated workflows; stakeholders cannot articulate needs | Medium |
| Document Analysis | Existing system constraints; regulatory/compliance requirements; replacing existing system | Low |
| Prototyping | UI/UX requirements; user feedback; stakeholders cannot articulate needs | High |
| Surveys | Large user base (50+); quantitative priority data | Low |
| Use Case Analysis | System interactions; behavioral requirements; cross-departmental systems | Medium |
| User Story Mapping | Agile backlog; feature prioritization | Medium |

### 5.2 Selection Rules

- Plan at least three techniques for comprehensive coverage.
- Complete stakeholder analysis before starting elicitation.
- Prepare interview questions in advance.
- Record or document all sessions (with permission).
- Enforce "what, not how" -- no solutioning during elicitation.

### 5.3 Document Analysis Sources

| Source | Extract |
|--------|---------|
| Existing system docs | Current features, data models, integrations |
| Contracts and SLAs | Performance requirements, compliance obligations |
| Regulations | Mandatory requirements (data retention, reporting) |
| Help desk tickets | Common complaints and feature requests |
| Training materials | Expected workflows and user procedures |

---

## 6. Quality Criteria for Requirements

Every approved requirement passes all six checks:

| Criterion | Test |
|-----------|------|
| **Unambiguous** | Two independent readers reach the same understanding |
| **Testable** | A pass/fail test can be written against the requirement |
| **Traceable** | Source link (backward) and implementation link (forward) exist |
| **Feasible** | Tech lead confirms the requirement is achievable within constraints |
| **Necessary** | The requirement traces to a business need |
| **Consistent** | No contradiction with any other requirement in the set |

A requirement that fails any criterion is returned for rework before it can reach Approved status.

---

## 7. Change Management

### 7.1 Change Request Process

1. **Submit** -- any team member raises a change request identifying affected requirements.
2. **Impact analysis** -- Business Analyst assesses scope, cost, schedule, and traceability impact.
3. **Review** -- Product Owner (for BR/STK) or Tech Lead (for SYS/SWR) reviews and decides: approve, reject, or defer.
4. **Update** -- on approval, update the requirement attributes, increment the version, and update all RTM rows affected.
5. **Communicate** -- notify all stakeholders of the change and its downstream effects.

### 7.2 Rules

- Retired requirement IDs are never reused. Document the retirement reason in the RTM.
- Every change triggers an RTM update before the next gate review.
- Approved changes that affect Must Have requirements require re-validation of forward traceability completeness.
- Deferred requirements remain documented to prevent uncontrolled re-introduction.

### 7.3 Version Control

- Every requirement carries a version number, incremented on each change.
- The RTM is version-controlled alongside requirements.
- Change history is preserved -- no silent overwrites.

---

## Cross-References

| Document | Link |
|----------|------|
| Business Requirements Document template | [../templates/business-requirements-document.md](../templates/business-requirements-document.md) |
| Software Requirements Specification template | [../templates/software-requirements-specification.md](../templates/software-requirements-specification.md) |
| Requirements Traceability Matrix template | [../templates/requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) |
| Use Case template | [../templates/use-case.md](../templates/use-case.md) |
| Change Request Form template | [../templates/change-request-form.md](../templates/change-request-form.md) |
| Gather Requirements runbook | [../runbooks/gather-requirements.md](../runbooks/gather-requirements.md) |
| SDLC Framework | [../framework.md](../framework.md) |
