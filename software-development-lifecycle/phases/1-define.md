# Phase 1: Define (Business Analysis + Requirements)

> **Purpose:** Identify business needs, define problems, evaluate options, and authorize projects through an approved project charter. Then systematically elicit, analyze, specify, and validate requirements that bridge business needs to software implementation, aligned with ISO 12207 and ISO 29148.

---

## Entry Criteria

- [ ] Business need or opportunity identified by stakeholder (strategic, operational, regulatory, or market-driven)
- [ ] Sponsor confirmed and available
- [ ] Need aligns with at least one organizational strategic objective
- [ ] Initial stakeholders identified
- [ ] Need expressed as an outcome, not a solution

---

## Deliverables

| # | Document | Template | Required | Runbook |
|---|----------|----------|----------|---------|
| 1 | Business Case | [templates/business-case.md](../templates/business-case.md) | All projects | [runbooks/start-a-project.md](../runbooks/start-a-project.md) |
| 2 | Project Charter | [templates/project-charter.md](../templates/project-charter.md) | All projects | [runbooks/start-a-project.md](../runbooks/start-a-project.md) |
| 3 | Stakeholder Register | [templates/stakeholder-register.md](../templates/stakeholder-register.md) | All projects | [runbooks/start-a-project.md](../runbooks/start-a-project.md) |
| 4 | Business Requirements Document (BRD) | [templates/business-requirements-document.md](../templates/business-requirements-document.md) | All projects | [runbooks/gather-requirements.md](../runbooks/gather-requirements.md) |
| 5 | Software Requirements Specification (SRS) | [templates/software-requirements-specification.md](../templates/software-requirements-specification.md) | Medium+ | [runbooks/gather-requirements.md](../runbooks/gather-requirements.md) |
| 6 | Use Cases | [templates/use-case.md](../templates/use-case.md) | Medium+ | [runbooks/gather-requirements.md](../runbooks/gather-requirements.md) |
| 7 | Requirements Traceability Matrix (RTM) | [templates/requirements-traceability-matrix.md](../templates/requirements-traceability-matrix.md) | Medium+ | [runbooks/gather-requirements.md](../runbooks/gather-requirements.md) |

**PlantUML diagrams:** None required (diagrams start in Phase 2: Design)

---

## Key Activities

### Business Analysis

1. **Identify business need** -- capture the need as an outcome-oriented statement from a documented source (strategy, incident, regulation, feedback). [runbooks/start-a-project.md](../runbooks/start-a-project.md)
2. **Map stakeholders** -- identify all affected parties using Power/Interest grid; build stakeholder register covering 6 categories: Executive, Operational, End User, External Customer, Regulatory, Partner. [runbooks/start-a-project.md](../runbooks/start-a-project.md)
3. **Define the problem** -- refine the need into a quantified problem statement (who, what, when, where, how large). No solution language. [runbooks/start-a-project.md](../runbooks/start-a-project.md)
4. **Develop business case** -- evaluate at least 3 options (including "do nothing") for strategic alignment, business value, feasibility, risk, and resources. [runbooks/start-a-project.md](../runbooks/start-a-project.md)
5. **Assess risks** -- rate likelihood and impact per option; propose mitigations for high-priority risks. [runbooks/start-a-project.md](../runbooks/start-a-project.md)
6. **Create project charter** -- formalize objectives, scope boundary (in/out), timeline, budget, authority, and success criteria. Determine project scale (Small/Medium/Large). Get sponsor sign-off. [runbooks/start-a-project.md](../runbooks/start-a-project.md)

### Requirements Engineering

7. **Elicit requirements** -- interviews, workshops, observation with all stakeholder groups identified in the register. [runbooks/gather-requirements.md](../runbooks/gather-requirements.md)
8. **Analyze and decompose** -- organize into the requirements hierarchy (see below). Prioritize with MoSCoW. Resolve conflicts between stakeholder groups. [runbooks/gather-requirements.md](../runbooks/gather-requirements.md)
9. **Specify requirements** -- document in BRD and SRS with Given/When/Then acceptance criteria per SWR. Include NFRs (performance, security, reliability, scalability, usability, maintainability, compliance). [runbooks/gather-requirements.md](../runbooks/gather-requirements.md)
10. **Validate requirements** -- stakeholder reviews, walkthroughs, checklists. Confirm correctness, completeness, feasibility, testability. [runbooks/gather-requirements.md](../runbooks/gather-requirements.md)
11. **Baseline and establish change control** -- approve requirements baseline; all subsequent changes via CR process with impact analysis and CCB approval. [runbooks/gather-requirements.md](../runbooks/gather-requirements.md)

