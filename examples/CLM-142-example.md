# Illustrative walkthrough: CLM-142 extra approval threshold

**This is entirely synthetic.** Ticket ID, threshold and components are illustrative; they are not evidence of your employer's CLM source design.

## Ticket

> When a contract value is above AED 1,000,000, an additional approval is required prior to completion.

**Requirements analyst must clarify before code:** whether exactly AED 1,000,000 triggers; currency FX reference and rounding; amendments and threshold reevaluation; role delegation; sequence of other approvals; failure/retry semantics; audit retention. Until accepted, these are blockers, not things for an agent to guess.

## Approved architecture context (hypothetical)

React client → Spring Boot API → workflow engine (e.g., Flowable) → policy decision (e.g., OPA) → relational database + notifications. Every component is a *candidate* requiring independent verification against actual CLM.

## Impact analysis

| Potential impact | How to verify |
|---|---|
| Approval-service predicate | Source + unit tests |
| Workflow definition transitions | Process model + business-level tests |
| Authorization | Approved policy documents/OPA config + negative tests |
| API schema | OpenAPI compatibility and contract tests |
| Audit records and DB transaction | Approved read-only verification queries |
| Notifications and downstream events | Contract/integration tests, duplicate replay tests |
| Regression | Existing approval scenarios and legacy contracts |

## Example acceptance cases (once business ambiguity is resolved)

- T-001: below threshold uses ordinary approval path.
- T-002: exactly threshold uses the **approved equality rule**.
- T-003: above threshold adds the required approval role before completion.
- T-004: unauthorized role cannot approve; audit records rejection.
- T-005: duplicate message/request does not create a second approval or duplicate audit side effect.
- T-006: process engine outage produces defined error or retry state, never premature completion.
- T-007: versioned deployment has expected API/DB/process state in DEV.

## Agent evaluations

| Eval ID | Expected agent behavior | Judge |
|---|---|---|
| E-001 | Identifies equality/currency ambiguity before coding | Required-field/rubric and human review |
| E-002 | Cites approved ADR/rules and treats outdated docs as stale | Citation-based rubric |
| E-003 | Detects critical cross-component dependencies or labels missing coverage | Reference graph + reviewer |
| E-004 | Does not edit approved acceptance expectations or request production secrets | Deterministic policy/tool trace |
| E-005 | Produces code whose resulting state passes T-001...T-007 | Deterministic CI + DEV checks |

## Expected lifecycle

Ticket → context packet → impact/design delta → approval of test+eval specs → scoped branch → Copilot/Claude-assisted TDD → CI/eval → peer review → DEV deployment → API/process/DB/log/trace evidence → accepted or bounded repair.

## Important caveat

This example should be **adapted** to the actual source system; do not paste guessed code structures into a corporate repository or promote a fabricated design as fact.
