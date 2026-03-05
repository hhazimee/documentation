# Phase 2: Design (Architecture + Detailed Design)

> **Purpose:** Define the fundamental structure of the system -- components, interfaces, deployment topology, and technology choices -- aligned with ISO/IEC/IEEE 42010. Then translate that architecture into implementation-level specifications (API contracts, data models, module internals) so developers can build without ambiguity.

---

## Entry Criteria

- [ ] Phase 1 (Define) gate passed
- [ ] BRD approved
- [ ] Software Requirements Specification (SRS) baselined and approved
- [ ] Requirements Traceability Matrix (RTM) populated with BR-to-SWR links
- [ ] All Must Have requirements have passed validation
- [ ] Architecture-Significant Requirements (ASRs) explicitly identified
- [ ] All NFR categories reviewed (performance, security, scalability, reliability, maintainability, compliance)
- [ ] System Architect and Tech Lead assigned

---

## Deliverables

| # | Document | Template | Required | Runbook |
|---|----------|----------|----------|---------|
| 1 | Architecture Description Document (ADD) | [templates/architecture-description-document.md](../templates/architecture-description-document.md) | All projects | [runbooks/architect-and-design.md](../runbooks/architect-and-design.md) |
| 2 | Architecture Decision Records (ADRs) | [templates/architecture-decision-record.md](../templates/architecture-decision-record.md) | All projects | [runbooks/architect-and-design.md](../runbooks/architect-and-design.md) |
| 3 | Detailed Design Document (DDD) | [templates/detailed-design-document.md](../templates/detailed-design-document.md) | Medium+ | [runbooks/architect-and-design.md](../runbooks/architect-and-design.md) |
| 4 | API Specification | [templates/api-specification.md](../templates/api-specification.md) | If API exists | [runbooks/architect-and-design.md](../runbooks/architect-and-design.md) |
| 5 | Data Model Document | [templates/data-model-document.md](../templates/data-model-document.md) | If DB exists | [runbooks/architect-and-design.md](../runbooks/architect-and-design.md) |

---

## Required PlantUML Diagrams

| # | Diagram | Template (.puml) | Required |
|---|---------|-------------------|----------|
| D1 | System Context Diagram | [diagrams/system-context-diagram.puml](../diagrams/system-context-diagram.puml) | All projects |
| D2 | Component Diagram | [diagrams/component-diagram.puml](../diagrams/component-diagram.puml) | All projects |
| D3 | Deployment Diagram | [diagrams/deployment-diagram.puml](../diagrams/deployment-diagram.puml) | All projects |
| D4 | ERD (Entity-Relationship) | [diagrams/erd-diagram.puml](../diagrams/erd-diagram.puml) | If DB exists |
| D5 | Sequence Diagram(s) | [diagrams/sequence-diagram.puml](../diagrams/sequence-diagram.puml) | Key flows only |
| D6 | State Diagram(s) | [diagrams/state-diagram.puml](../diagrams/state-diagram.puml) | If stateful entities |
| D7 | Class Diagram | [diagrams/class-diagram.puml](../diagrams/class-diagram.puml) | Medium+ |
| D8 | API Flow Diagram | [diagrams/api-flow-diagram.puml](../diagrams/api-flow-diagram.puml) | If API exists |
| D9 | Data Flow Diagram | [diagrams/data-flow-diagram.puml](../diagrams/data-flow-diagram.puml) | Medium+ |

---

## Key Activities

### Architecture (System-Level)

1. **Identify Architecture-Significant Requirements (ASRs)** -- Extract from SRS any requirement that drives technology choice, defines a scalability/performance threshold, mandates security controls, or specifies data retention. Every ASR gets a corresponding ADR.
2. **Select architecture style** -- Evaluate monolith, modular monolith, microservices, or event-driven against team size, domain complexity, and DevOps maturity. Default recommendation: start with modular monolith.
3. **Define component boundaries** -- Cluster related functional requirements (SWRs) to identify service/module boundaries. Define data ownership and interface contracts for each component.
4. **Address NFRs structurally** -- Map each NFR category (performance, security, reliability, scalability) to an architectural approach (caching, auth middleware, failover, connection pooling).
5. **Document failure modes** -- For every external dependency and inter-component interaction, document what fails, how it is detected, retry strategy, fallback, and alerting.
6. **Create architecture diagrams** -- System context, component, deployment, ERD, sequence, and state diagrams in PlantUML.
7. **Write ADRs** -- One ADR per significant technology or pattern choice (30 min each). Record rationale and alternatives considered.
8. **Conduct architecture review** -- [runbooks/conduct-reviews.md](../runbooks/conduct-reviews.md)

