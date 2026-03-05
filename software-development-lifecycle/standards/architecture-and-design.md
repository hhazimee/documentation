# Architecture and Design Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-AD-001 |
| **Source Standards** | STD-P3-001, STD-P3-002, STD-P3-003, STD-P4-001, STD-P4-002, STD-P4-003, STD-P4-004 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Last Verified** | 2026-03-05 |

---

## 1. Purpose

This standard defines how teams produce architecture and design artifacts -- from system-level architecture descriptions and decision records down to API contracts, database schemas, and UI specifications. It merges Phase 3 (System Architecture) and Phase 4 (Design) rules into a single operational reference. Every project must comply with the sections below, scaled by team size as noted.

---

## 2. Architecture Description Standard

The Architecture Description Document (ADD) is the single source of truth for system structure. Use the template at [../templates/architecture-description-document.md](../templates/architecture-description-document.md).

### Scaling Gate

| Team Size | Required |
|-----------|----------|
| Small (1-2 devs) | Sections 1-5, 10, 11 mandatory; rest optional |
| Medium (3-5 devs) | All sections; Deployment and Development views may combine |
| Large (6+ devs) | Full compliance |

### Required ADD Sections

| # | Section | Key Content |
|---|---------|-------------|
| 1 | Introduction | Purpose, scope, definitions, references |
| 2 | Architecture Goals and Constraints | Business and technical drivers |
| 3 | Stakeholder Concerns | Concerns mapped to viewpoints |
| 4 | System Context View | System boundary, external interactions |
| 5 | Logical/Functional View | Components, responsibilities, interfaces |
| 6 | Process/Runtime View | Data flows, concurrency, communication |
| 7 | Deployment View | Infrastructure, networking, environments |
| 8 | Development View | Code organization, build structure, repos |
| 9 | Quality Attribute Approaches | Performance, security, scalability, reliability strategies |
| 10 | Technology Stack | Technologies with selection rationale |
| 11 | Architecture Decisions | ADR references |
| 12 | Risks and Mitigations | Known architectural risks |
| 13 | Traceability | Requirements-to-architecture mapping |

### Quality Attributes -- Required Approaches

Document a concrete strategy for each:

| Attribute | Examples |
|-----------|----------|
| Performance | Caching, connection pooling, async processing, CDN |
| Security | Auth mechanism, authorization model, encryption, secrets management |
| Scalability | Horizontal/vertical scaling, stateless design, DB scaling |
| Reliability | Redundancy, failover, health checks, circuit breakers, retries |
| Maintainability | Modularity, loose coupling, dependency injection, config externalization |

### Technology Selection Documentation

Every technology choice must document: **name/version, purpose, alternatives considered, selection rationale, risks, license**. Significant choices (database, framework, message broker, cloud provider) require a formal ADR.

---

## 3. Architecture Decision Records

ADRs capture the "why" behind significant technical choices. Use the template at [../templates/architecture-decision-record.md](../templates/architecture-decision-record.md).

### When an ADR Is Required

Write an ADR for any decision involving: technology choices, architecture patterns, integration approaches, framework/library selections, infrastructure, security mechanisms, data storage approaches, trade-offs (e.g., consistency vs. availability), protocol or format choices.

### ADR Format

Every ADR must contain:

| Field | Content |
|-------|---------|
| **Status** | Proposed / Accepted / Deprecated / Superseded by ADR-XXX |
| **Date** | YYYY-MM-DD |
| **Context** | Situation, forces, constraints, requirement IDs |
| **Decision** | Clear statement: "We will use [X] for [Y]" |
| **Consequences** | Positive, Negative, and Risks subsections |
| **Alternatives Considered** | Description, pros, cons, rejection reason per alternative |

### Numbering and Storage

- Format: `ADR-XXX`, assigned sequentially, never reused.
- File name: `XXX-short-description.md` (e.g., `001-use-mqtt-for-iot-telemetry.md`).
- Location: `architecture/decisions/` within the relevant topic directory.

### Lifecycle

Proposed --> Accepted --> Deprecated or Superseded. Deprecated ADRs must include deprecation reason and date. Superseded ADRs must reference the replacing ADR.

---

