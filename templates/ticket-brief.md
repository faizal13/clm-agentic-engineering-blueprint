---
artifact_id: "REQ-<ticket>"
artifact_type: ticket-brief
status: draft # draft | in_review | approved | superseded
owner: "<name/role>"
reviewers: []
source_ticket: "<ID and canonical URL>"
source_revision: "<immutable revision/last_modified>"
system: "<system>"
revision: v1
---

# Ticket Brief — <ticket title>

## Business outcome and motivation
What measurable business behavior changes? Why is it needed now?

## Scope / non-scope
In scope: …  
Out of scope: …  
Affected users, processes, services and environments: …

## Requirements and source references
| Req ID | Precise requirement | Authoritative source + revision | Priority | Owner |
|---|---|---|---|---|
| REQ-001 | … | … | … | … |

## Business rules and edge cases
Boundaries; equality; currency/timezone; special privileges; amended/revoked contracts; duplicate/replayed events; exceptions; backward compatibility; auditability.

## Testable acceptance criteria
| AC ID | Given / When / Then | Observable oracle | Risk |
|---|---|---|---|
| AC-001 | Given … when … then … | API + approved DB state + event | … |

## NFR and compliance scenarios
Performance, resiliency, confidentiality, authorization, audit retention, availability, accessibility as applicable; state measurable target and method.

## Ambiguities and decisions needed
| Question | Why it blocks design | Decision owner | Resolution / date |
|---|---|---|---|

## Dependencies / assumptions
Explicit assumptions and source-backed dependencies; no invented platform details.

## Approval evidence
Approver; decision; time; approved revision; ticket/source URL. Do not fabricate signatures.
