---
artifact_id: "SAD-DELTA-<ticket>"
artifact_type: solution-architecture-delta
status: draft
owner: "<solution architect>"
reviewers: []
source_ticket: "<ticket>"
revision: v1
baseline_sad: "<SAD id + revision>"
related_adr_ids: []
---

# Architecture / HLD Delta — <ticket>

## 1. Context, motivation and scope
Business change, stakeholder concerns, assumptions and explicit boundaries.

## 2. Baseline references
Existing SAD revision, relevant C4 views, domain model, ADR decisions, NFR baseline, API/event contracts and source links.

## 3. Constraints and quality scenarios
Security, authorization, deployment, data residency, performance, reliability, audit, compatibility. Each quality scenario: stimulus → environment → measurable response.

## 4. Proposed architecture change
What changes, why, what remains stable, what alternatives were rejected.

## 5. Impacted boundaries and integration points
| System/component | Current responsibility | Proposed delta | Interaction | Evidence/source |
|---|---|---|---|---|

## 6. Diagrams
C4 context/container/component only where relevant; a runtime sequence for critical journey; deployment/trust boundary if impacted. Diagrams must be version controlled and source-reviewable.

## 7. Data, identity and audit implications
Ownership, schemas, access, authorization, audit trail, data lifecycle/migration and consistency.

## 8. Failure behavior and operational readiness
Timeouts, retries, idempotency, compensation, rollback, monitoring, alerting and support.

## 9. Architecture decisions
Record new consequential decisions as ADRs; link existing decisions and explain constraints, not copy them.

## 10. Risk, alternatives, open questions
| Risk/question | Severity | Impact | Mitigation or owner | Status |
|---|---|---|---|---|

## 11. Acceptance of design
What technical evidence proves the proposed architecture supports the functional/NFR scenarios? Trace to test IDs.

## 12. Review and approval
Approvers, feedback, revision, date, explicit outcome. No implied approval from LLM output.
