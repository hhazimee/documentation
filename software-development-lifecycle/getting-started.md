# Getting Started

> Read this first. It tells you what to do, in what order, for any new project.

---

## Your First Project — Step by Step

### 1. Understand the Framework

Read [framework.md](framework.md) to understand:
- The 4 phases (Define → Design → Build & Verify → Ship & Run)
- Your role in the RACI matrix
- How project size affects what you skip

### 2. Set Up ClickUp

Follow [clickup-workflow.md](clickup-workflow.md) to:
- Create a Space for your project
- Set up folders for each phase
- Configure custom fields and views

### 3. Phase 1: Define

Open [phases/1-define.md](phases/1-define.md) and work through the deliverables:

1. **Business Case** — Use [templates/business-case.md](templates/business-case.md), follow [runbooks/start-a-project.md](runbooks/start-a-project.md)
2. **Project Charter** — Use [templates/project-charter.md](templates/project-charter.md)
3. **Stakeholder Register** — Use [templates/stakeholder-register.md](templates/stakeholder-register.md)
4. **BRD** — Use [templates/business-requirements-document.md](templates/business-requirements-document.md), follow [runbooks/gather-requirements.md](runbooks/gather-requirements.md)
5. **SRS** (medium+ projects) — Use [templates/software-requirements-specification.md](templates/software-requirements-specification.md)
6. **Use Cases** (medium+ projects) — Use [templates/use-case.md](templates/use-case.md)
7. **RTM** (medium+ projects) — Use [templates/requirements-traceability-matrix.md](templates/requirements-traceability-matrix.md)

**Gate:** All deliverables reviewed → [runbooks/conduct-reviews.md](runbooks/conduct-reviews.md)

### 4. Phase 2: Design

Open [phases/2-design.md](phases/2-design.md) and produce:

1. **Architecture Description Document** — Use [templates/architecture-description-document.md](templates/architecture-description-document.md)
2. **ADRs** — Use [templates/architecture-decision-record.md](templates/architecture-decision-record.md)
3. **Detailed Design Document** (medium+) — Use [templates/detailed-design-document.md](templates/detailed-design-document.md)
4. **API Specification** (if API) — Use [templates/api-specification.md](templates/api-specification.md)
5. **Data Model Document** (if DB) — Use [templates/data-model-document.md](templates/data-model-document.md)
6. **PlantUML Diagrams** — Templates in [diagrams/](diagrams/)

Follow [runbooks/architect-and-design.md](runbooks/architect-and-design.md) for step-by-step guidance.

**Gate:** Architecture + Design reviews → [runbooks/conduct-reviews.md](runbooks/conduct-reviews.md)

### 5. Phase 3: Build & Verify

Open [phases/3-build-and-verify.md](phases/3-build-and-verify.md).

**Development:**
1. Set up environment → [runbooks/setup-dev-environment.md](runbooks/setup-dev-environment.md)
2. Implement features → [runbooks/implement-feature.md](runbooks/implement-feature.md)
3. Follow coding standards → [standards/coding-and-git.md](standards/coding-and-git.md)
4. Submit PRs using [templates/pull-request.md](templates/pull-request.md)
5. Review code → [standards/code-review.md](standards/code-review.md)

**Testing:**
1. Write test plan → [templates/test-plan.md](templates/test-plan.md)
2. Execute tests → [runbooks/run-test-cycle.md](runbooks/run-test-cycle.md)
3. Follow testing standards → [standards/testing.md](standards/testing.md)
4. Get UAT sign-off → [templates/uat-sign-off.md](templates/uat-sign-off.md)

**Gate:** All tests pass, UAT signed off

### 6. Phase 4: Ship & Run

Open [phases/4-ship-and-run.md](phases/4-ship-and-run.md).

1. Deploy → [runbooks/deploy-and-operate.md](runbooks/deploy-and-operate.md)
2. Monitor
3. Operate

---

## Project Size Guide

| Size | Duration | What to Skip |
|------|----------|-------------|
| **Small** | < 2 weeks | SRS, Use Cases, RTM, DDD, formal test plan. Simplified BRD, 1-page ADD. |
| **Medium** | 2-8 weeks | Full BRD + SRS. Simplified DDD. All diagrams. Formal test plan. |
| **Large** | 8+ weeks | Everything required. No shortcuts. |

---

## Need Help?

- **"What document do I need?"** → [references/artifacts-checklist.md](references/artifacts-checklist.md)
- **"What does this term mean?"** → [references/glossary.md](references/glossary.md)
- **"How do I classify a defect?"** → [references/defect-severity.md](references/defect-severity.md)
- **"What does a finished project look like?"** → [example-project/](example-project/)
- **"How do I update these docs?"** → [maintaining-docs.md](maintaining-docs.md)
