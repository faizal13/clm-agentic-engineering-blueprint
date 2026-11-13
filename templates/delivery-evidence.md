---
artifact_id: "DELIVERY-<ticket>"
artifact_type: dev-delivery-evidence
status: draft
source_ticket: "<ticket>"
revision: v1
---

# Verified DEV Delivery Evidence — <ticket>

## Required identity chain
| Field | Verified value and link |
|---|---|
| Ticket and approved revision | ... |
| Requirements/design/ADR revisions | ... |
| Approved test/eval spec revisions | ... |
| Pull request and human reviewers | ... |
| Commit SHA and CI run ID | ... |
| Artifact digest/signature | ... |
| DEV deploy ID and environment | ... |
| Runtime version verification | ... |

## Mandatory gate results
Build, lint/type, unit, contract, integration, SAST, secret scan, software dependencies, agent evaluation and permissions. All results link to their authoritative systems.

## Acceptance scenario outcomes
| AC/Test ID | Expected state | Measured state | API/trace/DB/query evidence ID | Pass/fail |
|---|---|---|---|---|

## Operational observations
Latency/error metrics, process state, event handling, audit entries, deployment window, known risks and SLO-related findings.

## Repair attempt history
| Attempt | Root cause hypothesis | Commit SHA | New CI/deploy run | Result | Approval |
|---|---|---|---|---|---|

## Security, exception and rollback status
Record failures, human escalation and whether rollback was needed or safe.

## Human acceptance
Signed decision, timestamp, authorized role. This document is **not** production deployment approval.
