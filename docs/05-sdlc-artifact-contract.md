# 05 — SDLC stage and artifact contract

## Lifecycle is iterative, evidence-focused

Activities overlap: security and test design start with requirements; operations inform design; architecture is versioned as changes occur. 'Stage' below means **quality checkpoint**, not mandatory sequential waterfall phase.

| Stage | Required/authoritative artifact types | Gate / exit evidence | Primary approver |
|---|---|---|---|
| 1 Discovery | Business case/scope and stakeholder map; feasibility and high-level risks when material | Problem, outcomes, ownership and boundaries understood | Business owner |
| 2 Requirements | BRD or product brief, structured stories, functional and acceptance criteria, NFR/quality scenarios, business glossary/rules | Unambiguous, testable, prioritized and source-linked requirements | Product owner / BA |
| 3 Solution architecture | SAD/HLD baseline or delta, C4 views as needed, ADR for consequential choice, integration overview and threat assessment when relevant | Feasible architectural approach and quality constraints reviewed | Solution architect / security |
| 4 Detailed design | LLD/design delta, API/event/data contracts, runtime sequence/state diagram, data migration plan where needed | Implementable design and independently reviewable test plan | Tech lead / architect / QA |
| 5 Implementation | Approved implementation tasks, code, TDD tests, PR/change record | Build, static checks and required tests green; independent review | Tech lead / peer reviewer |
| 6 Verification | Test spec, traceability, executed test results, security/performance tests when relevant, AI Eval Specification for AI behavior | Acceptance and critical policy criteria objectively met | QA / test owner |
| 7 Deployment | Release and change record, artifact digest, rollout/rollback plan, approved deployment job, environment evidence | Authorized immutable build safely deployed | Release/platform owner |
| 8 Operation | Runbook, SLO/alerts, telemetry, incident/postmortem where relevant | Observability and support responsibility defined | Service owner/SRE |

**Default policy:** baseline docs live for the life of the project; change records live per ticket and point to authoritative baseline revisions and execution evidence. Don't copy logs into markdown; link to controlled systems of record with durable IDs.

## Baseline artifact inventory

1. System/product scope, domain glossary, business process maps and rule catalog.
2. Requirements baseline with traceable IDs and acceptance criteria.
3. SAD with views, diagrams, quality scenarios and system constraints.
4. ADR register; API/event/data schema contracts.
5. Threat model/security controls, risk register and system ownership.
6. Test strategy, environments/test data policy and regression catalog.
7. Delivery/deployment architecture, backup/rollback and operational runbooks.

## Change artifact inventory

1. Ticket brief and source revision.
2. Context packet with citations/revisions; impact analysis and uncertainty list.
3. Risk classification; focused HLD/LLD or ADR update if needed.
4. Approved acceptance-test specification; AI eval spec if an AI behavior or agent customization changes.
5. PR, CI evidence, reviewer approval, release evidence and traceability manifest.

## Three change tiers

| Tier | Examples | Minimum documents/reviews |
|---|---|---|
| **Small / low risk** | Isolated copy/UI change, simple localized bug without contract/data/security impact | Ticket, lightweight impact check, TDD/unit test, PR/CI evidence; no new HLD/LLD |
| **Feature / moderate** | Business feature in an existing service | Ticket, impacted baseline references, design delta/LLD, updated contracts when impacted, test cases and reviewed PR; ADR only if new architectural decision |
| **Major / high risk** | New service, security boundary, cross-system workflow, critical schema change | Formal requirements/NFR, architecture and threat review, HLD/C4 updates, detailed design, ADR/contract/data plan, testing/release/rollback plan, operational acceptance |

**Risk overrides size:** a one-line authorization or compliance change is not automatically 'small'. Default to higher scrutiny when transaction integrity, PII, audit, authorization or legal/regulatory impact is involved.

## Artifact metadata standard

Every approved document should include: `artifact_id`, `artifact_type`, `status`, `owner`, `reviewers`, `source_ticket`, `system`, `scope`, `revision`, `approved_at`, `source_revisions`, `linked_adr_ids`, `related_test_ids`, `supersedes` and `last_verified_at`. Use stable IDs and machine-readable metadata where feasible; never let an agent invent an approval status.

## Definition of Ready for agent implementation

- Requirement and business rule conflicts resolved or explicitly deferred.
- Relevant authoritative context retrieved with versioned citations.
- Scope and exclusions defined, including affected repo/environment.
- Architecture and design delta approved at proper risk tier.
- Approved acceptance tests, evaluation expectations and authorization envelope versioned.
- Owners, rollback assumptions and escalation channels identified.

## Definition of Done for verified DEV

- PR approved and merged under branch rules (or approved pre-merge deployment policy).
- All deterministic checks and required agent evals meet mandatory thresholds.
- Tested immutable artifact deployed through approved pipeline.
- DEV smoke/business tests and expected state assertions pass.
- No critical security or data-integrity anomalies; known limitations disclosed.
- Evidence manifest links exact ticket, SHA, CI run, deployment, tests and reviewer decisions.
- Out-of-scope issues recorded; production release requires a **separate** gate.
