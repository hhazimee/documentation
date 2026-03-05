# Conduct Reviews

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-GEN-001 |
| **Owner** | Tech Lead |
| **Applies To** | Architecture Reviews, Design Reviews, Phase Gate Reviews |
| **Last Verified** | 2026-03-05 |

---

## 1. Purpose

This runbook provides a unified, step-by-step procedure for conducting architecture reviews, design reviews, and phase gate reviews across the software development lifecycle. It consolidates review criteria, checklists, and decision frameworks so that any reviewer or facilitator can prepare for, execute, and close out a review consistently.

---

## 2. Prerequisites

Before initiating any review, confirm the following:

- [ ] The artifact under review is complete (no placeholder sections or missing content).
- [ ] All reviewers have been identified and their availability confirmed.
- [ ] Review materials have been distributed with adequate pre-read time (minimum 2 business days for gate reviews, 3 business days for design reviews, 5 business days for architecture reviews).
- [ ] The applicable checklist or evaluation criteria have been obtained.
- [ ] Prior phase artifacts are approved and available as reference (e.g., approved requirements for an architecture review, approved architecture for a design review).

---

## 3. Architecture Review Procedure

**When:** End of Phase 3 (System Architecture), before proceeding to Phase 4 (Design).
**Facilitator:** Tech Lead | **Presenter:** System Architect
**SLA:** 5 business days end-to-end.
**Source:** *(merged into this runbook)*

### 3.1 Entry Criteria

- [ ] Draft Architecture Description Document (ADD) complete with all viewpoints.
- [ ] All Architecture Decision Records (ADRs) written and in Proposed status.
- [ ] ADD distributed to reviewers at least 5 business days before the review meeting.
- [ ] All required attendees confirmed (System Architect, Tech Lead, Product Owner, Infrastructure Engineer, QA Lead, Senior Developer(s) -- minimum 4 of 6).

### 3.2 Steps

1. **Distribute materials.** Send draft ADD, all ADRs, and the review checklist to attendees. Request written questions and collect pre-review feedback at least 2 days before the meeting. The architect prepares responses 1 day before the meeting.

2. **Conduct the review meeting (~3 hours).** Follow this agenda:
   - Open: state objectives and review criteria (10 min).
   - Present System Context View (15 min) and discuss system boundaries (15 min).
   - Present Logical View (20 min) and discuss component decomposition (20 min).
   - Break (10 min).
   - Present Process, Deployment, and Development Views (30 min) and discuss (15 min).
   - Walk through ADRs and key technology decisions (15 min).
   - Discuss quality attributes -- performance, security, scalability (15 min).
   - Summarize findings, action items, and decision (15 min).

3. **Evaluate against criteria.** Assess each criterion as Pass or Fail:
   - Conceptual Integrity -- consistent principles and uniform patterns.
   - Completeness -- all ASRs addressed, all external interfaces shown.
   - Consistency with Requirements -- every requirement traces to an architecture element.
   - Feasibility -- buildable with available skills and timeline.
   - Quality Attribute Coverage -- documented approach for performance, security, scalability, reliability.
   - Risk Identification -- risks identified and mitigated.
   - Testability -- each component testable independently.
   - Deployability -- deployment topology clear and automatable.
   - Maintainability -- components loosely coupled, data ownership clear.

4. **Evaluate quality attribute scenarios.** For each critical quality attribute (Performance, Security, Scalability, Reliability), walk through one scenario (stimulus and expected response), document the architecture response, and record a verdict (Adequate / Needs improvement). "Needs improvement" verdicts become Concerns or Blockers.

5. **Document findings.** Categorize each finding:
   - **Blocker** -- fundamental flaw; must fix before approval.
   - **Concern** -- must address before Phase 4 begins.
   - **Observation** -- suggestion; architect decides whether to act.

6. **Record decision.** Choose one:
   - **Approved** -- zero blockers, all criteria pass.
   - **Approved with Conditions** -- zero blockers, 1-3 concerns with defined resolution timeline.
   - **Rework Required** -- one or more blockers exist; return to architect; schedule re-review (blockers only, 1 hour).

7. **Post-review follow-up (3 business days).** Architect addresses blockers and concerns. Tech Lead redistributes the updated ADD, updates ADR statuses from Proposed to Accepted, and distributes the approved ADD to the full project team.

---

## 4. Design Review Procedure

**When:** During Phase 4 (Design), per component, before implementation begins.
**Facilitator:** Tech Lead | **Presenter:** Developer
**SLA:** 5 business days (3-day pre-read + 2-day review and disposition).
**Source:** *(merged into this runbook)*

### 4.1 Entry Criteria

