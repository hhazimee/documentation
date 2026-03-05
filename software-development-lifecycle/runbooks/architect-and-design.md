# Architect and Design

This runbook guides the team through the complete architecture and design workflow, from creating the Architecture Description Document through detailed component design, API contracts, and data models. It merges five individual runbooks into a single end-to-end procedure so that practitioners can follow one sequential path from Phase 3 (System Architecture) into Phase 4 (Design).

---

## Prerequisites

Before starting, confirm every item below is satisfied:

- [ ] BRD and SRS baselined (Phase 2 complete)
- [ ] Requirements Traceability Matrix (RTM) populated
- [ ] System Architect and Tech Lead assigned
- [ ] Access to stakeholder register and communication plan granted
- [ ] Detailed Design Standard, API Design Standard, and Database Design Standard reviewed
- [ ] Templates obtained:
  - Architecture Description Document -- [ADD Template](../templates/architecture-description-document.md)
  - Architecture Decision Record -- [ADR Template](../templates/architecture-decision-record.md)
  - Detailed Design Document -- [DDD Template](../templates/detailed-design-document.md)
  - API Specification -- [API Specification Template](../templates/api-specification.md)
  - Data Model Document -- [Data Model Document Template](../templates/data-model-document.md)

---

## Step 1: Create Architecture Description

**Owner:** Tech Lead | **SLA:** 10 business days

### 1.1 Review Baselined Requirements

- [ ] Read BRD and list all business objectives
- [ ] Read SRS and categorize all software requirements (functional, non-functional, interface, data)
- [ ] Review RTM and confirm every BR traces to at least one SWR
- [ ] Identify all external system interfaces
- [ ] Identify all user types and roles

### 1.2 Identify Architecture-Significant Requirements (ASRs)

Filter requirements against these ASR categories:

| ASR Category | Identification Criteria |
|-------------|------------------------|
| High-impact functional | Features defining core system behavior |
| Quality attribute | Non-functional requirements with measurable targets |
| System interface | Integrations with external systems |
| Constraint | Technology, regulatory, or infrastructure constraints |
| High-risk | Features with significant technical uncertainty |

- [ ] 15-30 ASRs identified and marked in RTM

> **IF** fewer than 15 ASRs **THEN** re-examine quality attribute and interface requirements.
> **IF** more than 30 ASRs **THEN** re-evaluate for over-classification.

### 1.3 Map Stakeholder Concerns to Viewpoints

| Stakeholder | Concern | Viewpoint |
|------------|---------|-----------|
| Product Owner | Business requirements coverage | System Context, Logical |
| Operations Staff | Daily usage workflows | System Context |
| Tech Lead | Build and maintain feasibility | Logical, Development |
| Infrastructure Engineer | Deployment, scaling | Deployment |
| QA Lead | Independent component testability | Logical, Development |
| Security Officer | Data protection | All viewpoints |

- [ ] All stakeholders mapped to concerns and viewpoints

### 1.4 Create System Context Diagram

**Template:** [system-context-diagram.puml](../diagrams/system-context-diagram.puml)

1. Copy the template to your project `diagrams/` directory.
2. Draw the system as a single box in the center.
3. Add every external entity (users, external systems, data sources) around it.
4. Label each line with protocol (REST, MQTT, SMTP), data direction, and data description.
5. Validate against SRS external interfaces -- every interface must appear.
6. Commit the `.puml` file.

- [ ] System context diagram committed to `diagrams/`

### 1.5 Create Logical/Functional View

**Template:** [component-diagram.puml](../diagrams/component-diagram.puml)

1. Group related ASRs by business capability.
2. Identify components; give each a kebab-case name, one-sentence responsibility, owned data, exposed interface, and dependencies.
3. Draw the component diagram and label each relationship with its integration pattern (sync REST, async event, etc.).
4. Validate that every functional requirement maps to at least one component.
5. Commit the `.puml` file.

- [ ] Component diagram committed to `diagrams/`

### 1.6 Create Process/Runtime View

**Template:** [sequence-diagram.puml](../diagrams/sequence-diagram.puml)

1. Identify the top 5 critical runtime scenarios.
2. Create a PlantUML sequence diagram for each (e.g., `sequence-create-order.puml`).
3. Document all scheduled jobs with trigger time, frequency, components, and data processed.
4. Commit all `sequence-*.puml` files.

- [ ] Sequence diagrams committed for each critical scenario

### 1.7 Create Deployment View

