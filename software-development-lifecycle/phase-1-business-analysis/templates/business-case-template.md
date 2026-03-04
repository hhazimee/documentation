# Business Case

| Field | Value |
|-------|-------|
| **Template ID** | TPL-P1-001 |
| **When to Use** | To justify a proposed project by documenting costs, benefits, risks, and alternatives for stakeholder approval |
| **Owner** | Business Analyst |
| **Reviewer** | Product Owner |
| **Approver** | Project Sponsor |
| **SLA** | 5 business days |
| **Runbook** | [Develop Business Case](../runbooks/develop-business-case.md) |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Executive Summary, Problem/Opportunity Statement, Proposed Solution, Cost-Benefit Summary, Recommendation, Approval required only
> **IF** medium project (3-5 devs) **THEN** All sections except Alternatives Considered
> **IF** large project (6+ devs) **THEN** Full template required

---

### [ ] Executive Summary

| Field | Value |
|-------|-------|
| **Project Name** | _[Enter project name]_ |
| **Date** | _[YYYY-MM-DD]_ |
| **Author** | _[Name, Role]_ |
| **Version** | _[e.g., 1.0]_ |
| **Summary** | _[2-3 sentence summary of the business case, the problem being solved, and the recommended approach]_ |

---

### [ ] Problem / Opportunity Statement

| Field | Value |
|-------|-------|
| **Current State** | _[Describe the current situation, pain points, or inefficiencies]_ |
| **Impact of Inaction** | _[What happens if nothing is done]_ |
| **Opportunity** | _[Describe the business opportunity or driver]_ |
| **Affected Users/Customers** | _[Who is impacted and how many]_ |
| **Urgency** | _[Low / Medium / High / Critical]_ |

---

### [ ] Proposed Solution (High-Level)

| Field | Value |
|-------|-------|
| **Solution Description** | _[High-level description of the proposed solution]_ |
| **Key Capabilities** | _[Bullet list of what the solution will deliver]_ |
| **Technology Approach** | _[Build / Buy / Integrate / Hybrid]_ |
| **Target Users** | _[Primary and secondary user groups]_ |

---

### [ ] Scope

**In-Scope:**

| # | Item | Description |
|---|------|-------------|
| 1 | _[Item]_ | _[Description]_ |
| 2 | _[Item]_ | _[Description]_ |
| 3 | _[Item]_ | _[Description]_ |

**Out-of-Scope:**

| # | Item | Rationale |
|---|------|-----------|
| 1 | _[Item]_ | _[Why excluded]_ |
| 2 | _[Item]_ | _[Why excluded]_ |
| 3 | _[Item]_ | _[Why excluded]_ |

---

### [ ] Cost Estimate

**Development Costs:**

| Category | Description | Estimate |
|----------|-------------|----------|
| Internal Labor | _[FTEs, hours, rate]_ | _[$X]_ |
| External Labor | _[Contractors, vendors]_ | _[$X]_ |
| Training | _[Team upskilling]_ | _[$X]_ |
| **Development Subtotal** | | **_[$X]_** |

**Infrastructure Costs:**

| Category | Description | Estimate |
|----------|-------------|----------|
| Cloud/Hosting | _[Compute, storage, network]_ | _[$X/month]_ |
| Environments | _[Dev, staging, prod]_ | _[$X/month]_ |
| Tools/Services | _[CI/CD, monitoring, etc.]_ | _[$X/month]_ |
| **Infrastructure Subtotal** | | **_[$X/month]_** |

**Licensing Costs:**

| Category | Description | Estimate |
|----------|-------------|----------|
| Software Licenses | _[Third-party software]_ | _[$X/year]_ |
| API/Service Fees | _[External APIs, SaaS]_ | _[$X/year]_ |
| **Licensing Subtotal** | | **_[$X/year]_** |

**Ongoing Costs (Annual):**

| Category | Description | Estimate |
|----------|-------------|----------|
| Maintenance | _[Bug fixes, patches]_ | _[$X/year]_ |
| Support | _[L1/L2/L3 support]_ | _[$X/year]_ |
| Operations | _[Monitoring, incident response]_ | _[$X/year]_ |
| **Ongoing Subtotal** | | **_[$X/year]_** |

| **Total One-Time Cost** | **_[$X]_** |
|--------------------------|-----------|
| **Total Annual Recurring Cost** | **_[$X/year]_** |

---

### [ ] Benefit Analysis

**Revenue Impact:**

| Benefit | Description | Estimated Value | Timeframe |
|---------|-------------|-----------------|-----------|
| _[Benefit]_ | _[How it drives revenue]_ | _[$X/year]_ | _[When realized]_ |
| _[Benefit]_ | _[How it drives revenue]_ | _[$X/year]_ | _[When realized]_ |

**Cost Savings:**

| Benefit | Description | Estimated Value | Timeframe |
|---------|-------------|-----------------|-----------|
| _[Benefit]_ | _[What cost is reduced]_ | _[$X/year]_ | _[When realized]_ |
| _[Benefit]_ | _[What cost is reduced]_ | _[$X/year]_ | _[When realized]_ |

**Efficiency Gains:**

| Benefit | Description | Estimated Value | Timeframe |
|---------|-------------|-----------------|-----------|
| _[Benefit]_ | _[What process is improved]_ | _[Hours saved / % improvement]_ | _[When realized]_ |
| _[Benefit]_ | _[What process is improved]_ | _[Hours saved / % improvement]_ | _[When realized]_ |

**Risk Reduction:**

| Benefit | Description | Estimated Value | Timeframe |
|---------|-------------|-----------------|-----------|
| _[Benefit]_ | _[What risk is mitigated]_ | _[Qualitative / $X avoided]_ | _[When realized]_ |
| _[Benefit]_ | _[What risk is mitigated]_ | _[Qualitative / $X avoided]_ | _[When realized]_ |

