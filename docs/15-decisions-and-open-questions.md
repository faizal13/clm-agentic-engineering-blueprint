# 15 — Decision record, alternatives and unknowns

## Current design decisions (proposal, pending organizational approval)

| ID | Proposed decision | Status | Rationale |
|---|---|---|---|
| D-001 | Native GitHub Copilot remains primary developer agent harness | Proposed | Preserve subscription capabilities, existing skills, user experience and supported integration |
| D-002 | Claude used as Copilot-routed model when entitled; standalone Claude tools only if authorized | Proposed | Avoid confusion between a model provider and a different harness/account |
| D-003 | No LiteLLM dependency at current stage | Confirmed current-state assumption | User is not currently using LiteLLM; avoid unnecessary integration |
| D-004 | Project-level baseline architecture + ticket-specific change deltas | Proposed | Reduce duplicate and stale AI-authored documents |
| D-005 | Independent accepted tests + agent evaluations before coding | Proposed | Separate business truth from generated implementation |
| D-006 | Deterministic security/permission/DEV gates outside the LLM | Proposed | Enforce controls even when the model misbehaves |
| D-007 | GitHub-native issue/PR/Actions first; durable engine only if needed | Proposed | Avoid premature platform engineering |
| D-008 | Bounded repairs, fresh commits, new CI/DEV evidence; no autonomous PROD | Proposed | Limit blast radius and prevent endless loops |
| D-009 | GitNexus only after commercial license/security diligence | Proposed | Upstream license explicitly noncommercial |

## Choices worth revisiting after pilot

**Copilot subscription vs LiteLLM/Bedrock:** native Copilot is simplest for interactive development, but does not guarantee routing all Copilot requests through a corporate gateway. Option A (BYOK through LiteLLM to Bedrock/other models) and Option B1 (LiteLLM `github_copilot/` upstream with per-developer auth) are future evaluations; do not assume billing or support compatibility. Debug/proxy interception should not be the enterprise default.

**GitHub-only orchestration vs Step Functions/other durable engine:** GitHub issues/Actions and Agentic Workflows may be sufficient for POC. Cross-system wait states, authorization across Jira/DEV, idempotent callbacks and long-running retries may justify AWS Step Functions or an existing enterprise orchestration platform later.

**GitNexus vs other code intelligence:** only choose after cost/license, dynamic-code coverage, index freshness, MCP and security proof. Existing language servers/code search and manual reviews remain viable.

**Monorepo vs multi-repo:** actual CLM topology determines graph federation, distributed change boundaries, PR coordination and deployment ownership.

## Answers still required from the organization

1. Work-item platform and API permissions; which ticket data is authoritative?
2. Which CLM repos, process engines, policies, frontend/backend and databases actually exist? Verify assumptions independently.
3. Where are approved BRD, SAD/HLD/LLD, contracts, ADRs and runbooks stored and who owns them?
4. Current GitHub plan, cloud agent permission, IDE policy, Claude subscription/model entitlements and compliance.
5. Existing build/test/release platforms, DEV environment and permitted automation identities.
6. Read-only observability and DB diagnostic interfaces; restrictions on sensitive data.
7. Architecture/QA/security and release approval ownership and lead times.
8. Target success thresholds, audit retention, capacity and cost budgets.
9. Corporate rules for personal GitHub repositories and third-party tools.

## Architecture review checklist

- Is the proposal based on actual requirements and approved references?
- Have dynamic/configuration/integration impacts been checked beyond static code search?
- Are error paths, retries, idempotency, audit and rollback included?
- Are interface/data ownership and trust boundaries explicit?
- Are outcomes deterministically testable and agent behaviors independently evaluable?
- Are model/provider/harness and tool/deploy responsibilities kept distinct?
- Which assumptions would stop implementation if false?
