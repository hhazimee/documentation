# Start a Project

## Purpose

This runbook walks you through the four activities required to take a project from an initial business request to a signed project charter. Follow Steps 1 through 4 in order; each step produces artifacts that feed into the next.

---

## Prerequisites

Before starting, confirm the following are in place:

- [ ] A business need or opportunity has been identified by a stakeholder
- [ ] A requesting stakeholder is identified and available
- [ ] An initial business request has been submitted (email, ticket, or verbal with written follow-up)
- [ ] Access to the organizational chart and department directory
- [ ] A project sponsor is identified (department head or above)
- [ ] Project scale has been determined (small / medium / large) to set the compliance level

> **Scaling note:** Small projects (1-2 devs) may use a brief written problem statement and verbal sponsor approval in place of a formal business case. Medium projects (3-5 devs) require all artifacts but may use streamlined formats. Large projects (6+ devs) require full compliance with no reductions.

---

## Step 1: Conduct Business Needs Analysis

**Owner:** Business Analyst | **SLA:** 5 business days | **Approver:** Project Sponsor

1. **Receive the business request.** Log the request in the project intake system with a unique identifier. Capture the requester's contact information and the request description verbatim. If the request was verbal, write it up and get the stakeholder to confirm.

2. **Assess viability.** Check strategic alignment with organizational goals. Confirm preliminary feasibility (technical and operational). Search for duplicate or overlapping initiatives. Assign an initial priority (Critical / High / Medium / Low). Stop if the request duplicates an existing initiative.

3. **Interview key stakeholders.** Identify participants (at minimum the requester and one domain expert). Prepare questions, conduct interviews, and document pain points, goals, and expectations per stakeholder.

4. **Analyze market and competitive context.** Gather relevant market data, assess competitive positioning impact, and identify regulatory or compliance implications. For internal-only needs, document the internal operational context instead.

5. **Quantify business impact.** Assess risk exposure (operational, reputational, regulatory, security). Estimate efficiency gains or losses (FTE hours, cycle time, throughput). Document all assumptions and data sources. Use qualitative assessment if quantitative data is unavailable.

6. **Write the problem statement.** Use the format: *[Who] experiences [what problem] resulting in [what impact].* Describe the current state, the desired future state, and the measurable gap. Have the Product Owner review it.

7. **Validate with the project sponsor.** Present the analysis findings and problem statement. Obtain a decision: Approved, Revise, or Reject. If rejected, document the rationale and close the request.

**Done when:** Problem statement is validated, business impact is quantified, and all findings are consolidated into a Business Needs Analysis artifact.

---

## Step 2: Develop Business Case

**Owner:** Business Analyst | **SLA:** 10 business days | **Approver:** Project Sponsor

> **Entry check:** Step 1 must be complete and the problem statement validated before proceeding.

1. **Define scope boundaries.** List in-scope items (features, processes, systems, user groups) and explicitly list out-of-scope items with rationale. Document assumptions and constraints. Review with the Product Owner.

2. **Assess business value.** Evaluate the initiative against all five value categories below and assign an impact level (High / Medium / Low) to each relevant category:

   | Value Category | What to Look For |
   |----------------|-----------------|
   | Efficiency Gains | Process automation, cycle time reduction, resource optimization, workflow streamlining, data entry reduction |
   | Risk Reduction | Compliance gaps closed, security vulnerabilities addressed, operational stability improved, data integrity, business continuity |
   | Productivity | Team capacity freed, quality improvement, faster knowledge access, better collaboration, faster onboarding |
   | Compliance | Regulatory alignment, policy enforcement, audit readiness, data governance |
   | User Experience | Usability, accessibility, responsiveness, self-service capability, user satisfaction |

   For each category, document the current state, the expected improvement, and confidence level (H/M/L). Define a value realization timeline (when value begins, ramp period, steady state).

   **Go/no-go guidance from the value assessment:**
   - At least one High-impact area with high confidence --> Recommend proceed
   - Multiple Medium-impact areas --> Proceed with conditions (document assumptions)
   - Only Low-impact areas but strong strategic alignment --> Escalate to sponsor
   - No meaningful value areas --> Recommend do not proceed

3. **Assess risks.** Identify technical, business, delivery, and operational risks. Score each by probability and impact (High / Medium / Low). Define mitigation strategies for High and Critical risks. Escalate to the sponsor if any risk is High probability AND High impact.

4. **Define success metrics.** Establish 3-7 KPIs. Each KPI must include: metric name, baseline value, target value, measurement method, and measurement frequency. Identify leading and lagging indicators. Assign ownership per metric.