### Stage Transitions

| From | To | Gate Criteria | Required Approver |
|------|----|---------------|-------------------|
| Business Need | Problem Statement | Need validated; sponsor confirmed; strategic alignment verified | Business Owner |
| Problem Statement | Business Case | Problem accepted; stakeholders mapped; baseline captured | Project Sponsor |
| Business Case | Project Charter | Business case approved; option selected; risk assessed | Governance Board / Sponsor |
| Project Charter | Requirements Elicitation | Charter approved; Phase 2 team assigned | Project Sponsor |
| Requirements Draft | Requirements Baseline | BRD/SRS validated; RTM populated; stakeholders signed off | Product Owner + Sponsor |

---

## Requirements Hierarchy

Every requirement at a lower level must trace back to a parent. Decomposition should be one-to-many (not 1:1).

| Level | ID Pattern | Describes | Owner |
|-------|-----------|-----------|-------|
| Business Requirement | BR-XXX | What the business needs to achieve | Product Owner |
| Stakeholder Requirement | STK-XXX | What each stakeholder group needs from the system | Business Analyst |
| System Requirement | SYS-XXX | What the system must do (technology-independent) | BA / Tech Lead |
| Software Requirement | SWR-XXX | Specific software behavior and constraints | Tech Lead / Developer |

**Rules:** No levels skipped in decomposition. No orphan requirements (SWR without SYS parent). NFRs defined at SWR level. Every SWR has Given/When/Then acceptance criteria.

---

## Key Roles

| Role | Business Analysis | Requirements Engineering |
|------|-------------------|--------------------------|
| Business Owner / Sponsor | Owns the need; funding authority; approves charter | Approves baseline; resolves escalations |
| Product Owner | -- | Defines business requirements; sets priorities; approves BRD |
| Business Analyst | Develops problem statement and business case | Facilitates elicitation; writes BRD/SRS; maintains RTM |
| Technical Lead / Architect | Assesses feasibility of proposed options | Reviews feasibility; decomposes SYS/SWR requirements |
| QA Lead | -- | Reviews testability; defines test approach per requirement |
| Governance Board | Approves or rejects the project charter | -- |

---

## Standards

- [Requirements Standard](../standards/requirements.md) -- requirements classification, traceability, elicitation techniques

---

## Business Case Evaluation Criteria

| # | Criterion | Weight | Score 1-5 |
|---|-----------|--------|-----------|
| 1 | Strategic Alignment | 25% | 5 = directly enables top-3 strategic objective |
| 2 | Business Value | 25% | 5 = high-impact value, rapid realization |
| 3 | Technical Feasibility | 20% | 5 = proven tech, in-house skills, no unknowns |
| 4 | Risk Profile | 15% | 5 = all risks low after mitigation |
| 5 | Resource Availability | 15% | 5 = all resources confirmed, no contention |

**Score interpretation:**

| Weighted Score | Strength | Action |
|----------------|----------|--------|
| 4.0 - 5.0 | Strong | Proceed to project charter; present to governance |
| 3.0 - 3.9 | Moderate | Address gaps in weak criteria; re-score before submission |
| 2.0 - 2.9 | Weak | Rework business case; consider alternative options or scope reduction |
| 1.0 - 1.9 | Insufficient | Do not submit; revisit business need and problem statement |

**Pre-submission checklist:**

- [ ] All 5 criteria scored for every proposed option
- [ ] Scoring performed by at least 2 independent reviewers
- [ ] "Do nothing" option included and scored
- [ ] Strategic alignment validated with sponsor
- [ ] Technical feasibility confirmed by technical lead
- [ ] Scoring rationale documented for each criterion
- [ ] Executive summary prepared for governance review

**Weight adjustments:** Increase Strategic Alignment to 35% for regulatory mandates. Increase Technical Feasibility to 30% for novel technology. Increase Resource Availability to 25% when resource-constrained.

---

## Top 5 Pitfalls

