# Glossary

| Field | Value |
|-------|-------|
| **Reference ID** | REF-GL-001 |
| **Use When** | Looking up SDLC terminology used across all phases |
| **Last Updated** | 2026-03-05 |

---

## Terms

| Term | Definition |
|------|-----------|
| Acceptance Criteria | Specific, measurable conditions that a requirement must satisfy to be accepted. Often written in Given/When/Then format. |
| ADD (Architecture Description Document) | Complete architecture documentation covering all viewpoints (context, logical, deployment, process, development) per ISO 42010. |
| ADR (Architecture Decision Record) | A document capturing a single architecture decision with context, alternatives considered, decision, and rationale. |
| ASR (Architecturally Significant Requirement) | A requirement that has a measurable impact on the system's architecture, typically driving key design decisions. |
| Baseline | An approved, version-controlled snapshot of artifacts at a point in time. Changes require formal change control. |
| BRD (Business Requirements Document) | A document that captures business requirements, objectives, scope, and stakeholder needs. |
| Business Requirement | A high-level statement of what the business needs to achieve. Prefixed BR-XXX. |
| CCB (Change Control Board) | A group authorized to approve or reject changes to baselined artifacts. |
| Change Request | A formal proposal to modify a baselined artifact. Assigned ID CR-XXX and processed through impact analysis and CCB review. |
| Changelog | A summary of all changes included in a release, generated from conventional commits. |
| CI/CD (Continuous Integration / Continuous Delivery) | The practice of automatically building, testing, and preparing code changes for release through an automated pipeline. |
| Code Review | A systematic examination of source code by a peer to find defects, ensure standards compliance, and share knowledge. |
| Conventional Commit | A commit message following the format `type(scope): description` to enable automated changelog generation. |
| DDD (Detailed Design Document) | A document describing the internal structure, business logic, error handling, and interfaces of a single component. |
| Decomposition | The process of breaking higher-level requirements into more detailed lower-level requirements (BR to STK to SYS to SWR). |
| Defect | A flaw in a work product that causes it to fail to meet its requirements. Classified by severity (Critical, High, Medium, Low). |
| Deployment Diagram | A diagram showing infrastructure topology, server specifications, and network layout for the system. |
| Elicitation | The process of discovering requirements from stakeholders through interviews, workshops, observation, and other techniques. |
| Feasibility | Whether a requirement can be implemented within known technical and schedule constraints. |
| Feature Branch | A Git branch created for developing a single feature, following the naming convention `feature/TICKET-NNN-description`. |
| Functional Requirement | A requirement that specifies what the system must do (behavior, features, operations). |
| Integration Test | A test that verifies the interaction between two or more components or services. |
| MoSCoW | A prioritization method: Must Have, Should Have, Could Have, Won't Have. |
| NFR (Non-Functional Requirement) | A requirement that specifies how the system must perform (quality attributes: performance, security, usability, reliability, scalability, maintainability, compliance). |
| PR (Pull Request) | A request to merge a feature branch into a target branch, including description, test plan, and linked ticket for code review. |
| RACI | A responsibility assignment matrix: Responsible, Accountable, Consulted, Informed. |
| Regression Test | A test that verifies previously working functionality still works after new changes are introduced. |
| Release Branch | A Git branch `release/X.Y.Z` used to stabilize code before a production release. |
| RTM (Requirements Traceability Matrix) | A document that maps requirements from business origin through design, implementation, and testing. |
| Scope Creep | Uncontrolled expansion of project scope through unapproved requirement additions. |
| Sequence Diagram | A diagram showing runtime interaction between components for a specific scenario, ordered by time. |
| SLA (Service Level Agreement) | A defined target for response or resolution time, used in defect management to set fix deadlines by severity. |
| Software Requirement | A specific statement of software behavior, constraints, or interfaces. Prefixed SWR-XXX. |
| SRS (Software Requirements Specification) | A document containing all software requirements with attributes, acceptance criteria, and traceability. |
| Stakeholder | Any person or group with an interest in or influence over the system. |
| Stakeholder Requirement | A requirement from the perspective of a specific stakeholder group. Prefixed STK-XXX. |
| System Context Diagram | A diagram showing the boundary of the system and all external actors and systems it interacts with. |
| System Requirement | A requirement that specifies what the system must do to satisfy stakeholder needs. Prefixed SYS-XXX. |
| TDD (Test-Driven Development) | A development practice where unit tests are written before implementation code. |
| Technical Debt | A deliberate or inadvertent shortcut in implementation that will require future rework. Tracked in a Technical Debt Register. |
| Test Case | A set of preconditions, inputs, steps, and expected results designed to verify a specific requirement or behavior. |
| Test Plan | A document defining the scope, approach, resources, and schedule for testing activities. |
| Traceability | The ability to trace a requirement from its origin through specification, design, implementation, and verification. |
| UAT (User Acceptance Testing) | Testing performed by end users or business stakeholders to confirm the system meets business needs before release. |
| Unit Test | A test that verifies the behavior of a single function or method in isolation from external dependencies. |
| Use Case | A description of how an actor interacts with the system to achieve a goal, including main flow, alternate flows, and exception flows. |
| User Story | An informal requirement format: "As a [role], I want [capability], so that [business value]." Used in Agile execution. |
| Validation | Confirmation that the system meets stakeholder needs and intended use (building the right product). |
| Verification | Confirmation that a work product meets its specified requirements (building the product right). |
| Viewpoint (Architecture) | A perspective from which an architecture is described (e.g., logical, deployment, process, development). Defined by ISO 42010. |

---

## Requirement Type Prefixes

| Prefix | Type | Example |
|--------|------|---------|
| BR-XXX | Business Requirement | BR-001: Reduce equipment idle time by 20% |
| STK-XXX | Stakeholder Requirement | STK-001: Warehouse staff can scan returns via barcode |
| SYS-XXX | System Requirement | SYS-001: System shall record return timestamp on scan |
| SWR-XXX | Software Requirement | SWR-001: POST /returns endpoint accepts barcode and records timestamp |
| CR-XXX | Change Request | CR-001: Add late-fee waiver for premium customers |

---

## Decision Tree -- What Type of Requirement Is This?

```
IF requirement describes a business objective or need
    THEN type = Business Requirement (BR-XXX)

ELSE IF requirement describes what a stakeholder group needs
    THEN type = Stakeholder Requirement (STK-XXX)

ELSE IF requirement describes what the system must do at system level
    THEN type = System Requirement (SYS-XXX)

ELSE IF requirement describes specific software behavior or constraints
    THEN type = Software Requirement (SWR-XXX)
    IF it specifies behavior, features, or operations
        THEN subtype = Functional Requirement
    ELSE IF it specifies quality attributes (performance, security, etc.)
        THEN subtype = Non-Functional Requirement
```

---

## Decision Tree -- Verification vs. Validation

```
IF checking that a work product conforms to its specification
    THEN activity = Verification ("building the product right")

ELSE IF checking that the system meets stakeholder needs and intended use
    THEN activity = Validation ("building the right product")
```

---

## Cross-References

| Document | Type | Link |
|----------|------|------|
| Artifacts Checklist | Reference | [artifacts-checklist.md](./artifacts-checklist.md) |
| Defect Severity Reference | Reference | [defect-severity.md](./defect-severity.md) |