5. **Draft the business case document.** Use the [business case template](../templates/business-case.md). Include: executive summary (max 1 page), problem statement, scope boundaries, value assessment, risk assessment, success metrics, and a recommendation (Proceed / Proceed with conditions / Do not proceed).

6. **Circulate for stakeholder review.** Distribute to the Product Owner, Tech Lead, and Domain Expert. Allow a minimum of 2 business days for review. Consolidate feedback and revise.

7. **Obtain sponsor approval.** Present the final business case. Record the decision: Approved / Approved with conditions / Rejected / Deferred. Obtain formal written confirmation and communicate the decision to all stakeholders.

**Done when:** Business case is approved by the sponsor with a documented decision, risk register is created, and KPIs are defined with baselines and targets.

---

## Step 3: Identify Stakeholders

**Owner:** Business Analyst and Product Owner | **SLA:** 3 business days | **Approver:** Project Sponsor

> This step can run in parallel with Step 2 once Step 1 is underway.

1. **Review the organizational chart.** Obtain a current org chart (dated within the last 6 months). Map functional areas relevant to the business need, reporting lines, and cross-functional teams.

2. **Identify executive stakeholders.** Find the executive sponsor (decision authority), C-suite or VP-level stakeholders with strategic interest, impacted department heads, and governance or steering committee members.

3. **Identify department-level stakeholders.** Find managers and team leads in directly impacted areas, IT/Engineering leads for affected systems, and HR, Legal, or Compliance contacts if relevant.

4. **Identify end-user and support stakeholders.** Identify primary end-user groups by role or function with estimated user counts. Find help desk leads, training contacts, and operations/infrastructure contacts. For groups larger than 50, identify representative user champions instead of listing individuals.

5. **Identify external stakeholders.** Consider customers, regulators, partners, and vendors. Flag any that require NDA or contractual review before engagement.

6. **Classify by influence and interest.** Score each stakeholder on influence (H/M/L) and interest (H/M/L). Map to quadrants:
   - High Influence / High Interest = **Manage Closely**
   - High Influence / Low Interest = **Keep Satisfied**
   - Low Influence / High Interest = **Keep Informed**
   - Low Influence / Low Interest = **Monitor**

   Validate the classification with the Product Owner.

7. **Create the stakeholder register.** Use the [stakeholder register template](../templates/stakeholder-register.md). Each entry must include: name, title, department, contact info, project role, influence level, interest level, and engagement strategy. Group by category (Executive, Department, End-User/Support, External).

8. **Define communication needs.** For each stakeholder group, document preferred format, frequency, and channel. Note any language or accessibility requirements.

9. **Validate with the project sponsor.** Confirm completeness, validate executive classifications, and capture any political sensitivities.

**Done when:** Stakeholder register is populated, classified, validated by the sponsor, and stored in the project repository.

---

## Step 4: Create Project Charter

**Owner:** Business Analyst | **SLA:** 5 business days | **Approver:** Project Sponsor

> **Entry check:** Step 2 (approved business case) must be complete. Step 3 should be complete or in progress.

1. **Define project objectives.** Extract goals from the approved business case. State each objective in SMART format (Specific, Measurable, Achievable, Relevant, Time-bound). Limit to 5 primary objectives. Review with the Product Owner.

2. **Define high-level scope.** List in-scope deliverables (systems, features, integrations, migrations) and in-scope user groups. Explicitly list out-of-scope items with rationale. Confirm consistency with the approved business case.

3. **Identify constraints.** Document timeline, technology, regulatory, and resource constraints. Classify each as fixed (non-negotiable) or flexible (adjustable with approval). If constraints make the approved scope infeasible, return to the business case for scope revision.

4. **Define high-level milestones.** Set one phase gate milestone per SDLC phase, plus external deadline milestones (regulatory, contractual, market) and key deliverable milestones (MVP, beta, GA). Assign target dates at the month or quarter level.

5. **Assign key roles.** Confirm individuals for: Project Sponsor, Product Owner, Business Analyst, Tech Lead, QA Lead, Operations Lead, and Domain Expert(s). Record allocation percentages. Confirm assignments with each individual's manager. Populate the RACI matrix for Phase 1 activities.

6. **Define the communication approach.** Set status reporting frequency per audience, meeting cadence (standup, steering committee, sponsor check-in), communication channels, escalation path, and decision-making process.

7. **Draft the project charter.** Use the [project charter template](../templates/project-charter.md). Include all sections: project name and identifier, objectives, scope, constraints, milestones, roles, communication approach, and approval/sign-off blocks. Have the Product Owner review before sponsor presentation.

