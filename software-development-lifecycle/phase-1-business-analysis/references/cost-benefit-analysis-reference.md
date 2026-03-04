# Cost-Benefit Analysis Reference

| Field | Value |
|-------|-------|
| **Reference ID** | REF-P1-003 |
| **Use When** | Performing cost-benefit analysis during business case development or evaluating project financial viability |
| **Last Updated** | 2026-03-04 |

---

## COST CATEGORIES

### Development Costs

| Category | Sub-Category | Description | Estimation Method | Typical Range |
|----------|-------------|-------------|-------------------|---------------|
| Labor | Internal developers | Salaries/rates for development team members | FTE x duration x rate | 60-70% of total dev cost |
| Labor | Business Analyst | Requirements and analysis effort | FTE x duration x rate | 10-15% of total dev cost |
| Labor | QA/Testing | Testing and quality assurance effort | FTE x duration x rate | 15-25% of total dev cost |
| Labor | Project management | PM/coordination overhead | FTE x duration x rate | 5-10% of total dev cost |
| Labor | External contractors | Contract/vendor development resources | Contract rate x duration | Variable |
| Tools | Development tools | IDE licenses, CI/CD tooling, code analysis | Per-seat or per-org license | Annual recurring |
| Tools | Design tools | Prototyping, wireframing, diagramming | Per-seat license | Annual recurring |
| Training | Team upskilling | Training for new technologies or methodologies | Course cost + time away | One-time per skill gap |
| Training | Onboarding | New team member ramp-up time | Reduced productivity x duration | 2-4 weeks per new member |

### Infrastructure Costs

| Category | Sub-Category | Description | Estimation Method | Typical Range |
|----------|-------------|-------------|-------------------|---------------|
| Hosting | Cloud compute | Servers, containers, serverless execution | Usage-based or reserved | Monthly recurring |
| Hosting | Storage | Database storage, object storage, backups | GB/TB x rate | Monthly recurring |
| Hosting | Network | Data transfer, CDN, load balancers | Usage-based | Monthly recurring |
| Hosting | Environments | Dev, staging, UAT, production environments | Per-environment cost | Monthly recurring |
| Licensing | Third-party APIs | External service integrations | Per-call or subscription | Monthly/annual recurring |
| Licensing | Software licenses | Databases, middleware, monitoring tools | Per-seat or per-instance | Annual recurring |
| Maintenance | Patching/updates | Ongoing infrastructure maintenance | FTE x hours/month | Monthly recurring |
| Maintenance | Disaster recovery | Backup infrastructure, failover systems | % of primary infrastructure | Monthly recurring |

### Operational Costs

| Category | Sub-Category | Description | Estimation Method | Typical Range |
|----------|-------------|-------------|-------------------|---------------|
| Support | L1/L2 support | Help desk and application support | FTE x hours/month | Monthly recurring |
| Support | L3 support | Engineering escalation support | % of dev team time | Monthly recurring |
| Support | Documentation | User guides, knowledge base maintenance | FTE x hours/quarter | Quarterly recurring |
| Monitoring | Application monitoring | APM, logging, alerting tools | Per-host or per-GB | Monthly recurring |
| Monitoring | Security monitoring | SIEM, vulnerability scanning, pen testing | Subscription + periodic testing | Monthly/annual recurring |
| Monitoring | Compliance auditing | Regulatory compliance verification | Audit cost x frequency | Annual recurring |

---

## BENEFIT CATEGORIES

### Revenue Benefits

| Category | Sub-Category | Description | Measurement Method |
|----------|-------------|-------------|-------------------|
| New Revenue | New product/feature revenue | Revenue from new capabilities not previously available | Projected sales x price point |
| New Revenue | New market access | Revenue from entering new customer segments | Market size x capture rate |
| Increased Conversion | Conversion rate improvement | Additional revenue from higher conversion rates | Current traffic x conversion delta x avg revenue |
| Increased Conversion | Reduced churn | Retained revenue from improved customer retention | Churn reduction x avg customer value |
| Increased Conversion | Upsell/cross-sell | Revenue from enhanced product capabilities | Eligible customers x upsell rate x value |

### Cost Savings Benefits

| Category | Sub-Category | Description | Measurement Method |
|----------|-------------|-------------|-------------------|
| Automation | Manual process elimination | FTE hours saved by automating manual tasks | Hours saved/month x hourly rate |
| Automation | Error reduction | Cost avoided by eliminating manual errors | Error rate reduction x avg error cost |
| Efficiency | Cycle time reduction | Value of faster process completion | Time saved x throughput x value |
| Efficiency | Resource optimization | Reduced infrastructure or staffing needs | Current cost - projected cost |
| Efficiency | Vendor consolidation | Savings from replacing multiple tools/vendors | Current vendor costs - new solution cost |

### Risk Reduction Benefits

| Category | Sub-Category | Description | Measurement Method |
|----------|-------------|-------------|-------------------|
| Compliance | Regulatory compliance | Avoided fines and penalties for non-compliance | Probability of violation x penalty amount |
| Compliance | Audit readiness | Reduced audit preparation effort | Hours saved x rate |
| Security | Breach prevention | Avoided cost of security incidents | Probability of breach x avg breach cost |
| Security | Data protection | Avoided cost of data loss/exposure | Probability x (legal + remediation + reputation cost) |
| Operational | Downtime reduction | Avoided revenue loss from system outages | Downtime reduction x revenue/hour |
| Operational | Business continuity | Avoided losses from disaster scenarios | Probability x impact |

---

## FORMULA REFERENCE

### Return on Investment (ROI)

