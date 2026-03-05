# Gather Requirements

## Purpose

This runbook provides a unified, end-to-end procedure for gathering, documenting, validating, and managing software requirements. It consolidates stakeholder analysis, business requirement extraction, software requirement derivation, validation, and change management into a single actionable workflow.

---

## Prerequisites

- [ ] Approved business case or project charter available
- [ ] Access to organizational chart confirmed
- [ ] Business Analyst, Product Owner, Tech Lead, and QA Lead assigned
- [ ] Scheduled time with project sponsor secured
- [ ] Stakeholder availability confirmed for elicitation sessions
- [ ] Change Control Board (CCB) members identified: Product Owner, Tech Lead, QA Lead, Project Sponsor

---

## Step 1: Conduct Stakeholder Analysis

**Owner:** Business Analyst | **SLA:** 5 business days

### 1.1 Identify All Stakeholders

List every person or group with influence over or affected by the project.

- [ ] Internal groups reviewed: executives, department heads, end users, support staff
- [ ] External groups reviewed: customers, regulators, partners, third-party providers

### 1.2 Classify Using Power/Interest Grid

Assign each stakeholder a Power level (High/Medium/Low) and Interest level (High/Medium/Low), then map to a strategy:

| Quadrant | Power | Interest | Strategy |
|----------|-------|----------|----------|
| Manage Closely | High | High | Engage actively, consult on decisions |
| Keep Satisfied | High | Low | Inform of major decisions only |
| Keep Informed | Low | High | Provide regular updates |
| Monitor | Low | Low | Major milestones only |

- [ ] Every stakeholder classified into a quadrant

### 1.3 Document Profiles and Create Register

Record for each stakeholder: ID, name, role, organization, power/interest levels, classification, key concerns, communication preference, and contact information.

- [ ] All profiles documented with mandatory fields
- [ ] Register compiled (no duplicates)

### 1.4 Define Communication Plan

- [ ] Communication method, frequency, content, and owner defined for each stakeholder group
- [ ] All Manage Closely stakeholders have scheduled 1:1 interviews

### 1.5 Obtain Sign-Off

- [ ] Stakeholder register and communication plan presented to project sponsor
- [ ] Written approval obtained and register distributed to project team

> **IF** sponsor identifies missing stakeholders **THEN** return to 1.1 and add them.

---

## Step 2: Extract Business Requirements

**Owner:** Business Analyst | **SLA:** 15 business days

### 2.1 Review Business Case and Project Charter

- [ ] Business case reviewed; objectives, scope, and constraints identified
- [ ] Project charter reviewed; success criteria and timeline noted
- [ ] All business objectives listed for requirement mapping

### 2.2 Schedule and Conduct Elicitation Sessions

- [ ] Structured interviews scheduled with all Manage Closely stakeholders (45-60 min each)
- [ ] Requirements workshop scheduled for cross-functional needs (2-4 hours)
- [ ] Observation sessions planned for operational processes
- [ ] All interviews completed; responses recorded and attributed to source stakeholder

### 2.3 Facilitate Requirements Workshop