---

### [ ] Cost-Benefit Summary

| Metric | Value |
|--------|-------|
| **Total Investment (Year 1)** | _[$X]_ |
| **Total Annual Benefits** | _[$X/year]_ |
| **Net Present Value (NPV)** | _[$X over N years]_ |
| **Return on Investment (ROI)** | _[X%]_ |
| **Payback Period** | _[X months]_ |
| **Break-Even Point** | _[Date or month]_ |

---

### [ ] Risk Assessment

| # | Risk | Probability | Impact | Risk Score | Mitigation Strategy | Owner |
|---|------|-------------|--------|------------|---------------------|-------|
| 1 | _[Risk description]_ | _[Low/Med/High]_ | _[Low/Med/High]_ | _[L/M/H/Critical]_ | _[Mitigation approach]_ | _[Name]_ |
| 2 | _[Risk description]_ | _[Low/Med/High]_ | _[Low/Med/High]_ | _[L/M/H/Critical]_ | _[Mitigation approach]_ | _[Name]_ |
| 3 | _[Risk description]_ | _[Low/Med/High]_ | _[Low/Med/High]_ | _[L/M/H/Critical]_ | _[Mitigation approach]_ | _[Name]_ |
| 4 | _[Risk description]_ | _[Low/Med/High]_ | _[Low/Med/High]_ | _[L/M/H/Critical]_ | _[Mitigation approach]_ | _[Name]_ |
| 5 | _[Risk description]_ | _[Low/Med/High]_ | _[Low/Med/High]_ | _[L/M/H/Critical]_ | _[Mitigation approach]_ | _[Name]_ |

**Risk Scoring Matrix:**

| | Low Impact | Medium Impact | High Impact |
|---|-----------|---------------|-------------|
| **High Probability** | Medium | High | Critical |
| **Medium Probability** | Low | Medium | High |
| **Low Probability** | Low | Low | Medium |

---

### [ ] Success Metrics / KPIs

| # | Metric/KPI | Baseline | Target | Measurement Method | Measurement Frequency |
|---|-----------|----------|--------|--------------------|-----------------------|
| 1 | _[Metric name]_ | _[Current value]_ | _[Target value]_ | _[How measured]_ | _[Weekly/Monthly/Quarterly]_ |
| 2 | _[Metric name]_ | _[Current value]_ | _[Target value]_ | _[How measured]_ | _[Weekly/Monthly/Quarterly]_ |
| 3 | _[Metric name]_ | _[Current value]_ | _[Target value]_ | _[How measured]_ | _[Weekly/Monthly/Quarterly]_ |

---

### [ ] Timeline (High-Level Milestones)

| # | Milestone | Target Date | Dependencies |
|---|-----------|-------------|--------------|
| 1 | _[Milestone name]_ | _[YYYY-MM-DD]_ | _[Dependencies]_ |
| 2 | _[Milestone name]_ | _[YYYY-MM-DD]_ | _[Dependencies]_ |
| 3 | _[Milestone name]_ | _[YYYY-MM-DD]_ | _[Dependencies]_ |
| 4 | _[Milestone name]_ | _[YYYY-MM-DD]_ | _[Dependencies]_ |
| 5 | _[Milestone name]_ | _[YYYY-MM-DD]_ | _[Dependencies]_ |

---

### [ ] Alternatives Considered

| # | Alternative | Description | Pros | Cons | Estimated Cost | Reason Not Selected |
|---|------------|-------------|------|------|----------------|---------------------|
| 1 | _[Alternative name]_ | _[Brief description]_ | _[Key advantages]_ | _[Key disadvantages]_ | _[$X]_ | _[Why rejected]_ |
| 2 | _[Alternative name]_ | _[Brief description]_ | _[Key advantages]_ | _[Key disadvantages]_ | _[$X]_ | _[Why rejected]_ |
| 3 | Do Nothing | _[Maintain status quo]_ | _[No cost, no disruption]_ | _[Problems persist]_ | _[$0]_ | _[Why rejected]_ |

---

### [ ] Recommendation

| Field | Value |
|-------|-------|
| **Recommended Option** | _[Name of recommended solution]_ |
| **Justification** | _[Why this option is recommended over alternatives]_ |
| **Conditions / Dependencies** | _[Any conditions that must be met for success]_ |
| **Next Steps** | _[Immediate actions if approved]_ |

---

### [ ] Approval

| Role | Name | Signature | Date | Decision |
|------|------|-----------|------|----------|
| Project Sponsor | _[Name]_ | _[Signature]_ | _[YYYY-MM-DD]_ | _[Approved / Rejected / Deferred]_ |
| Product Owner | _[Name]_ | _[Signature]_ | _[YYYY-MM-DD]_ | _[Approved / Rejected / Deferred]_ |
| _[Additional Approver]_ | _[Name]_ | _[Signature]_ | _[YYYY-MM-DD]_ | _[Approved / Rejected / Deferred]_ |

**Comments / Conditions of Approval:**

_[Enter any conditions or comments from approvers]_

---

## COMPLETION CHECKLIST

- [ ] All required sections filled
- [ ] Cost estimates validated with Finance
- [ ] Benefits quantified with supporting data
- [ ] Risk assessment reviewed with stakeholders
- [ ] Success metrics are measurable and time-bound
- [ ] Reviewed by Product Owner
- [ ] Approved by Project Sponsor

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Develop Business Case | Runbook | [../runbooks/develop-business-case.md](../runbooks/develop-business-case.md) |
| Project Charter | Template | [project-charter-template.md](project-charter-template.md) |
| Stakeholder Register | Template | [stakeholder-register-template.md](stakeholder-register-template.md) |