**Template:** [deployment-diagram.puml](../diagrams/deployment-diagram.puml)

1. List all infrastructure components (servers, databases, brokers, caches, load balancers).
2. Define network topology (public vs. internal segments, firewall rules).
3. Map each software component to its deployment target.
4. Document server specs, DB config, SSL/TLS termination, and backup infrastructure.
5. Commit the `.puml` file.

- [ ] Deployment diagram committed to `diagrams/`

> **IF** staging differs from production **THEN** document both environments.

### 1.8 Create Development View

1. Define repository structure (monorepo vs. multi-repo).
2. Document top-level directory organization.
3. Map package/module boundaries to logical components.
4. Document build pipeline stages (lint, test, build, deploy).
5. Define shared library and dependency management strategies.

- [ ] Development view documented

### 1.9 Document Technology Stack

1. Create a technology table with columns: Technology, Version, Purpose, Rationale.
2. Identify which choices require a formal ADR (see Step 2).

- [ ] Technology stack documented

### 1.10 Conduct Architecture Review and Obtain Approval

1. Execute the architecture review per the [Conduct Architecture Review](./conduct-reviews.md) runbook.
2. Present the final ADD to the approval authority and walk through each viewpoint.
3. Obtain written sign-off from System Architect, Tech Lead, and Product Owner.
4. Record the approved ADD version as the baseline.
5. Update the RTM with architecture references.

- [ ] Architecture review completed with no open blockers
- [ ] Written sign-off obtained
- [ ] RTM updated with architecture references

---

## Step 2: Write Architecture Decision Records

**Owner:** Tech Lead | **SLA:** 3 business days per ADR

For each significant technology or pattern choice, produce a formal ADR.

### 2.1 Confirm an ADR Is Required

An ADR is required when the decision involves:

- Selecting a technology (database, framework, library, cloud service)
- Choosing an architecture pattern (monolith, microservices, event-driven)
- Choosing an integration approach (REST, messaging, shared DB)
- Making a significant trade-off (consistency vs. availability)
- Deviating from an established standard

> **IF** none of these apply **THEN** document the decision informally in the ADD.

### 2.2 Assign ADR Number and Create File

1. Check existing ADRs in `architecture/decisions/`.
2. Take the next sequential number.
3. Create `architecture/decisions/NNN-short-description.md` using the [ADR Template](../templates/architecture-decision-record.md).

### 2.3 Write the ADR

1. **Context** -- State the problem, reference BR/SWR IDs, list constraints, explain the trigger.
2. **Alternatives** -- Document at least 2-3 options with name/version, strengths, weaknesses, team experience, licensing, and community support.
3. **Trade-off evaluation** -- Build a comparison matrix with weighted criteria (requirements fit, team expertise, performance, operational complexity, licensing cost, community support).
4. **Decision** -- Write a clear statement: "We will use [X] for [purpose]."
5. **Consequences** -- List positives, negatives (trade-offs accepted), and risks with mitigations.

> **IF** two options score equally **THEN** use team expertise and operational complexity as tiebreakers.

### 2.4 Review and Approve

1. Set status to Proposed.
2. Request peer review from at least one architect or senior developer.
3. Address feedback; change status to Accepted upon approval.
4. Reference the ADR in the ADD and announce the decision to the team.

- [ ] ADR peer-reviewed and accepted
- [ ] ADR referenced in ADD

**Minimum ADRs required:**

- [ ] Architecture style (monolith / microservices / modular monolith)
- [ ] Primary programming language and framework
- [ ] Database technology
- [ ] Message broker (if applicable)
- [ ] Authentication mechanism
- [ ] Hosting / infrastructure platform

---

## Step 3: Create Detailed Design

**Owner:** Developer | **Accountable:** Tech Lead | **SLA:** 5 business days per component

### 3.1 Review Architecture Context

1. Read the ADD section for the assigned component.
2. Note the component's responsibility, owned data, and interfaces.
3. Read all ADRs that affect this component.
4. List all SWR IDs assigned to this component.

- [ ] Component context fully understood and documented

### 3.2 Define Public Interface

1. Document every method, endpoint, or event the component exposes.
2. Define request/response schemas per the API Design Standard.

- [ ] All REST endpoints, published events, and service methods listed

### 3.3 Design Internal Structure

1. Break the component into internal modules.
2. Define each module's responsibility (one sentence), public methods, and dependencies.
3. Identify test file locations.

- [ ] Module structure defined with single responsibility per module
- [ ] No circular dependencies