```
ROI = ((Total Benefits - Total Costs) / Total Costs) x 100

Where:
  Total Benefits = Sum of all quantified benefits over evaluation period
  Total Costs    = Sum of all costs (development + infrastructure + operational) over evaluation period

Example:
  Total Benefits = $500,000 (over 3 years)
  Total Costs    = $200,000 (over 3 years)
  ROI = (($500,000 - $200,000) / $200,000) x 100 = 150%
```

| ROI Range | Interpretation |
|-----------|---------------|
| < 0% | Project costs exceed benefits -- not financially justified |
| 0-50% | Low return -- requires strong strategic justification |
| 50-100% | Moderate return -- generally acceptable |
| 100-200% | Strong return -- well justified |
| > 200% | Exceptional return -- high priority candidate |

### Payback Period

```
Payback Period = Total Investment / Annual Net Benefit

Where:
  Total Investment   = All upfront and one-time costs (development + initial infrastructure)
  Annual Net Benefit = (Annual Benefits - Annual Recurring Costs)

Example:
  Total Investment   = $150,000
  Annual Net Benefit = $75,000
  Payback Period     = $150,000 / $75,000 = 2.0 years
```

| Payback Period | Interpretation |
|----------------|---------------|
| < 1 year | Rapid payback -- strong financial case |
| 1-2 years | Acceptable payback -- standard justification |
| 2-3 years | Extended payback -- requires strategic justification |
| > 3 years | Long payback -- requires executive sponsor approval and strategic alignment |

### Net Present Value (NPV)

```
NPV = Sum of [Net Cash Flow(t) / (1 + r)^t] for t = 0 to n

Where:
  Net Cash Flow(t) = Benefits(t) - Costs(t) in year t
  r                = Discount rate (see table below)
  n                = Number of years in evaluation period
  t                = Year (0 = initial investment)

Example (3-year, 10% discount rate):
  Year 0: -$150,000 / (1.10)^0 = -$150,000
  Year 1:  +$75,000 / (1.10)^1 =  +$68,182
  Year 2:  +$75,000 / (1.10)^2 =  +$61,983
  Year 3:  +$75,000 / (1.10)^3 =  +$56,349
  NPV = -$150,000 + $68,182 + $61,983 + $56,349 = +$36,514
```

### Discount Rate Guidance

| Project Risk Profile | Recommended Discount Rate | When to Use |
|----------------------|---------------------------|-------------|
| Low risk | 5-8% | Internal efficiency projects, proven technology, stable market |
| Medium risk | 8-12% | New feature development, moderate technical complexity |
| High risk | 12-18% | New product/market, unproven technology, significant uncertainty |
| Very high risk | 18-25% | Experimental/R&D projects, highly volatile market conditions |

| NPV Result | Interpretation |
|------------|---------------|
| NPV > 0 | Project adds value -- financially justified |
| NPV = 0 | Project breaks even in present value terms |
| NPV < 0 | Project destroys value -- not financially justified without strategic override |

---

## DECISION TREE

### Which Analysis Depth Is Required?

```
IF project scale is SMALL (1-2 developers)
    THEN analysis depth: BASIC
        - Cost estimate: Order-of-magnitude (+/- 50%)
        - Benefit estimate: Qualitative or rough quantitative
        - Required calculations: ROI only
        - Format: Summary table in Business Case (not standalone)
        - NPV: NOT REQUIRED
        - Sensitivity analysis: NOT REQUIRED

ELSE IF project scale is MEDIUM (3-5 developers)
    THEN analysis depth: STANDARD
        - Cost estimate: Budget-level (+/- 25%)
        - Benefit estimate: Quantitative with documented assumptions
        - Required calculations: ROI + Payback Period
        - Format: Standalone CBA document
        - NPV: RECOMMENDED but not required
        - Sensitivity analysis: NOT REQUIRED

ELSE IF project scale is LARGE (6+ developers)
    THEN analysis depth: COMPREHENSIVE
        - Cost estimate: Definitive (+/- 10%)
        - Benefit estimate: Quantitative with data-backed assumptions
        - Required calculations: ROI + Payback Period + NPV
        - Format: Standalone CBA document with executive summary
        - NPV: REQUIRED
        - Sensitivity analysis: REQUIRED (best case / expected / worst case)
```

### Is the CBA Sufficient for Gate Review?

```
IF all required calculations for project scale are complete
    AND all cost categories relevant to project are estimated
    AND all benefit categories relevant to project are estimated
    AND all assumptions are documented
    AND ROI > 0% OR strategic justification is documented
    THEN CBA is SUFFICIENT for gate review
ELSE
    THEN identify gaps → complete before gate review
```

### Should the Project Proceed Based on CBA?

```
IF ROI > 50% AND Payback Period < 2 years
    THEN RECOMMEND: Proceed
ELSE IF ROI > 0% AND Payback Period < 3 years
    THEN RECOMMEND: Proceed with conditions (document risk mitigation)
ELSE IF ROI < 0% BUT strategic justification exists
    THEN ESCALATE to Project Sponsor for go/no-go decision
ELSE IF ROI < 0% AND no strategic justification
    THEN RECOMMEND: Do not proceed
```

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Conduct Business Needs Analysis | Runbook | ../runbooks/conduct-business-needs-analysis.md |
| Business Case Development | Runbook | ../runbooks/develop-business-case.md |
| Business Analysis Artifacts Checklist | Reference | ./business-analysis-artifacts-checklist.md |
| Business Analysis RACI Matrix | Reference | ./business-analysis-raci-matrix.md |
| SDLC Framework Standard | Standard | ../../standards/sdlc-framework.md |
| Phase 1 Standards | Standard | ../standards/phase-1-standards.md |
| Glossary | Reference | ../../references/glossary.md |
