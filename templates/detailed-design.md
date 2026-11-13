---
artifact_id: "LLD-<ticket>"
artifact_type: detailed-design
status: draft
owner: "<tech lead>"
revision: v1
source_ticket: "<ticket>"
architecture_delta: "<SAD-DELTA id + revision>"
---

# LLD — <ticket>

## Implementation intent
Concise feature description; linked approved requirements, HLD and ADRs.

## Component responsibilities and touched interfaces
| Component/module | Responsibility | Change | Source code / contract link | Owner |
|---|---|---|---|---|

## API/events/contracts
Link the versioned OpenAPI/AsyncAPI schema; list endpoint semantics, errors, auth scopes, schema compatibility and versioning decisions. Do not duplicate schema text unnecessarily.

## State/process logic
State transitions, roles/approval matrix, boundary conditions, rejection paths, retries, duplicates, timers and process compensation. Include a reviewed sequence/state diagram where helpful.

## Persistence and transactions
Schema changes, consistency boundaries, isolation/retry model, idempotency keys, migration/backfill and safe rollback or forward-fix.

## Security and auditability
OPA/policy engine or application authorization rules as actually verified in project, audit record contents without exposing sensitive data, permission failures and abuse cases.

## Error handling and resilience
Timeouts, retry budgets, dependency failures, dead-letter handling, partial success, circuit breakers, observability events.

## Implementation plan / tasks
Small, ordered tasks with dependencies and acceptance/test IDs. State prohibited changes.

## Testability and evidence
| AC ID | Unit/contract/integration/E2E case | Oracle | Test owner |
|---|---|---|---|

## Risks and open decisions
Explicit stop conditions if requirements/design context insufficient.

## Review and signoff
Architect/tech lead/QA, approved revision and linked decision log.