- [ ] Interview findings presented and validated with group
- [ ] Requirements identified and prioritized using MoSCoW (Must/Should/Could/Won't Have)
- [ ] Conflicts between stakeholder needs resolved or escalated
- [ ] Workshop minutes and action items recorded

### 2.4 Analyze Existing Systems and Processes

- [ ] As-is state documented for each relevant process
- [ ] Data flows mapped (inputs, outputs, transformations)
- [ ] External system integrations listed
- [ ] Business rules captured

### 2.5 Document Business Requirements

Write each requirement in BR-XXX format using the [Business Requirements Document](../templates/business-requirements-document.md) template. Each requirement must include: ID, title, description ("The business shall..."), priority, source, rationale, acceptance criteria, and status.

- [ ] All requirements follow BR-XXX format with all mandatory attributes
- [ ] Every BR traces to at least one business objective (no orphan requirements)

### 2.6 Review, Validate, and Obtain Approval

- [ ] Draft BRD distributed to all stakeholders; 5 business day review period allowed
- [ ] Written feedback collected and incorporated
- [ ] All Must Have requirements walked through with project sponsor
- [ ] Written sign-off obtained from project sponsor
- [ ] BRD baselined (all future changes follow Step 5)

---

## Step 3: Derive Software Requirements

**Owner:** Business Analyst + Tech Lead | **SLA:** 10 business days

### 3.1 Review Approved Business Requirements

- [ ] Baselined BRD reviewed by Business Analyst and Tech Lead
- [ ] Must Have and Should Have requirements listed
- [ ] Ambiguous requirements resolved with Product Owner before proceeding

### 3.2 Identify System Boundaries and Interfaces

Define the system scope and document all boundary elements: external systems, user interfaces, data interfaces, and infrastructure dependencies.

- [ ] System scope defined
- [ ] All boundary elements documented

### 3.3 Decompose Requirements

Perform a three-level decomposition:

1. **BR to Stakeholder Requirements (STK-XXX):** For each BR, identify what each stakeholder group needs.
2. **STK to System Requirements (SYS-XXX):** For each STK, define what the system must do (implementation-neutral).
3. **SYS to Software Requirements (SWR-XXX):** For each SYS, define specific, implementable software behavior.

- [ ] All BRs decomposed through STK -> SYS -> SWR levels
- [ ] IDs assigned at each level

> **IF** a SWR requires architecture decisions not yet made **THEN** escalate to Tech Lead for architecture review.
> **IF** a SWR is too large for a single sprint **THEN** decompose further.

### 3.4 Classify Each Requirement

Assign to every SWR: type (Functional/Non-Functional), NFR category if applicable, priority (MoSCoW), risk level (High/Medium/Low), and source.

- [ ] All SWRs classified

### 3.5 Define Acceptance Criteria

Write acceptance criteria for each SWR in Given/When/Then format. Use the [Use Case Template](../templates/use-case.md) where applicable.

- [ ] Every SWR has at least one measurable acceptance criterion
- [ ] No subjective terms without quantification

### 3.6 Establish Traceability

Update the [Requirements Traceability Matrix](../templates/requirements-traceability-matrix.md) with all links: SWR -> SYS -> STK -> BR.

- [ ] Every SWR traces back to at least one BR
- [ ] No orphan SWRs

### 3.7 Obtain Peer Review and Tech Lead Approval

- [ ] BA completeness and consistency review done
- [ ] Tech Lead feasibility review done
- [ ] All issues resolved; Tech Lead sign-off obtained
- [ ] SRS documented using the [Software Requirements Specification](../templates/software-requirements-specification.md) template

---

## Step 4: Validate Requirements

**Owner:** Business Analyst + Tech Lead + QA Lead | **SLA:** 10 business days

### 4.1 Check Completeness

- [ ] Every BR has at least one SWR
- [ ] All non-functional categories addressed (Performance, Security, Usability, Reliability, Scalability)
- [ ] All system interfaces and user roles have requirements

### 4.2 Check Consistency

- [ ] No contradictory functional requirements
- [ ] Non-functional requirements are compatible with each other
- [ ] Priority assignments are consistent (no Should Have depending on a Could Have)

### 4.3 Check Feasibility

- [ ] Technology exists to implement each Must Have and Should Have requirement
- [ ] Each requirement is deliverable within project timeline
- [ ] No requirement exceeds known infrastructure constraints

### 4.4 Check Testability

- [ ] Every SWR has at least one acceptance criterion
- [ ] No subjective terms without quantification
- [ ] Test approach identified for each SWR (manual, automated, or inspection)

### 4.5 Conduct Requirements Review Meeting

**Attendees:** Project Sponsor, Product Owner, Business Analyst, Tech Lead, QA Lead, Domain Expert(s)

- [ ] Validation findings from 4.1-4.4 presented
- [ ] Each flagged issue walked through and resolved
- [ ] Action items assigned with owners and deadlines
- [ ] Meeting minutes recorded

### 4.6 Resolve Issues and Update Requirements

- [ ] All conflicts and ambiguities resolved (escalate to Product Owner if no agreement)
- [ ] Flagged requirements reworked; RTM updated
- [ ] Validation checks re-run on modified requirements -- all pass

### 4.7 Obtain Baseline Approval

- [ ] Product Owner sign-off obtained (business validity)
- [ ] Tech Lead sign-off obtained (technical feasibility)
- [ ] QA Lead sign-off obtained (testability)
- [ ] SRS marked as official baseline; version number and date recorded
- [ ] Baselined SRS distributed to project team

---

## Step 5: Manage Requirements Changes

**Owner:** Business Analyst | **SLA:** 10 business days per change request

> This step applies after the requirements baseline is established. All post-baseline changes must follow this procedure.

### 5.1 Receive and Log Change Request

- [ ] Change request received in writing using the [Change Request Form](../templates/change-request-form.md)
- [ ] Unique CR-XXX ID assigned
- [ ] All fields recorded: CR ID, date, requestor, description, affected requirements, justification, status
- [ ] Receipt acknowledged to requestor within 2 business days

### 5.2 Perform Impact Analysis

Analyze impact across five dimensions: scope, schedule, cost, risk, and technical. Use the RTM to trace the full impact chain.

- [ ] All five dimensions analyzed
- [ ] Impact level determined (Low / Medium / High)

### 5.3 Present to Change Control Board and Record Decision

| Impact Level | Decision Authority |
|-------------|-------------------|
| Low | Product Owner alone |
| Medium | Product Owner + Tech Lead |
| High | Full CCB including Project Sponsor |

- [ ] One-page impact summary presented to CCB
- [ ] Decision recorded with rationale (Approved / Rejected / Deferred)

### 5.4 Implement Approved Changes

- [ ] Affected requirements modified in SRS (retired requirements marked as Retired, not deleted)
- [ ] New requirements added with new IDs if needed
- [ ] Baseline version number incremented; SRS revision history updated
- [ ] RTM updated; all traceability links verified valid

### 5.5 Communicate and Archive

- [ ] All affected parties notified (development team, QA, Product Owner, requestor, Project Sponsor for high-impact changes)
- [ ] CR status set to Closed; final decision and actual impact recorded
- [ ] CR archived with project documentation

---

## Outputs Checklist

| Output | Template | Produced In |
|--------|----------|-------------|
| Stakeholder Register and Communication Plan | -- | Step 1 |
| Business Requirements Document (BRD) | [business-requirements-document.md](../templates/business-requirements-document.md) | Step 2 |
| Software Requirements Specification (SRS) | [software-requirements-specification.md](../templates/software-requirements-specification.md) | Step 3 |
| Requirements Traceability Matrix (RTM) | [requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) | Step 3, updated in Steps 4-5 |
| Use Cases | [use-case.md](../templates/use-case.md) | Step 3 |
| Requirements Validation Report | -- | Step 4 |
| Baseline Sign-Off Records | -- | Steps 1, 2, 4 |
| Change Request Log | [change-request-form.md](../templates/change-request-form.md) | Step 5 |

---

## Tips

- **Start with stakeholders, not requirements.** Understanding who cares and why prevents rework later.
- **Interview before you workshop.** Individual interviews surface candid concerns that groups may suppress.
- **One requirement, one behavior.** If a requirement contains "and", consider splitting it into two.
- **Trace everything.** A requirement without traceability to a business objective is a candidate for removal.
- **Use MoSCoW consistently.** Prioritize at the business level first, then inherit into software requirements.
- **Make acceptance criteria measurable.** Replace "fast" with "responds within 2 seconds under 100 concurrent users."
- **Baseline before you build.** Never start development against a draft SRS. Lock the baseline and use the change management process for all subsequent modifications.
- **Keep the RTM alive.** Update it every time a requirement changes -- it is the single source of truth for impact analysis.
- **Archive rejected changes too.** Recording why a change was rejected prevents the same request from resurfacing without new justification.
- **Communicate decisions promptly.** Every stakeholder affected by a change should hear about it before they discover it themselves.
