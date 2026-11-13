# 04 — Architecture documentation standards and HLD/LLD discipline

## Standards and frameworks are not identical

- **ISO/IEC/IEEE 42010:2022**: architecture description discipline (stakeholders, concerns, viewpoints, views, rationale). Does **not** prescribe separate HLD and LLD Word files.
- **arc42**: practical template for a Software Architecture Document (SAD): introduction/goals, constraints, scope/context, strategy, building blocks, runtime, deployment, concepts, decisions, quality, risks, glossary.
- **C4**: System Context → Container → Component → Code zoom levels; create only the views needed to communicate the change.
- **ADRs (MADR-style)**: problem/context, decision drivers, considered options, decision, consequences, status/date and links.
- **ISO/IEC 25010:2023**: software product quality model; use measurable quality scenarios, not vague 'scalable' or 'secure'.
- **ISO/IEC/IEEE 29148:2018**: requirements engineering guidance.
- **ISO/IEC/IEEE 29119-3:2021**: test documentation guidance.
- **ISO/IEC/IEEE 12207:2026**: software lifecycle process framework, **not a fixed waterfall artifact checklist**.

Check your employer's mandatory standards before adopting this proposal; referenced standards may require purchase to read in full.

## HLD/SAD: what and why

HLD defines boundaries, interacting systems, key technology/deployment choices, communication patterns, trust zones, data ownership, availability/reliability assumptions, and major quality attributes. A baseline SAD is maintained throughout the system's life; changes update impacted views and important decisions rather than regenerating the entire document.

**Suggested SAD outline (arc42-aligned):**

1. Context, scope and business goals (including stakeholder concerns).
2. Constraints (technology, regulations, hosting, integration, SLAs).
3. System context and container diagrams (C4).
4. Design strategy and principles.
5. Building blocks and responsibilities.
6. Runtime sequences and important business journeys.
7. Deployment topology, failure domains and trust boundaries.
8. Cross-cutting concepts: identity, audit, resilience, observability, data ownership.
9. ADRs and tradeoffs.
10. Quality scenarios and acceptance measures.
11. Risks, technical debt and open decisions.
12. Glossary, versions, source references and ownership.

## LLD: how it works

LLD defines how a scoped behavior is implemented: components/classes and responsibilities; API/event schemas; business predicates and boundary conditions; state machines/process definitions; transactions, retries and idempotency; data migration and consistency; validation, security checks, errors, monitoring and test strategy. Do not prescribe internal class names unnecessarily when an approved API/behavioral contract suffices.

## Example CLM approval-change design

**Ticket:** Contracts above a threshold require an extra approval step. Note: whether equality triggers the rule, currency conversion, revisions and delegated authority must come from approved business rules, not AI inference.

- **HLD delta:** Flowable orchestration and policy decision boundary; integration to contract API and notification path; key failure/rollback considerations.
- **LLD delta:** eligibility predicate, process-state transitions, OPA input schema, exact threshold/currency behavior, transaction boundaries, duplicate event handling, error behavior and database assertions.
- **ADR only if needed:** changed decision about where the approval policy belongs, not merely because a new ticket exists.
- **Other artifacts:** OpenAPI/event contract changes, data model migration, threat model if authorization boundaries change, test specification and operations evidence.

## Document quality gates

An architecture artifact must identify **source requirements, versions, author/owner, reviewers, assumptions, rejected options, open questions, impacted components, measurable quality criteria and related evidence**. Any generated figure needs its underlying definition and assumptions reviewed. HLD/LLD should not contradict approved ADRs or contracts.

## What NOT to do

- Do not create an HLD and LLD for every one-line change.
- Do not duplicate full API schemas in prose; link to the versioned OpenAPI/AsyncAPI definition.
- Do not use a static code graph as proof of runtime behavior.
- Do not declare 'approved' just because an agent produced polished diagrams.

See [architecture template](../templates/architecture-design.md), [LLD template](../templates/detailed-design.md), [ADR template](../templates/adr.md).