| # | Pitfall | Warning Sign | Fix |
|---|---------|-------------|-----|
| 1 | **Solution-first thinking** | Problem statement contains technology or product names (e.g., "BR: Use React + Node.js") | Rewrite to describe the business problem only; evaluate multiple approaches before recommending |
| 2 | **Ambiguous requirements** | Terms like "fast", "intuitive", "user-friendly" without numbers | Replace with measurable criteria (e.g., "within 200ms at 95th percentile, 200 concurrent users") |
| 3 | **Missing stakeholders** | Only 1-2 groups consulted; end users excluded | Complete Power/Interest grid; interview all Manage Closely and Keep Informed groups |
| 4 | **No acceptance criteria** | SWRs lack Given/When/Then; subjective language in criteria | Every SWR must have explicit, testable acceptance criteria with measurable thresholds |
| 5 | **Single-option business case** | Business case presents only the preferred solution | Include "do nothing" + at least one alternative; score all options against the same criteria |

**Also watch for:**

- **Scope creep at Phase 1** -- items deferred to later phases must go in a parking lot; do not absorb new scope without formal review.
- **Missing NFRs** -- if SRS has zero non-functional requirements, add at least one per category (performance, security, usability, reliability, scalability, maintainability, compliance).
- **No success metrics** -- every business objective needs at least one SMART metric with baseline, target, and measurement method.
- **Gold plating** -- if no stakeholder requested the feature, remove it or get explicit sign-off.
- **Scope creep after baseline** -- no features added without a change request (CR-XXX) through CCB.

---

## Exit Criteria / Phase Gate

### Business Analysis Gate

- [ ] Problem statement approved by sponsor
- [ ] Business case evaluated -- all 5 criteria scored by at least 2 reviewers
- [ ] Business case approved by Product Owner (all projects) and Sponsor (medium/large)
- [ ] Risk assessment completed for selected option
- [ ] Project charter signed by Sponsor and Product Owner (+ Tech Lead for medium/large)
- [ ] Project scale formally determined (Small / Medium / Large)
- [ ] In-scope and out-of-scope sections defined in charter
- [ ] Success criteria defined with measurable targets, baselines, and measurement methods

### Stakeholder Management Gate

- [ ] Stakeholder register created with all 6 categories evaluated (Executive, Operational, End User, External Customer, Regulatory, Partner)
- [ ] Power/Interest classification completed (medium/large)
- [ ] Communication plan defined per quadrant (medium/large)
- [ ] Stakeholder register reviewed by Sponsor (medium/large)

### Requirements Gate

- [ ] Stakeholder analysis completed
- [ ] BRD baselined and approved
- [ ] SRS baselined and approved (medium/large)
- [ ] RTM populated with BR-to-SWR traceability links (medium/large)
- [ ] All Must Have requirements validated
- [ ] Change management process established
- [ ] All deliverables reviewed and accepted
- [ ] Phase 2 team and resources identified

---

## Scaling Notes

| Project Size | Criteria | Skip/Simplify |
|-------------|----------|---------------|
| Small (< 2 weeks) | 1-2 devs, <= 500 person-hours, single team | Skip SRS, Use Cases, RTM. BRD can be 1-page summary. Simplified charter (scope + key constraints + core roles). Stakeholder register: name and role only, Power/Interest grid optional. Business case: executive summary + problem + solution + simplified value assessment. |
| Medium (2-8 weeks) | 3-5 devs, 500-5000 person-hours, 2-3 teams | Full BRD, simplified SRS. RTM optional. Standard charter with full scope definition and all constraint categories. All 6 stakeholder categories evaluated with Power/Interest grid. |
| Large (8+ weeks) | 6+ devs, > 5000 person-hours, 4+ teams | All deliverables required. Full charter with RACI, backup roles, scope change process. Detailed communication plan per stakeholder. Monthly stakeholder register reviews. |

---

## Phase 1 Outputs Feed Phase 2

| Phase 1 Output | Phase 2 Input |
|----------------|---------------|
| Approved Problem Statement | Basis for requirements elicitation scope |
| Business Case (selected option) | Constraints, assumptions, and context for requirements |
| Stakeholder Register | Starting point for requirements workshops and interviews |
| Project Charter (scope, budget, timeline) | Boundaries for project planning and resource allocation |
| Risk Assessment | Input to risk management plan and contingency planning |
| Success Criteria | Basis for acceptance criteria and test strategy |
| BRD / SRS / RTM | Direct input to system architecture and design |

---

## Next Phase

-> [Phase 2: Design](2-design.md)
