# Develop Business Case

| Field | Value |
|-------|-------|
| **Procedure ID** | RB-P1-002 |
| **Owner** | Business Analyst |
| **Accountable** | Project Sponsor |
| **SLA** | 10 business days |
| **Escalation** | Project Sponsor |
| **Last Verified** | 2026-03-04 |

---

## ENTRY CRITERIA -- DO NOT PROCEED WITHOUT

- [ ] Business Needs Analysis completed and approved (RB-P1-001)
- [ ] Problem statement validated by Project Sponsor
- [ ] Business impact data available (quantitative or qualitative)
- [ ] Key stakeholders identified and accessible for consultation

---

## ABORT CONDITIONS

| Condition | Action | Escalate To |
|-----------|--------|-------------|
| Cost estimates exceed organizational investment threshold without executive pre-approval | STOP. Escalate to Project Sponsor for executive alignment | Project Sponsor |
| Benefits cannot be substantiated with available data | STOP. Request additional data or commission feasibility study | Project Sponsor |
| Strategic priorities shift making business need obsolete | STOP. Document change and close business case | Project Sponsor |
| Regulatory or legal impediment discovered | STOP. Engage Legal/Compliance team and pause until cleared | Project Sponsor |

---

## PROCEDURE

### Step 1: Define Scope Boundaries

| Action | Owner | SLA |
|--------|-------|-----|
| Establish clear in-scope and out-of-scope boundaries for the proposed solution | Business Analyst | 1 business day |

- [ ] In-scope items listed (features, processes, systems, user groups)
- [ ] Out-of-scope items explicitly listed with rationale
- [ ] Scope boundaries reviewed with Product Owner
- [ ] Assumptions and constraints documented

> **IF** scope boundaries are disputed among stakeholders **THEN** escalate to Product Owner for resolution within 1 business day
> **ELSE** proceed with agreed scope boundaries

### Step 2: Estimate Costs

| Action | Owner | SLA |
|--------|-------|-----|
| Calculate total cost of ownership including development, infrastructure, and licensing | Business Analyst | 2 business days |

- [ ] Development costs estimated (labor hours x blended rate, by phase)
- [ ] Infrastructure costs estimated (hosting, compute, storage, networking)
- [ ] Licensing costs estimated (software, third-party services, subscriptions)
- [ ] Operational costs estimated (support, maintenance, training)
- [ ] Contingency buffer applied (minimum 15% for known risks)
- [ ] Cost estimates reviewed with Tech Lead for technical accuracy
- [ ] All assumptions documented with sources

> **IF** Tech Lead unavailable for cost review **THEN** flag technical estimates as unvalidated and escalate to Product Owner
> **ELSE** proceed with validated cost estimates

### Step 3: Estimate Benefits

| Action | Owner | SLA |
|--------|-------|-----|
| Quantify expected benefits across revenue, cost savings, and efficiency dimensions | Business Analyst | 2 business days |

- [ ] Revenue benefits estimated (new revenue streams, increased conversion, upsell)
- [ ] Cost savings estimated (reduced manual effort, eliminated redundancy, lower error rates)
- [ ] Efficiency gains estimated (cycle time reduction, throughput increase, FTE reallocation)
- [ ] Intangible benefits documented (brand, compliance, customer satisfaction, employee morale)
- [ ] Benefit realization timeline defined (when benefits begin, ramp period, steady state)
- [ ] All estimates documented with assumptions and confidence levels

> **IF** benefits are primarily intangible **THEN** apply proxy metrics and document valuation methodology
> **ELSE** use direct financial quantification

### Step 4: Perform Cost-Benefit Analysis

| Action | Owner | SLA |
|--------|-------|-----|
| Calculate financial metrics comparing costs against benefits over the investment horizon | Business Analyst | 1 business day |

- [ ] Net Present Value (NPV) calculated (minimum 3-year horizon)
- [ ] Return on Investment (ROI) calculated
- [ ] Payback period determined
- [ ] Break-even point identified
- [ ] Sensitivity analysis performed (best case, expected case, worst case)
- [ ] Financial model documented and reproducible

> **IF** NPV is negative under expected case **THEN** document strategic justification or recommend no-go and escalate to Project Sponsor
> **ELSE** proceed with positive financial justification

### Step 5: Assess Risks

| Action | Owner | SLA |
|--------|-------|-----|
| Identify and evaluate risks that could impact project success or business case assumptions | Business Analyst | 1 business day |

- [ ] Technical risks identified (technology maturity, integration complexity, skill gaps)
- [ ] Business risks identified (market change, regulatory change, stakeholder turnover)
- [ ] Financial risks identified (cost overrun, benefit shortfall, funding withdrawal)
- [ ] Operational risks identified (adoption, change management, support capacity)
- [ ] Each risk scored by probability (High/Medium/Low) and impact (High/Medium/Low)
- [ ] Mitigation strategies defined for High and Critical risks
- [ ] Risk register created

