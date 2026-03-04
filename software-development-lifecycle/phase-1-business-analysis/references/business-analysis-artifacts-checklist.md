# Business Analysis Artifacts Checklist

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P1-001 |
| **Use When** | Determining which Phase 1 artifacts are required for a project and verifying completeness before Phase 1 gate review |
| **Last Updated** | 2026-03-04 |

---

## ARTIFACT REGISTER

| Artifact | Description | Owner | Format | Required | Approval Authority |
|----------|-------------|-------|--------|----------|--------------------|
| Business Case | Justification for the project including problem, proposed solution, cost-benefit analysis, and strategic alignment | Business Analyst | Document (Markdown/PDF) | Yes | Project Sponsor |
| Project Charter | Formal authorization defining scope, objectives, constraints, assumptions, high-level timeline, and budget | Product Owner | Document (Markdown/PDF) | Yes | Project Sponsor |
| Stakeholder Register | Catalog of all identified stakeholders with roles, influence, interest, communication preferences, and engagement strategy | Business Analyst | Spreadsheet/Table | Yes | Product Owner |
| Problem Statement | Concise description of the business problem: who is affected, what the problem is, and the measurable impact | Business Analyst | Document (Markdown/PDF) | Yes | Product Owner |
| Cost-Benefit Analysis | Detailed financial analysis including cost categories, benefit categories, ROI calculation, payback period, and NPV | Business Analyst | Spreadsheet/Document | Conditional (see decision tree) | Project Sponsor |

---

## ARTIFACT DETAIL -- FORMAT AND CONTENT

| Artifact | Required Sections | Minimum Length | Review Cycle |
|----------|-------------------|----------------|--------------|
| Business Case | Problem Statement, Proposed Solution, Strategic Alignment, Cost-Benefit Summary, Risk Summary, Recommendation | 3-5 pages | 1 review before gate |
| Project Charter | Purpose, Scope, Objectives, Constraints, Assumptions, Stakeholders, High-Level Timeline, Budget, Approval Signatures | 2-3 pages | 1 review before gate |
| Stakeholder Register | Name, Role, Organization, Influence (H/M/L), Interest (H/M/L), Communication Preference, Engagement Level | 1 entry per stakeholder | Updated continuously |
| Problem Statement | Who, What Problem, What Impact, Current State, Desired State, Measurable Gap | 0.5-1 page | 1 review by Product Owner |
| Cost-Benefit Analysis | Cost Categories, Benefit Categories, ROI Calculation, Payback Period, NPV (if applicable), Assumptions | 2-4 pages | 1 review before gate |

---

## COMPLETION CHECKLIST

### Business Case
- [ ] Problem statement included and validated
- [ ] Proposed solution(s) described with rationale
- [ ] Strategic alignment to organizational goals documented
- [ ] Cost-benefit summary included (or cross-referenced to standalone CBA)
- [ ] Key risks identified with preliminary mitigation
- [ ] Recommendation stated with supporting evidence
- [ ] Project Sponsor approval obtained

### Project Charter
- [ ] Project purpose and justification stated
- [ ] Scope defined (in-scope and out-of-scope)
- [ ] SMART objectives defined
- [ ] Constraints and assumptions documented
- [ ] High-level timeline with milestones established
- [ ] Budget estimate included
- [ ] Key stakeholders listed
- [ ] Project Sponsor signature obtained

### Stakeholder Register
- [ ] All known stakeholders identified
- [ ] Influence and interest levels assessed for each stakeholder
- [ ] Communication preferences documented
- [ ] Engagement strategy defined per stakeholder
- [ ] Register reviewed by Product Owner

### Problem Statement
- [ ] Follows format: [Who] experiences [what problem] resulting in [what impact]
- [ ] Current state described
- [ ] Desired future state described
- [ ] Measurable gap between current and desired state defined
- [ ] Reviewed and confirmed by Product Owner

### Cost-Benefit Analysis
- [ ] All cost categories identified and estimated
- [ ] All benefit categories identified and estimated
- [ ] ROI calculated with documented formula
- [ ] Payback period calculated
- [ ] NPV calculated (large projects only)
- [ ] All assumptions documented
- [ ] Sensitivity analysis performed (large projects only)
- [ ] Project Sponsor approval obtained

### Phase 1 Gate Readiness
- [ ] All required artifacts produced per project scale
- [ ] All artifacts reviewed by designated approval authority
- [ ] All approval signatures obtained
- [ ] Artifacts stored in designated repository
- [ ] Phase 1 gate review scheduled

---

## DECISION TREE

### Is This Artifact Required for My Project Size?

```
IF project scale is SMALL (1-2 developers)
    THEN required artifacts:
        - Business Case: YES (streamlined format, 1-2 pages)
        - Project Charter: YES (streamlined format, 1 page)
        - Stakeholder Register: YES (simplified, key stakeholders only)
        - Problem Statement: YES (included in Business Case, not standalone)
        - Cost-Benefit Analysis: NO (summary in Business Case is sufficient)

ELSE IF project scale is MEDIUM (3-5 developers)
    THEN required artifacts:
        - Business Case: YES (full format)
        - Project Charter: YES (full format)
        - Stakeholder Register: YES (full format)
        - Problem Statement: YES (standalone document)
        - Cost-Benefit Analysis: YES (standard depth, ROI + payback period)

ELSE IF project scale is LARGE (6+ developers)
    THEN required artifacts:
        - Business Case: YES (full format with executive summary)
        - Project Charter: YES (full format)
        - Stakeholder Register: YES (full format with engagement plan)
        - Problem Statement: YES (standalone document)
        - Cost-Benefit Analysis: YES (full depth, ROI + payback period + NPV + sensitivity analysis)
```

### Is the Phase 1 Gate Ready?

```
IF all required artifacts for project scale are produced
    AND all artifacts reviewed by designated approval authority
    AND all approval signatures obtained
    THEN Phase 1 gate is READY
ELSE
    THEN identify missing/unapproved artifacts → complete before scheduling gate review
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Conduct Business Needs Analysis | Runbook | ../runbooks/conduct-business-needs-analysis.md |
| Business Case Development | Runbook | ../runbooks/develop-business-case.md |
| Project Charter Creation | Runbook | ../runbooks/create-project-charter.md |
| Initial Stakeholder Identification | Runbook | ../runbooks/conduct-initial-stakeholder-identification.md |
| Cost-Benefit Analysis Reference | Reference | ./cost-benefit-analysis-reference.md |
| Business Analysis RACI Matrix | Reference | ./business-analysis-raci-matrix.md |
| SDLC Framework Standard | Standard | ../../standards/sdlc-framework.md |
| Phase 1 Standards | Standard | ../standards/phase-1-standards.md |
| Stakeholder Analysis Template | Template | ../../templates/stakeholder-analysis-template.md |
| Glossary | Reference | ../../references/glossary.md |