8. **Obtain sponsor sign-off.** Present the charter to the Project Sponsor. Record the decision (Signed / Revise / Reject). Obtain formal sign-off, distribute the signed charter to all key roles, and store it in the project repository.

**Done when:** Charter is signed by the sponsor and distributed to all key roles.

---

## Outputs Checklist

When all four steps are complete, you should have the following artifacts:

| # | Artifact | Produced In | Template |
|---|----------|-------------|----------|
| 1 | Business Needs Analysis | Step 1 | -- |
| 2 | Problem Statement | Step 1 | -- |
| 3 | Stakeholder Interview Notes | Step 1 | -- |
| 4 | Business Case Document | Step 2 | [business-case.md](../templates/business-case.md) |
| 5 | Business Value Assessment | Step 2 | -- |
| 6 | Risk Register | Step 2 | -- |
| 7 | KPI Definition Sheet | Step 2 | -- |
| 8 | Stakeholder Register | Step 3 | [stakeholder-register.md](../templates/stakeholder-register.md) |
| 9 | Influence-Interest Matrix | Step 3 | -- |
| 10 | Project Charter (signed) | Step 4 | [project-charter.md](../templates/project-charter.md) |
| 11 | RACI Matrix | Step 4 | -- |
| 12 | Milestone Schedule | Step 4 | -- |

Confirm these items are stored in `project-repo/phase-1/` before scheduling the Phase 1 gate review. The gate review requires the Project Sponsor and Product Owner as reviewers. See [Phase 1 details](../phases/1-define.md).

---

## Tips

### Sequencing and Timing

1. **Run Step 3 in parallel with Step 2.** Stakeholder identification can begin as soon as the business needs analysis is underway. This saves up to 3 business days on the overall timeline.

2. **Check for duplicate initiatives during Step 1.** Discovering overlap after the business case is written wastes effort. Search the project intake system and talk to department heads before you invest time in the full analysis.

3. **Schedule the kickoff meeting before closing Step 4.** Use the kickoff to walk the team through the framework, roles, timeline, and communication channels. Ensure all team members have read access to the SDLC documentation repository before the meeting.

### Analysis Quality

4. **Start with the problem statement, not the solution.** A well-formed problem statement ([Who] experiences [what problem] resulting in [what impact]) keeps the business case grounded and prevents scope drift before the project even starts.

5. **Match assessment depth to project scale.** Small projects need only 2 value categories at a high level. Medium projects assess all 5 categories with a value realization timeline. Large projects require detailed indicators with supporting evidence. Do not over-engineer a small project or under-document a large one.

6. **Quantify what you can, qualify what you cannot.** When hard numbers are unavailable, use qualitative assessments with documented rationale and flag them for sponsor review. Do not let the absence of perfect data stall the analysis.

7. **Document assumptions explicitly.** Every estimate in the business case rests on assumptions. Write them down, assign a confidence level (High / Medium / Low), and revisit them at the Phase 1 gate review. Unstated assumptions are the top source of scope disputes later.

### Stakeholders and Communication

8. **Use the influence-interest matrix to set communication expectations early.** Stakeholders in the "Manage Closely" quadrant need frequent, detailed updates. Those in "Monitor" need minimal contact. Getting this wrong leads to either stakeholder fatigue or blindside objections later.

9. **Interview at least two people in Step 1.** The minimum is the requester plus one domain expert. A single-source analysis carries significant blind-spot risk. If the requester identifies additional interviewees, schedule follow-up interviews within the SLA.

10. **Identify external stakeholders who need NDA review.** Partners, vendors, and regulators may require contractual review before you can engage them. Flag these early and route to Legal so they do not become blockers in later phases.

### Approvals and Governance

11. **Get written approvals.** Verbal approvals are not sufficient for the business case or charter. Obtain a signature, digital approval, or written confirmation from the sponsor. This protects the project if priorities shift or leadership changes.

12. **Keep the charter concise.** The charter authorizes the project; it does not plan it in detail. Limit objectives to 5, keep milestones at the month or quarter level, and save detailed planning for Phase 2.

13. **Prepare for the Phase 1 gate review.** The gate review requires the Project Sponsor and Product Owner. Assemble all artifacts from the outputs checklist above and distribute them at least 2 business days before the review meeting. Each exit criterion will be evaluated as Met, Partially Met, or Not Met.

14. **Know the abort conditions.** If the requesting stakeholder disappears for more than 3 business days, the business need duplicates an active initiative, strategic priorities shift, or a legal impediment is discovered -- stop work, document the reason, and escalate to the Project Sponsor rather than continuing on inertia.