## 4. System Decomposition

### Component Identification Rules

| Rule | Detail |
|------|--------|
| Single responsibility | Each component has one reason to change |
| Well-defined interface | Every component exposes a documented interface |
| Independent testability | Each component can be developed and tested in isolation |
| Business capability mapping | Components identified from business capabilities |
| Data ownership | Each component owns its data; no cross-boundary direct DB access |
| Change coupling | Components that always change together -- evaluate for merging |

### Service Boundary Definition

Each service must document: **responsibility statement** (one sentence), **owned data** (source-of-truth entities), **exposed interface** (API endpoints), **consumed interfaces** (dependencies), **events published**, **events consumed**.

### Integration Patterns

| Pattern | When to Use |
|---------|------------|
| Synchronous REST | Caller needs immediate response |
| Asynchronous Messaging | Producer does not wait for consumer |
| Event-Driven | Multiple consumers react to the same event |
| Batch/Scheduled | Processing large datasets periodically |
| Webhook | External system notifies our system |

### Dependency Rules

**Allowed:** Service --> API Gateway; service --> service via defined interface only; service --> shared libraries (logging, auth, validation); service --> infrastructure (DB, broker, cache).

**Forbidden:** No direct cross-boundary DB access. No circular dependencies. No business logic in API Gateway. No shared mutable state.

---

## 5. Architecture Viewpoints

All viewpoint diagrams must be PlantUML `.puml` files committed to the `diagrams/` directory.

| Viewpoint | Question It Answers | Audience | Diagram Type | Template |
|-----------|-------------------|----------|--------------|----------|
| System Context | What interacts with our system? | Product Owner, BA, all stakeholders | C4 Context / box diagram | [../diagrams/system-context-diagram.puml](../diagrams/system-context-diagram.puml) |
| Logical/Functional | What are the components and how do they relate? | Tech Lead, Developers | Component diagram | [../diagrams/component-diagram.puml](../diagrams/component-diagram.puml) |
| Process/Runtime | How does the system behave at runtime? | Tech Lead, Developers, QA | Sequence diagrams | [../diagrams/sequence-diagram.puml](../diagrams/sequence-diagram.puml) |
| Deployment | Where does the system run? | Infra Engineer, Ops Lead | Deployment diagram | [../diagrams/deployment-diagram.puml](../diagrams/deployment-diagram.puml) |
| Development | How is the codebase organized? | Developers, Tech Lead | Package/module diagram | Directory tree or module dependency |
| Entity-Relationship | What are the data entities? | Developers, DBA | ERD | [../diagrams/erd-diagram.puml](../diagrams/erd-diagram.puml) |
| State | What states do key entities go through? | Developers, QA | State diagram | [../diagrams/state-diagram.puml](../diagrams/state-diagram.puml) |

Every stakeholder concern must map to at least one viewpoint. Map "what it does" to Logical, "how data flows" to Process, "where it runs" to Deployment, "how code is organized" to Development, "security" to all views.

---

## 6. Architecture Patterns

### Selection Table

| Pattern | Best For | Pros | Cons |
|---------|----------|------|------|
| Modular Monolith | Small-to-medium teams; default choice | Simple deployment, modular internals, easy refactor | Requires discipline for boundaries; all-or-nothing releases |
| Layered | General-purpose web apps | Simple, enforces separation of concerns | Can be rigid; layer traversal overhead |
| Hexagonal (Ports & Adapters) | Services with 3+ external integrations | Highly testable, swappable dependencies | More abstractions; can feel over-engineered for CRUD |
| Event-Driven | Async workflows, IoT telemetry | Loose coupling, high throughput | Hard to debug, eventual consistency |
| Microservices | Large teams (10+), independent scaling | Team autonomy, fault isolation | Operational complexity, distributed debugging |
| CQRS | Read-heavy apps (10:1+ ratio) | Optimized read/write paths | Increased complexity, eventual consistency |
| Pipe and Filter | ETL, data pipelines | Stages are simple and testable | Not for interactive apps |

### Default Selection

- New project, no special constraints: **Modular Monolith + Layered + Client-Server**.
- IoT telemetry pipeline: **Event-Driven + Pipe and Filter**.
- Multiple external integrations: **Hexagonal (Ports and Adapters)**.
- Document the chosen pattern in an ADR.