- [ ] Detailed Design Document (DDD) complete for the component.
- [ ] API specification complete (if the component exposes APIs).
- [ ] Data model complete (if the component owns data).
- [ ] Design Review Checklist template obtained from *(Section 6 below)*.
- [ ] All reviewers identified and available (Tech Lead, Senior Developer, QA Lead, Frontend Developer if API).

### 4.2 Steps

1. **Distribute materials.** Send DDD, API spec, data model, and the Design Review Checklist to all reviewers. Confirm receipt within 1 business day. Schedule the review meeting at least 3 business days after distribution. If documents are updated after distribution, redistribute and reset the pre-read period.

2. **Conduct the review meeting (1 to 1.5 hours per component).** Follow this agenda:
   - Present component overview and context (10 min).
   - Walk through public interface (10 min).
   - Walk through internal structure and business logic (15 min).
   - Walk through data model (10 min).
   - Walk through error handling and edge cases (10 min).
   - Review against Design Review Checklist (10 min).
   - Discuss findings and action items (10 min).
   - Record decision (10 min).

   If the meeting exceeds 1.5 hours, table remaining items and schedule a follow-up within 2 business days.

3. **Evaluate using the Design Review Checklist.** Complete every item in the checklist. Record pass, fail, or N/A per item. Failed items become documented findings (see Section 6 for the consolidated checklist).

4. **Record decision.** Choose one:
   - **Approved** -- all checklist items pass, zero blocking issues.
   - **Approved with Conditions** -- minor items to address, no blocking issues.
   - **Rework Required** -- blocking issues found; return to designer, re-review after fixes.

5. **Post-review actions (2 business days).** Developer addresses all findings. Tech Lead verifies fixes for blocking and major findings, marks the approved design as baseline, and confirms the RTM is updated with design references.

---

## 5. Phase Gate Review Procedure

**When:** At the transition between any two SDLC phases.
**Facilitator:** Phase Lead | **Decision Maker:** Varies by phase (see table below).
**SLA:** 2 business days for preparation; gate meeting plus disposition in 1 business day.
**Source:** [sdlc-framework.md -- Gate Review Procedure](../framework.md)

### 5.1 Steps

1. **Preparation.** The phase lead assembles all required artifacts and distributes them to gate reviewers at least 2 business days before the review meeting.

2. **Review meeting.** Gate reviewers evaluate artifacts against the exit criteria defined for the phase. Agenda:
   - Phase lead presents a summary of work completed and artifacts produced.
   - Reviewers raise questions, concerns, and deficiencies.
   - Each exit criterion is evaluated as Met, Partially Met, or Not Met.

3. **Decision.** The gate decision is one of:
   - **Proceed** -- all exit criteria are Met; advance to the next phase.
   - **Conditional Proceed** -- minor items remain open but do not block; create a punch list with owners and due dates.
   - **Rework** -- one or more exit criteria are Not Met; remain in the current phase until resolved; conduct a follow-up review.
   - **Stop** -- fundamental issues call project viability into question; project sponsor makes a go/no-go decision.

4. **Documentation.** Record the gate review decision, attendees, and action items in the project log. For medium and large projects, file a formal gate review record.

### 5.2 Gate Reviewers by Phase

| Phase Gate | Required Reviewers |
|------------|--------------------|
| Phase 1 exit (Business Analysis) | Project Sponsor, Product Owner |
| Phase 2 exit (Requirements) | Product Owner, Business Analyst, Tech Lead, Domain Expert(s) |
| Phase 3 exit (Architecture) | Tech Lead, Product Owner, QA Lead |
| Phase 4 exit (Design) | Tech Lead, Developer(s) assigned to implementation |
| Phase 5 exit (Development) | Tech Lead, QA Lead |
| Phase 6 exit (Testing) | Product Owner, Tech Lead, QA Lead |
| Phase 7 exit (Deployment) | Product Owner, Tech Lead, QA Lead, Operations Lead |
| Phase 8 reviews (Operations) | Tech Lead, Operations Lead, Product Owner (quarterly) |

---

## 6. Review Checklist (Consolidated)

Use this consolidated checklist during architecture and design reviews. Mark each item as Pass, Fail, or N/A.

### Architecture Adherence

- [ ] Component responsibilities match the ADD.
- [ ] Component boundaries match architecture definitions.
- [ ] Technology choices align with ADRs.
- [ ] Interfaces match architecture contracts.
- [ ] Data ownership respects component boundaries.

### API Design (if applicable)

- [ ] URL structure follows the [API Design Standard](../standards/architecture-and-design.md).
- [ ] HTTP methods used correctly.
- [ ] Request/response schemas fully defined.
- [ ] All error responses documented.
- [ ] Pagination implemented for list endpoints.
- [ ] Authentication requirements specified.
- [ ] Idempotency addressed for write operations.

### Data Model (if applicable)

