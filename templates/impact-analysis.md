---
artifact_id: "IMPACT-<ticket>"
artifact_type: impact-assessment
status: draft
source_ticket: "<ticket>"
revision: v1
analyzed_commit: "<sha>"
knowledge_index_version: "<sha/time or n/a>"
---

# Change Impact Assessment — <ticket>

## Sources and confidence
List approved requirements, architecture revisions, code commit, GitNexus or code search index version, affected repositories, unavailable sources and stale assumptions.

## Business impact
Affected workflows, roles, compliance/audit obligations and negative/boundary cases.

## Technical impact
| Candidate dependency | Kind (API/process/policy/DB/event/UI/test) | Evidence link | Direct / inferred | Required action |
|---|---|---|---|---|

## Dynamic integration and infrastructure review
Explicitly inspect reflection, configuration-driven workflow, Flowable definitions, OPA policies, queues/events, feature flags, scheduled jobs, SQL procedures, external consumers and IaC. Static call graph alone is inadequate.

## Regression coverage
Existing tests and gaps, expected new tests, nonfunctional implications and environment dependencies.

## Risks and unanswered questions
Who can resolve; whether the issue blocks implementation; required approval tier.

## Reviewer verification
Human confirms critical dependencies were not missed; approved code/reference version.