---

## 7. Technology Evaluation Criteria

Use a weighted scoring matrix when selecting new technologies. Score each option 1-5 per criterion.

| Criterion | Weight | Assessment Method |
|-----------|--------|-------------------|
| Requirements Fit | Critical (5) | Map each ASR to technology capabilities |
| Team Expertise | High (4) | Survey team: Strong / Moderate / None |
| Maturity | High (4) | Version history, major users, years in production |
| Community & Support | High (4) | GitHub activity, docs, release frequency |
| Performance | Medium (3) | Benchmarks under expected load |
| Operational Complexity | Medium (3) | Deployment, monitoring, upgrade path |
| Security | Medium (3) | CVE history, update frequency |
| Licensing | Medium (3) | MIT/Apache = safe; GPL/AGPL = consult legal |
| Scalability | Medium (3) | Horizontal/vertical scaling options |
| Cost | Low-Medium (1) | License fees, infra, training |
| Learning Curve | Low (1) | Ramp-up time for an average developer |

**Weighted score** = Score x Weight. Sum all for final ranking. If top two options are within 20 points, run a proof-of-concept before deciding. If all options score below 100/170, revisit requirements.

---

## 8. Detailed Design Standard

The Detailed Design Document (DDD) specifies how each component is built internally. Use the template at [../templates/detailed-design-document.md](../templates/detailed-design-document.md).

### Required DDD Sections

| Section | Key Content |
|---------|-------------|
| Component Overview | Name, responsibility, architectural context |
| Public Interface | All methods/endpoints exposed |
| Internal Structure | Classes, modules, relationships. Deliver as [../diagrams/class-diagram.puml](../diagrams/class-diagram.puml) |
| Data Model | Tables, entities, relationships owned. Deliver as [../diagrams/data-flow-diagram.puml](../diagrams/data-flow-diagram.puml) |
| Business Logic | Algorithms, state machines, decision rules |
| Error Handling | Detection, reporting, recovery |
| Logging and Observability | Log levels, metrics |
| Security | Auth, authorization, input validation |
| Dependencies | External services, libraries, internal components |
| Design Decisions | Patterns used, rationale |

### Design Principles

| Principle | Rule |
|-----------|------|
| **S** - Single Responsibility | Each class/module has one reason to change |
| **O** - Open/Closed | Open for extension, closed for modification |
| **L** - Liskov Substitution | Subtypes substitutable for base types |
| **I** - Interface Segregation | Clients do not depend on unused methods |
| **D** - Dependency Inversion | Depend on abstractions, not concretions |
| DRY | Extract shared logic; prefer duplication over wrong abstraction |
| KISS | Simplest approach that satisfies the requirement |
| YAGNI | Do not design for hypothetical future requirements |
| Fail Fast | Validate inputs at boundary; throw immediately on invariant violation |

### Code Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Class/Interface | PascalCase | RentalService, LateFeeCalculator |
| Function/Method | camelCase | calculateLateFee, getRentalById |
| Variable | camelCase | rentalAgreement, daysOverdue |
| Constant | SCREAMING_SNAKE_CASE | MAX_RENTAL_DURATION_DAYS |
| File (module) | kebab-case | rental-service.ts |
| Test file | [module].test.ts or .spec.ts | rental-service.test.ts |

---

## 9. API Design Standard

### URL Structure

Pattern: `https://{host}/api/v{version}/{resource}`

| Element | Convention | Example |
|---------|-----------|---------|
| Base path | /api/v{N}/ | /api/v1/ |
| Resource | Plural noun, kebab-case | /api/v1/rental-agreements |
| Instance | /{resource}/{id} | /api/v1/rental-agreements/ra-001 |
| Sub-resource | /{resource}/{id}/{sub} | /api/v1/rental-agreements/ra-001/line-items |

### HTTP Methods and Status Codes

| Method | Purpose | Idempotent | Success Code |
|--------|---------|-----------|-------------|
| GET | Retrieve resource(s) | Yes | 200 |
| POST | Create new resource | No | 201 |
| PUT | Replace resource entirely | Yes | 200 |
| PATCH | Update specific fields | No | 200 |
| DELETE | Remove resource | Yes | 204 |