### 3.4 Design Business Logic

1. State each business rule with its SWR ID reference.
2. Define the algorithm or decision logic for each rule.
3. Identify edge cases, boundary conditions, and error conditions.

- [ ] Business rules linked to requirements
- [ ] Edge cases and error conditions handled

### 3.5 Design Error Handling

1. List every error scenario for this component.
2. Define detection method, HTTP status, error code, and recovery strategy for each.

- [ ] Client errors vs. server errors distinguished
- [ ] Recovery strategies defined (retry, queue, none)

### 3.6 Design Logging, Monitoring, and Security

1. Define log points with level and data for: request received, operation completed, external calls, errors, performance warnings.
2. Verify no sensitive data is logged (passwords, tokens, PII).
3. Define input validation, authorization checks, parameterized queries, and DTO-based data exposure controls.

- [ ] Logging and monitoring points defined
- [ ] Security considerations addressed

### 3.7 Create Sequence Diagrams and Document Patterns

1. Create a sequence diagram for each interaction involving 3+ components.
2. List every design pattern used with its location and justification.

- [ ] Sequence diagrams committed for complex interactions
- [ ] Design patterns documented

### 3.8 Submit for Design Review

Follow the [Conduct Design Review](./conduct-reviews.md) runbook.

- [ ] DDD completed using the [DDD Template](../templates/detailed-design-document.md)
- [ ] Design review initiated

---

## Step 4: Design API Contracts

**Owner:** Developer | **Accountable:** Tech Lead | **SLA:** 3 business days per API resource

### 4.1 Identify Resources

1. Map each SRS requirement to a REST resource.
2. Define resource name, URL pattern, and description following the API Design Standard.

- [ ] Every requirement mapped to at least one resource

### 4.2 Define Endpoints

1. List all CRUD endpoints per resource (GET list, GET single, POST, PUT, PATCH, DELETE).
2. List action endpoints for non-CRUD operations (e.g., POST `/orders/{id}/cancel`).
3. Assign required roles per endpoint.

- [ ] HTTP methods follow API Design Standard

### 4.3 Design Request/Response Schemas

1. Define request body schema for every POST/PUT/PATCH endpoint.
2. Define response body schema for every endpoint.
3. Specify field types (string, number, UUID, ISO 8601 date), required/optional, and constraints (max length, regex).

- [ ] Schemas include standard fields: id, created_at, updated_at

### 4.4 Define Error Responses

Map every error condition to an HTTP status code and error code:

| Status | Code | When |
|--------|------|------|
| 400 | VALIDATION_ERROR | Invalid input |
| 401 | AUTHENTICATION_REQUIRED | Unauthenticated access |
| 403 | PERMISSION_DENIED | Unauthorized role |
| 404 | RESOURCE_NOT_FOUND | Missing entity |
| 409 | CONFLICT | State conflict |
| 422 | BUSINESS_RULE_VIOLATION | Business rule failure |

- [ ] Error responses follow API Design Standard format

### 4.5 Document Query Parameters and Authentication

1. Define pagination (page, per_page with defaults and max), filter, sort, and date-range parameters for list endpoints.
2. Specify authentication requirement (Yes/No) and allowed roles per endpoint.
3. Document special headers (Idempotency-Key, etc.) where required.

- [ ] Query parameters documented for all list endpoints
- [ ] Auth requirements documented per endpoint

### 4.6 Write OpenAPI Specification

1. Produce an OpenAPI 3.0 spec in YAML or JSON using the [API Specification Template](../templates/api-specification.md).
2. Validate the spec against the API Design Standard.

- [ ] OpenAPI 3.0 spec produced and validates without errors

### 4.7 Peer Review and Mock

1. Share the spec with the frontend/consumer team for review.
2. Confirm all SRS requirements are covered and incorporate feedback.
3. Set up a mock server returning example responses per endpoint.

- [ ] API spec reviewed by consumer
- [ ] Mock server running and accessible to frontend team

---

## Step 5: Design Data Models

**Owner:** Developer | **Accountable:** Tech Lead | **SLA:** 3 business days per data domain

### 5.1 Identify Entities

1. Extract entities from SRS requirements and design documents.
2. Map each entity to its source SWR ID and document descriptions.

- [ ] All entities identified and traced to requirements

### 5.2 Define Attributes

