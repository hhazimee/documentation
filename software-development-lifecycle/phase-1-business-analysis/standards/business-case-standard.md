# Business Case Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P1-001 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Product Owner |
| **Verification Method** | Phase 1 Gate Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project **THEN** Executive Summary, Problem Statement, Proposed Solution, and simplified cost-benefit (1-year projection, no risk-adjusted estimates required)
> **IF** medium project **THEN** All required sections; 3-year cost-benefit projection with ROI calculation and risk-adjusted estimates
> **IF** large project **THEN** Full compliance; all sections, 3-year projection, ROI calculation, risk-adjusted estimates, sensitivity analysis, and external review

---

## COMPLIANCE REQUIREMENTS

### Required Sections

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Business case MUST contain an Executive Summary | All projects | [ ] Executive Summary section present | Reject at gate review; return for revision |
| 2 | Business case MUST contain a Problem Statement with quantified business impact | All projects | [ ] Problem Statement section present with measurable impact data | Reject at gate review; return for revision |
| 3 | Business case MUST contain a Proposed Solution section | All projects | [ ] Proposed Solution section present | Reject at gate review; return for revision |
| 4 | Business case MUST contain an Alternatives Considered section with minimum 2 alternatives | Medium/Large | [ ] Alternatives section present with >= 2 alternatives evaluated | Reject at gate review; return for revision |
| 5 | Business case MUST contain a Cost-Benefit Analysis section | All projects | [ ] Cost-Benefit Analysis section present | Reject at gate review; return for revision |
| 6 | Business case MUST contain a Risk Assessment section | Medium/Large | [ ] Risk Assessment section present | Reject at gate review; return for revision |
| 7 | Business case MUST contain a Success Metrics section | All projects | [ ] Success Metrics section present | Reject at gate review; return for revision |
| 8 | Business case MUST contain a Timeline and Milestones section | Medium/Large | [ ] Timeline section present | Reject at gate review; return for revision |
| 9 | Business case MUST contain a Stakeholder Impact section | Large | [ ] Stakeholder Impact section present | Reject at gate review; return for revision |

### Minimum Content

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 10 | Executive Summary MUST NOT exceed 1 page | All projects | [ ] Executive Summary is 1 page or less | Return for revision |
| 11 | Problem Statement MUST reference at least 1 quantified data point | All projects | [ ] Quantified data point present in Problem Statement | Return for revision |
| 12 | Proposed Solution MUST describe the approach, not just the outcome | All projects | [ ] Solution approach described | Return for revision |
| 13 | Each alternative MUST include reason for rejection | Medium/Large | [ ] Rejection rationale documented per alternative | Return for revision |

### Cost-Benefit Analysis Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 14 | Cost-benefit analysis MUST include a 3-year financial projection | Medium/Large | [ ] 3-year projection present | Reject at gate review; return for revision |
| 15 | Cost-benefit analysis MUST include ROI calculation | Medium/Large | [ ] ROI calculation present and formula documented | Reject at gate review; return for revision |
| 16 | Cost-benefit analysis MUST include risk-adjusted estimates (pessimistic, expected, optimistic) | Medium/Large | [ ] Three estimate scenarios documented | Reject at gate review; return for revision |
| 17 | All cost figures MUST include capital expenditure and operational expenditure separately | Medium/Large | [ ] CapEx and OpEx itemized separately | Return for revision |
| 18 | Benefits MUST be categorized as tangible (quantified) or intangible (qualified) | All projects | [ ] Benefits categorized | Return for revision |
| 19 | Cost-benefit analysis MUST include a 1-year projection at minimum | Small | [ ] 1-year projection present | Reject at gate review; return for revision |
| 20 | Sensitivity analysis MUST be performed on key financial assumptions | Large | [ ] Sensitivity analysis documented | Return for revision |

### Success Metrics Rules

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 21 | Each success metric MUST be measurable with a numeric or binary indicator | All projects | [ ] All metrics have measurable indicators | Reject at gate review; return for revision |
| 22 | Each success metric MUST have a documented baseline value | All projects | [ ] Baseline value recorded for each metric | Reject at gate review; return for revision |
| 23 | Each success metric MUST have a documented target value | All projects | [ ] Target value recorded for each metric | Reject at gate review; return for revision |
| 24 | Each success metric MUST have a defined measurement method | All projects | [ ] Measurement method documented for each metric | Reject at gate review; return for revision |
| 25 | Each success metric MUST have a measurement frequency | Medium/Large | [ ] Measurement frequency defined for each metric | Return for revision |
| 26 | Minimum 3 success metrics MUST be defined | Medium/Large | [ ] >= 3 success metrics documented | Return for revision |
| 27 | Minimum 1 success metric MUST be defined | Small | [ ] >= 1 success metric documented | Return for revision |

### Approval Requirements

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 28 | Business case MUST be approved by Product Owner | All projects | [ ] Product Owner sign-off recorded | Cannot proceed to Phase 1 gate |
| 29 | Business case MUST be approved by Project Sponsor | Medium/Large | [ ] Project Sponsor sign-off recorded | Cannot proceed to Phase 1 gate |
| 30 | Business case MUST be approved by Budget Authority | Large | [ ] Budget Authority sign-off recorded | Cannot proceed to Phase 1 gate |
| 31 | All approvals MUST include date, name, and role of approver | All projects | [ ] Approval metadata complete | Return for revision |

---

## COMPLIANCE CHECKLIST

- [ ] Executive Summary present and within 1-page limit
- [ ] Problem Statement present with quantified business impact
- [ ] Proposed Solution present with approach description
- [ ] Alternatives Considered present with >= 2 alternatives and rejection rationale (medium/large)
- [ ] Cost-Benefit Analysis present with required projection period
- [ ] 3-year financial projection included (medium/large)
- [ ] ROI calculation included with formula (medium/large)
- [ ] Risk-adjusted estimates (pessimistic, expected, optimistic) included (medium/large)
- [ ] CapEx and OpEx itemized separately (medium/large)
- [ ] Benefits categorized as tangible or intangible
- [ ] Sensitivity analysis performed (large)
- [ ] Risk Assessment present (medium/large)
- [ ] Success Metrics present with minimum count met
- [ ] Each success metric has measurable indicator
- [ ] Each success metric has baseline value
- [ ] Each success metric has target value
- [ ] Each success metric has measurement method
- [ ] Each success metric has measurement frequency (medium/large)
- [ ] Timeline and Milestones present (medium/large)
- [ ] Stakeholder Impact section present (large)
- [ ] Product Owner approval recorded with date, name, role
- [ ] Project Sponsor approval recorded with date, name, role (medium/large)
- [ ] Budget Authority approval recorded with date, name, role (large)

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Business Case Development Runbook | Runbook | [../runbooks/business-case-runbook.md](../runbooks/business-case-runbook.md) |
| Business Case Template | Template | [../templates/business-case-template.md](../templates/business-case-template.md) |
| Cost-Benefit Analysis Template | Template | [../templates/cost-benefit-analysis-template.md](../templates/cost-benefit-analysis-template.md) |
| Success Metrics Template | Template | [../templates/success-metrics-template.md](../templates/success-metrics-template.md) |
| Project Charter Standard | Standard | [project-charter-standard.md](project-charter-standard.md) |
| Stakeholder Management Standard | Standard | [stakeholder-management-standard.md](stakeholder-management-standard.md) |