### Complete Status Code Reference

| Code | Name | When to Use |
|------|------|------------|
| 200 | OK | Successful GET, PUT, PATCH |
| 201 | Created | Successful POST creating a resource |
| 202 | Accepted | Request accepted for async processing |
| 204 | No Content | Successful DELETE, no response body |
| 400 | Bad Request | Malformed syntax, invalid parameters |
| 401 | Unauthorized | No token or token invalid/expired |
| 403 | Forbidden | Valid token, insufficient permissions |
| 404 | Not Found | Resource does not exist |
| 409 | Conflict | Action conflicts with current state |
| 422 | Unprocessable Entity | Valid syntax but violates business rules |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Unhandled server error (log full trace server-side) |
| 502 | Bad Gateway | Upstream service returned invalid response |
| 503 | Service Unavailable | System temporarily unable to handle requests |

**Rules:** Never return 200 for an error. Never return 500 for a client error. Always include error body for 4xx/5xx. Never expose stack traces to clients. Prefer 422 over 400 for business rule violations.

### Error Response Format

```json
{
  "error": {
    "code": "SCREAMING_SNAKE_CASE",
    "message": "Human-readable description",
    "details": [{"field": "...", "message": "..."}]
  }
}
```

Standard error codes: VALIDATION_ERROR, INVALID_PARAMETER, AUTHENTICATION_REQUIRED, PERMISSION_DENIED, RESOURCE_NOT_FOUND, CONFLICT, BUSINESS_RULE_VIOLATION, RATE_LIMIT_EXCEEDED, INTERNAL_ERROR.

### Request/Response Rules

- All JSON fields use **snake_case**.
- Dates use **ISO 8601** (date: `2026-03-01`, datetime: `2026-03-01T08:00:00Z` UTC, duration: `P14D`).
- All list endpoints support **pagination** (`page`, `per_page`; defaults: page=1, per_page=25, max 100).
- Pagination metadata in response: `page`, `per_page`, `total_items`, `total_pages`.
- Filtering via query parameters. Sorting via `sort` parameter (prefix `-` for descending).

### Authentication and Versioning

- All endpoints require JWT in `Authorization: Bearer {token}` header. Public endpoints (health, login) explicitly whitelisted.
- Version in URL path: `/api/v1/`, `/api/v2/`. Increment only for breaking changes.
- Previous version supported for **6 months** after new version release. Deprecated endpoints include `Deprecation` response header.

### Idempotency

- POST endpoints for financial operations require `Idempotency-Key` header.
- PATCH endpoints for critical operations: Idempotency-Key recommended.

---

## 10. Database Design Standard

### Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Table | Plural, snake_case | rental_agreements |
| Column | snake_case | customer_name |
| Primary key | id | id (UUID or BIGINT) |
| Foreign key | {referenced_table_singular}_id | customer_id |
| Index | idx_{table}_{column(s)} | idx_rental_agreements_customer_id |
| Unique constraint | uq_{table}_{column(s)} | uq_customers_email |
| Check constraint | chk_{table}_{description} | chk_rental_agreements_end_after_start |
| FK constraint | fk_{table}_{referenced_table} | fk_rental_agreements_customers |

### Required Columns (Every Table)

| Column | Type | Default |
|--------|------|---------|
| id | UUID (default) or BIGINT | gen_random_uuid() |
| created_at | TIMESTAMP WITH TIME ZONE | NOW() |
| updated_at | TIMESTAMP WITH TIME ZONE | NOW() (updated by trigger) |

### Data Type Rules

| Use Case | Data Type |
|----------|-----------|
| Monetary amounts | DECIMAL(12,2) -- never FLOAT/DOUBLE |
| Percentages | DECIMAL(5,4) |
| Short text (known max) | VARCHAR(N) |
| Long text | TEXT |
| Boolean | BOOLEAN |
| Date only | DATE |
| Date and time | TIMESTAMP WITH TIME ZONE |
| Enumerated values | VARCHAR with CHECK constraint |
| JSON metadata | JSONB |
| Binary/files | Store file in object storage, store URL in DB |