- [ ] Naming follows the [Database Design Standard](../standards/architecture-and-design.md).
- [ ] Required columns present (id, timestamps).
- [ ] Foreign keys and constraints defined.
- [ ] Indexes support identified query patterns.
- [ ] Normalization verified (3NF minimum); denormalization documented with rationale.
- [ ] Migration scripts structured.

### Business Logic

- [ ] All assigned requirements addressed.
- [ ] Algorithms clearly specified.
- [ ] Edge cases identified and handled.
- [ ] Business rules match SRS acceptance criteria.

### Error Handling

- [ ] All error scenarios identified.
- [ ] Error responses follow standard format.
- [ ] Recovery/retry strategy defined where applicable.
- [ ] No sensitive data in error messages.

### Security

- [ ] Input validation defined at boundaries.
- [ ] Authorization checks for each endpoint.
- [ ] SQL injection prevention (parameterized queries).
- [ ] Sensitive data not logged.
- [ ] No secrets hardcoded.

### Testability

- [ ] Dependencies injectable (can be mocked).
- [ ] Public methods have clear inputs and outputs.
- [ ] Acceptance criteria are testable.
- [ ] Edge cases can be unit tested.
- [ ] Each component testable independently (architecture-level).

### SOLID Principles

- [ ] Single Responsibility: each module has one reason to change.
- [ ] Open/Closed: extensible without modification.
- [ ] Interface Segregation: no forced dependencies on unused methods.
- [ ] Dependency Inversion: depends on abstractions for externals.

### Traceability

- [ ] Every design element traces to a requirement.
- [ ] No orphan design elements (no requirement source).
- [ ] RTM updated with design references.

---

## 7. Outputs

Every review produces the following records. Store them in the project repository under `docs/reviews/`.

| Output | Description | Produced By |
|--------|-------------|-------------|
| Review Record | Attendees, date, type (architecture / design / gate), findings, and decision | Facilitator |
| Findings Log | Each finding with severity (Blocker / Concern / Observation), description, assigned owner, and due date | Facilitator |
| Action Items | Specific corrective actions with owner and target date, tracked to closure | Facilitator |
| Updated Artifacts | Revised ADD, DDD, ADRs, or other documents reflecting review feedback | Artifact owner |
| Gate Decision Record | Formal decision (Proceed / Conditional / Rework / Stop) with rationale (for gate reviews) | Phase lead |
| Updated RTM | Traceability matrix updated with architecture or design references | Developer / BA |

### Templates and Standards

| Resource | Link |
|----------|------|
| Architecture Description Document Template | [ADD Template](../templates/architecture-description-document.md) |
| Architecture Decision Record Template | [ADR Template](../templates/architecture-decision-record.md) |
| Design Review Checklist Template | *(Section 6 of this runbook)* |
| Detailed Design Document Template | [DDD Template](../templates/detailed-design-document.md) |
| SDLC Framework Standard | [SDLC Framework](../framework.md) |
| Architecture Description Standard | [Architecture Standard](../standards/architecture-and-design.md) |
| Detailed Design Standard | [Design Standard](../standards/architecture-and-design.md) |

---

## 8. Tips

1. **Pre-read is non-negotiable.** Reviews without adequate pre-read devolve into read-aloud sessions. Enforce the minimum pre-read period and collect written feedback before the meeting.

2. **Separate finding severity strictly.** Blockers must be resolved before approval. Concerns must be resolved before the next phase begins. Observations are optional. Mixing these categories weakens the review decision.

3. **Time-box relentlessly.** Architecture reviews should not exceed 3 hours. Design reviews should not exceed 1.5 hours per component. If time runs out, schedule a focused follow-up rather than rushing through remaining items.

4. **Use the checklist as a forcing function.** Walk through every checklist item during the meeting, even items that seem obviously satisfied. Skipped items are where defects hide.

5. **Record decisions immediately.** Write the decision (Approved / Approved with Conditions / Rework / Proceed / Conditional Proceed / Stop) before the meeting ends. Ambiguous outcomes lead to re-work and schedule slip.

6. **Track action items to closure.** Every finding must have an owner and a due date. The facilitator is responsible for following up. Do not consider the review complete until all blockers and concerns are verified as resolved.

7. **Scale appropriately.** For small projects (1-2 developers), self-review with the checklist is acceptable for design reviews and gate reviews can be informal. For large projects (6+ developers), full formal reviews with dedicated meetings are mandatory. Refer to the scaling gate in the [SDLC Framework](../framework.md).

8. **Avoid combining review types.** Architecture reviews and design reviews have different scopes, attendees, and criteria. Running them together creates confusion about what level of abstraction is being evaluated.

9. **Re-reviews should be focused.** When rework is required, the follow-up review should only cover the items that failed. Do not re-review the entire artifact.

10. **Capture lessons learned.** After a review with significant findings, note what could have been caught earlier. Feed this into process improvement through the ADR process or sprint retrospectives.