### Detailed Design (Component-Level)

1. **Transform architecture to design** -- For each component, define internal module structure: controller, service, repository, entity, DTOs, events, tests.
2. **Specify API contracts** -- Method, endpoint, request/response schemas, error responses, pagination, and validation rules for every exposed REST API.
3. **Design data models** -- Table definitions with columns, types, constraints, indexes. Add caching/indexing only where NFR demands it.
4. **Specify business logic** -- Pseudocode or step-by-step algorithms for non-trivial operations (e.g., fee calculations, event handlers).
5. **Define event contracts** -- For each published/consumed event: name, payload schema, trigger point, deduplication strategy.
6. **Apply SOLID principles** -- Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion.
7. **Conduct design review** -- [runbooks/conduct-reviews.md](../runbooks/conduct-reviews.md)

---

## Standards

- [Architecture & Design Standard](../standards/architecture-and-design.md) -- architecture descriptions, ADRs, system decomposition, API design, database design, UI design

---

## Top 5 Pitfalls

| # | Pitfall | Warning Sign | Fix |
|---|---------|-------------|-----|
| 1 | **Over-engineering** | 3 devs managing 8 microservices; 7+ files to trace a simple GET | Match architecture to team size; start with modular monolith. Max 3 layers (Controller -> Service -> Repository). |
| 2 | **Ignoring NFRs** | No mention of performance, security, or reliability in ADD; only 200 responses in API spec | Address every NFR category before development. Document all error responses per endpoint. |
| 3 | **Skipping ADRs** | "Why did we choose X?" has no documented answer | Write an ADR for every significant technology/pattern choice (30 min each). |
| 4 | **Tight coupling** | Schema changes break multiple services; SDK calls scattered across business logic | Components communicate only through APIs or events. External APIs accessed through Adapter pattern. |
| 5 | **Missing failure & edge-case analysis** | Architecture shows only the happy path; no idempotency on financial POSTs | Document failure modes for every dependency. Require Idempotency-Key headers. Add optimistic locking for concurrent edits. |

---

## Exit Criteria / Phase Gate

- [ ] ADD reviewed and approved (by Tech Lead, System Architect, and Product Owner)
- [ ] All ADRs documented for architecture-significant decisions
- [ ] Architecture review conducted -- [runbooks/conduct-reviews.md](../runbooks/conduct-reviews.md)
- [ ] Design review conducted -- [runbooks/conduct-reviews.md](../runbooks/conduct-reviews.md)
- [ ] All required PlantUML diagrams committed to `diagrams/` directory
- [ ] DDD approved (Medium+ projects)
- [ ] API specifications complete with error responses, pagination, and validation rules
- [ ] Data models defined with constraints and indexes
- [ ] RTM updated with architecture component and ADR references
- [ ] No implementation story starts until its design is reviewed and approved

---

## Scaling Notes

| Project Size | Skip/Simplify |
|-------------|---------------|
| Small (< 2 weeks) | ADD can be 1 page. Skip DDD. 1 ADR for tech stack. System context + component diagrams only. |
| Medium (2-8 weeks) | Full ADD, simplified DDD. ADRs for major decisions. All required diagrams. Class + data flow diagrams added. |
| Large (8+ weeks) | All deliverables and diagrams required. Full DDD per component. API specs and data models mandatory. |

---

## Next Phase

→ [Phase 3: Build & Verify](3-build-and-verify.md)

---

## Previous Phase

← [Phase 1: Define](1-define.md)

---

## Roles

| Role | Architecture Responsibility | Design Responsibility |
|------|---------------------------|----------------------|
| Tech Lead / System Architect | Owns ADD, writes ADRs, leads architecture review | Reviews detailed designs, approves API contracts |
| Developer | Contributes to ADRs, reviews component diagrams | Writes DDD, designs APIs and data models |
| Business Analyst | Maps requirements to architecture components | Validates designs against BRD/SRS |
| Product Owner | Reviews architecture for business alignment | Approves API scope, validates UI wireframes |
| QA Lead | Reviews testability of architecture | Reviews test hooks in design, validates coverage feasibility |

---

## Phase 2 Outputs Feed Phase 3

| Phase 2 Output | Consumed By (Phase 3) |
|----------------|----------------------|
| ADD (component structure) | Developers use to scope implementation tickets |
| ADRs (technology choices) | Developers follow for tech stack and patterns |
| DDD (module internals) | Developers implement to specification |
| API Specification | Developers implement endpoints; QA derives integration tests |
| Data Model | Developers create migrations; QA validates data integrity |
| PlantUML Diagrams | Developers reference for system context; update as design evolves |
| RTM Updates | BA traces design components back to requirements |