### Soft Delete

Tables with business data (rental_agreements, customers, invoices, equipment_items) use `deleted_at TIMESTAMPTZ` (NULL = active). All queries on soft-delete tables must filter `WHERE deleted_at IS NULL` unless explicitly querying deleted records.

### Indexing, Normalization, Migrations

- **Indexes:** Add for columns in WHERE, JOIN, ORDER BY. Composite index: most selective column first. No unnecessary indexes on small tables (<1,000 rows).
- **Normalization:** Baseline is 3NF. Denormalization allowed for reporting (materialized views), snapshot data, performance-critical reads -- document rationale.
- **Migrations:** Sequential numbering (`001_create_rental_agreements.sql`). Every migration has UP and DOWN scripts. Destructive changes require multi-step migration. Data migrations separate from schema migrations. Test UP/DOWN on test database before production.
- **Audit trail:** Financial/compliance tables (invoices, payments, rental_agreements) require audit log triggers recording table_name, record_id, action, old_values, new_values, changed_by, changed_at.

---

## 11. UI Design Standard

### Responsive Breakpoints

| Breakpoint | Min Width | Target |
|-----------|-----------|--------|
| Mobile | 320px | Smartphones |
| Tablet | 768px | Tablets, small laptops |
| Desktop | 1024px | Standard laptops |
| Large Desktop | 1440px | Large monitors |

Mobile-first design: start with mobile layout, expand for larger screens.

### Accessibility (WCAG 2.1 AA)

- Color contrast: 4.5:1 normal text, 3:1 large text.
- All interactive elements reachable via Tab; focus order matches visual order.
- All images have alt text; form fields have labels; ARIA roles for custom components.
- Visible focus ring on all focusable elements.
- Errors identified by text, not color alone.
- Content usable at 200% zoom.

### Form Design Rules

- Visible label above every field (no placeholder-as-label). Required fields marked with asterisk.
- Validate on blur; show inline error below field with specific message.
- Submit button disabled until all required fields valid; loading state during submission.

### Component States

Every UI component must handle: **Loading** (skeleton/spinner, never blank), **Empty** (helpful message + action), **Error** (message + retry), **Success** (toast, auto-dismiss 5s), **Partial** (show available data, error for failed sections).

### Navigation

- Sidebar (desktop) or hamburger menu (mobile); max 8 top-level items.
- Breadcrumbs for pages 2+ levels deep. Current page highlighted. Unique page titles. Back button works.

### RTL/LTR

Use CSS logical properties (margin-inline-start, not margin-left). Text alignment: start/end, not left/right. Language switcher on every page.

---

## 12. Design Patterns Quick Reference

### Selection Table

| Pattern | Category | When to Use | Avoid When |
|---------|----------|-------------|------------|
| Factory | Creational | Multiple implementations chosen at runtime | Only one implementation exists |
| Builder | Creational | Object with 5+ parameters, many optional | Simple object with 2-3 required fields |
| Singleton | Creational | DB connection pool, config manager | General-purpose -- use sparingly |
| Repository | Structural | Any database access (always use) | One-off scripts/migrations |
| Adapter | Structural | Integrating third-party APIs/SDKs | Internal code you control |
| Facade | Structural | Complex subsystem needs simplified API | Already-simple subsystems |
| Decorator | Structural | Adding logging, caching, validation wrappers | N/A |
| Strategy | Behavioral | Multiple algorithms selectable at runtime | Only one algorithm exists |
| Observer/Events | Behavioral | Multiple consumers react to same event | Only one consumer (use direct call) |
| State Machine | Behavioral | Entity transitions through defined states | Simple boolean flags |
| Command | Behavioral | Job queues, undo/redo, audit logging | Simple synchronous operations |
| Middleware/Pipeline | Behavioral | HTTP request processing chain | N/A |

### Anti-Patterns to Avoid

**God Object** (2000+ lines, 50+ methods -- split by responsibility), **Anemic Domain Model** (entities with only getters/setters -- move logic into entity methods), **Spaghetti Code** (no clear call structure -- refactor into layers), **Golden Hammer** (one pattern everywhere -- choose right tool per problem), **Premature Abstraction** (interface before second implementation -- abstract after third instance).