> **IF** any risk scores as High probability AND High impact **THEN** escalate to Project Sponsor before proceeding
> **ELSE** document risk register and proceed

### Step 6: Define Success Metrics and KPIs

| Action | Owner | SLA |
|--------|-------|-----|
| Establish measurable success criteria and key performance indicators for the initiative | Business Analyst | 1 business day |

- [ ] Primary KPIs defined (minimum 3, maximum 7)
- [ ] Each KPI includes: metric name, baseline value, target value, measurement method, measurement frequency
- [ ] Leading indicators identified (early signals of success or failure)
- [ ] Lagging indicators identified (outcome measures)
- [ ] KPI ownership assigned per metric
- [ ] Success criteria reviewed with Product Owner

> **IF** baseline data unavailable for any KPI **THEN** define baseline measurement plan and timeline
> **ELSE** document current baselines with data source

### Step 7: Draft Business Case Document

| Action | Owner | SLA |
|--------|-------|-----|
| Compile all analysis into the formal business case document using the approved template | Business Analyst | 1 business day |

- [ ] Executive summary drafted (max 1 page)
- [ ] Problem statement included from RB-P1-001
- [ ] Scope boundaries documented
- [ ] Cost estimates documented with assumptions
- [ ] Benefit estimates documented with assumptions
- [ ] Cost-benefit analysis results included
- [ ] Risk assessment included
- [ ] Success metrics and KPIs included
- [ ] Recommendation stated (Proceed / Proceed with conditions / Do not proceed)
- [ ] Document formatted per business case template

> **IF** business case recommends "Do not proceed" **THEN** document rationale and present to Project Sponsor for final decision
> **ELSE** proceed to stakeholder review

### Step 8: Review with Stakeholders

| Action | Owner | SLA |
|--------|-------|-----|
| Circulate draft business case to key stakeholders for review and feedback | Product Owner | 2 business days |

- [ ] Business case distributed to: Product Owner, Tech Lead, Domain Expert
- [ ] Review period communicated (minimum 2 business days)
- [ ] Feedback collected and consolidated
- [ ] Conflicts or disagreements in feedback identified
- [ ] Revisions applied to business case based on feedback
- [ ] Change log updated with revision summary

> **IF** stakeholder feedback introduces material changes to cost or benefit estimates **THEN** re-execute Steps 2-4 as needed
> **ELSE** incorporate feedback and proceed to sponsor approval

### Step 9: Obtain Sponsor Approval

| Action | Owner | SLA |
|--------|-------|-----|
| Present final business case to Project Sponsor for formal approval decision | Business Analyst | 1 business day |

- [ ] Approval meeting scheduled with Project Sponsor
- [ ] Business case presented with executive summary, financials, and recommendation
- [ ] Questions and concerns addressed
- [ ] Sponsor decision recorded (Approved / Approved with conditions / Rejected / Deferred)
- [ ] Approval signature or formal written confirmation obtained
- [ ] Decision communicated to all consulted and informed stakeholders

> **IF** sponsor approves with conditions **THEN** document conditions, assign owners, and set deadlines for condition resolution
> **ELSE IF** sponsor rejects **THEN** document rejection rationale, communicate to stakeholders, and close
> **ELSE IF** sponsor defers **THEN** document deferral criteria and schedule re-evaluation date
> **ELSE** proceed to exit criteria

---

## EXIT CRITERIA

- [ ] Business case document completed per template
- [ ] Cost-benefit analysis completed with documented assumptions
- [ ] Risk assessment completed with mitigation strategies for high risks
- [ ] Success metrics and KPIs defined with baselines and targets
- [ ] Business case approved by Project Sponsor (signature or written confirmation)
- [ ] Approval decision communicated to all stakeholders
- [ ] Business case stored in designated repository

---

## OUTPUT ARTIFACTS

| Artifact | Template | Storage |
|----------|----------|---------|
| Business Case Document | [Business Case Template](../templates/business-case-template.md) | `project-repo/phase-1/business-case/` |
| Cost-Benefit Analysis | [Cost-Benefit Analysis Template](../templates/cost-benefit-analysis-template.md) | `project-repo/phase-1/business-case/` |
| Risk Register | [Risk Register Template](../templates/risk-register-template.md) | `project-repo/phase-1/risk-register/` |
| KPI Definition Sheet | [KPI Template](../templates/kpi-definition-template.md) | `project-repo/phase-1/kpis/` |

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Business Needs Analysis | Runbook | [RB-P1-001](./conduct-business-needs-analysis.md) |
| Project Charter Creation | Runbook | [RB-P1-003](./create-project-charter.md) |
| Initial Stakeholder Identification | Runbook | [RB-P1-004](./conduct-initial-stakeholder-identification.md) |
| Business Case Template | Template | [../templates/business-case-template.md](../templates/business-case-template.md) |
| Phase 1 Standards | Standard | [../standards/phase-1-standards.md](../standards/phase-1-standards.md) |