1. List all attributes per entity with column name, type, nullable flag, default, and constraints.
2. Follow snake_case naming per the Database Design Standard.
3. Include standard columns: `id` (UUID PK), `created_at` (TIMESTAMPTZ), `updated_at` (TIMESTAMPTZ), `deleted_at` (TIMESTAMPTZ, nullable) where soft-delete applies.

- [ ] All attributes fully defined

### 5.3 Define Relationships

1. Define relationship type (1:1, 1:N, M:N) between entities.
2. Specify foreign key columns and ON DELETE behavior (RESTRICT, CASCADE, SET NULL).

- [ ] All relationships documented
- [ ] Junction tables created for M:N relationships

> **IF** relationship crosses component boundaries **THEN** use ID reference only (no FK constraint) and document in design.

### 5.4 Normalize to 3NF

1. Verify 1NF (no repeating groups), 2NF (no partial dependencies), 3NF (no transitive dependencies).
2. Document any intentional denormalization with business rationale.

- [ ] Schema normalized to 3NF
- [ ] Denormalizations documented with rationale

### 5.5 Define Indexes and Constraints

1. Define indexes for every FK column, filtered/sorted column, and multi-column query pattern.
2. Define unique indexes for business uniqueness constraints.
3. Define CHECK, UNIQUE, FK, and NOT NULL constraints.

- [ ] Indexes cover all query patterns
- [ ] Constraints enforce data integrity rules

### 5.6 Design Migration and Seed Data Scripts

1. Create versioned migration files with UP (apply) and DOWN (rollback) sections.
2. Tables must be created in dependency order (referenced tables first).
3. Define seed data covering status variations and edge cases for dev/test.

- [ ] Migration scripts structured with UP/DOWN
- [ ] Seed data maintains referential integrity

### 5.7 Submit for Review

1. Submit the data model to the Tech Lead.
2. Verify all SRS data requirements are covered, naming follows the Database Design Standard, and indexes support identified query patterns.

- [ ] Data model approved by Tech Lead

---

## Outputs Checklist

| # | Artifact | Template | Storage |
|---|----------|----------|---------|
| 1 | Architecture Description Document | [ADD Template](../templates/architecture-description-document.md) | `architecture/` |
| 2 | Architecture Decision Records | [ADR Template](../templates/architecture-decision-record.md) | `architecture/decisions/` |
| 3 | System Context Diagram (.puml) | [system-context-diagram.puml](../diagrams/system-context-diagram.puml) | `diagrams/` |
| 4 | Component Diagram (.puml) | [component-diagram.puml](../diagrams/component-diagram.puml) | `diagrams/` |
| 5 | Deployment Diagram (.puml) | [deployment-diagram.puml](../diagrams/deployment-diagram.puml) | `diagrams/` |
| 6 | Sequence Diagrams (.puml) | [sequence-diagram.puml](../diagrams/sequence-diagram.puml) | `diagrams/` |
| 7 | Detailed Design Documents | [DDD Template](../templates/detailed-design-document.md) | `/docs/design/` |
| 8 | API Specification + OpenAPI 3.0 | [API Specification Template](../templates/api-specification.md) | `/docs/design/api/` |
| 9 | Data Model Document | [Data Model Document Template](../templates/data-model-document.md) | `/docs/design/data/` |
| 10 | Migration Scripts | -- | `/migrations/` |
| 11 | Seed Data Scripts | -- | `/seeds/` |
| 12 | Updated RTM | -- | `/docs/traceability/` |

---

## Tips

- **Work sequentially.** Architecture (Steps 1-2) must be approved before detailed design (Steps 3-5) begins. Designing components against an unapproved architecture causes rework.
- **Keep ADRs short.** A good ADR is one to two pages. If it grows longer, the decision scope is probably too broad -- split it.
- **Validate traceability continuously.** After each step, verify that every SRS requirement traces forward to at least one architecture component, design element, API endpoint, or data entity.
- **Use PlantUML consistently.** Store all `.puml` files in the project `diagrams/` directory and commit them to version control so diagrams stay in sync with the codebase.
- **Design APIs from the consumer's perspective.** Share contracts with frontend or integration teams early. A mock server unblocks parallel development.
- **Normalize first, denormalize with evidence.** Start at 3NF and only denormalize when you have a documented performance justification.
- **Automate schema validation.** Run OpenAPI spec validation and migration script dry-runs in CI to catch contract and schema drift early.
- **Escalate, do not guess.** Every abort condition in the source runbooks exists because proceeding without clarity creates compounding errors. When in doubt, stop and escalate.