---

## 13. Diagramming Rules

### PlantUML Conventions

All architecture and design diagrams are delivered as PlantUML `.puml` files. No Visio, no draw.io, no screenshots of whiteboards.

### Required Diagram Files

| Diagram | File Path | Produces |
|---------|-----------|----------|
| System Context | `diagrams/system-context-diagram.puml` | System boundary, external systems, user types, data flows |
| Component | `diagrams/component-diagram.puml` | All components, responsibilities, interfaces |
| Sequence (per scenario) | `diagrams/sequence-{scenario}.puml` | Top 3 workflows, async flows, error flows |
| Deployment | `diagrams/deployment-diagram.puml` | Production topology, servers, network, LBs, DBs |
| ERD | `diagrams/erd-diagram.puml` | All data entities, attributes, relationships |
| State (per entity) | `diagrams/state-{entity}.puml` | Lifecycle states for key domain entities |
| Class | `diagrams/class-diagram.puml` | Component internal structure |
| Data Flow | `diagrams/data-flow-diagram.puml` | Data transformation and flow paths |
| API Flow | `diagrams/api-flow-diagram.puml` | API request/response sequence flows |

### Diagram Quality Rules

- Every line/arrow labeled with protocol and data flow direction.
- System Context shows system as a single black box -- no internal components.
- Logical View assigns data ownership to exactly one component per entity.
- No circular dependencies between components.
- No component directly accesses another component's database.

### Naming Conventions Summary

| Element | Convention | Example |
|---------|-----------|---------|
| Service/Component | kebab-case | rental-service |
| API endpoint | /api/v{N}/{resource} | /api/v1/rental-agreements |
| Database name | snake_case | rental_service_db |
| Table name | plural snake_case | rental_agreements |
| Queue/Topic | dot-separated | rental.agreement.overdue |
| Environment variable | SCREAMING_SNAKE_CASE | DATABASE_URL |
| Config file | kebab-case | app-config.yaml |
| PlantUML file | kebab-case | system-context-diagram.puml |

---

## Cross-References

| Document | Type | Link |
|----------|------|------|
| Architecture Description Document | Template | [../templates/architecture-description-document.md](../templates/architecture-description-document.md) |
| Architecture Decision Record | Template | [../templates/architecture-decision-record.md](../templates/architecture-decision-record.md) |
| Component Diagram | Template | [../diagrams/component-diagram.puml](../diagrams/component-diagram.puml) |
| Detailed Design Document | Template | [../templates/detailed-design-document.md](../templates/detailed-design-document.md) |
| API Specification | Template | [../templates/api-specification.md](../templates/api-specification.md) |
| Data Model Document | Template | [../templates/data-model-document.md](../templates/data-model-document.md) |
| Design Review Checklist | Template | [../runbooks/conduct-reviews.md](../runbooks/conduct-reviews.md) |
| System Context Diagram | Diagram | [../diagrams/system-context-diagram.puml](../diagrams/system-context-diagram.puml) |
| Component Diagram | Diagram | [../diagrams/component-diagram.puml](../diagrams/component-diagram.puml) |
| Sequence Diagram | Diagram | [../diagrams/sequence-diagram.puml](../diagrams/sequence-diagram.puml) |
| Deployment Diagram | Diagram | [../diagrams/deployment-diagram.puml](../diagrams/deployment-diagram.puml) |
| ERD Diagram | Diagram | [../diagrams/erd-diagram.puml](../diagrams/erd-diagram.puml) |
| State Diagram | Diagram | [../diagrams/state-diagram.puml](../diagrams/state-diagram.puml) |
| Class Diagram | Diagram | [../diagrams/class-diagram.puml](../diagrams/class-diagram.puml) |
| Data Flow Diagram | Diagram | [../diagrams/data-flow-diagram.puml](../diagrams/data-flow-diagram.puml) |
| Architect & Design | Runbook | [../runbooks/architect-and-design.md](../runbooks/architect-and-design.md) |
| Conduct Reviews | Runbook | [../runbooks/conduct-reviews.md](../runbooks/conduct-reviews.md) |
