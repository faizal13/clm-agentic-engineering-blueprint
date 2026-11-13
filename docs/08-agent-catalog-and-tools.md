# 08 — Agent catalog, skills, tools and harness boundaries

## Philosophy

An **agent role** owns a distinct task, tool/permission context, or independent review perspective. A **skill** is a reusable procedure or body of knowledge loaded when needed. The **Copilot harness** orchestrates tool calls, state and approved actions. The **model** proposes content and next actions. Do not multiply agents simply to create a large org chart.

## Proposed logical roles

| Role | Inputs | Outputs | Tool access | Approval boundary |
|---|---|---|---|---|
| Requirements analyst | Ticket + linked approved documents | Structured brief, ambiguity list | Read ticket/context | Product owner approves scope/rules |
| Context researcher | Ticket and repository locations | Citation-backed context packet and impact candidates | Read knowledge/graph/code | Architect validates high-risk claims |
| Solution architect | Approved brief, baseline, context | HLD delta, tradeoffs, ADR candidate, NFR scenarios | Read design/code | Human architect approves decisions |
| Detailed designer | Approved HLD and contracts | LLD, sequences, interfaces, failure conditions | Read code/contracts | Tech lead validates implementation readiness |
| Test designer | Acceptance criteria, design | Test data, expected states, independent assertions | Read docs/code; write test plan | QA/product approves independent acceptance |
| Implementation agent | Approved plan, pinned contracts | Scoped code and developer tests on branch | Scoped Git/workspace; **no deploy/DB writes** | Protected PR checks and review |
| Code/security reviewer | Diff, design, policy and tests | Findings with evidence and severity | Read-only source/artifacts | Independent engineer makes merge decision |
| Build repair agent | CI failure, diff and fixed test spec | Small, auditable code patch | Scoped branch write | Retry budget; no test relaxation |
| Runtime verifier | Approved acceptance suite and DEV artifact | Measured evidence of real behavior | Read-only telemetry/DB diagnostic and approved test runner | Independent acceptance gate |
| Incident investigator | Correlated failure evidence | Diagnosis, reproducible case, proposed fix | Read-only logs/traces/deployments | Human escalation for unsafe/uncertain actions |

A pilot can use 3–4 actual agents plus reusable skills rather than provisioning every role as a separately deployed service.

## Example skills

- `ticket-to-design`: read ticket, gather authoritative context, produce a bounded design packet with citations; never auto-approve.
- `impact-assessment`: consult code/search/code graph, verify contracts and dynamic workflows; label missing coverage.
- `tdd-implementation`: produce failing deterministic tests, implement code, run tests, protect approved acceptance requirements.
- `verify-evidence`: collect CI/deploy/runtime records; compare against approved expectations.
- `architecture-review`: compare design delta with SAD/ADRs and measurable NFRs.
- `eval-review`: run repeatable agent behavior tests with saved version metadata.

See [sample agents and skills](../.github/agents/requirements-analyst.agent.md). Samples are conservative and **not** wired to your actual issue tracker or corporate systems.

## MCP service inventory (conceptual)

| Service | Example tools | Default scope |
|---|---|---|
| Work items | `get_ticket`, `list_linked_requirements` | Read only |
| Knowledge Fabric | `search_approved_docs`, `get_source_revision`, `get_adr` | Read only and ACL-filtered |
| Code intelligence | `find_symbol`, `get_callers`, `analyze_impact` | Read only and commit-pinned |
| GitHub | `read_repo`, `create_branch`, `commit_patch`, `create_pr` | Repo-specific scoped write |
| CI/CD | `get_job`, `request_ci_run` | Selected workflows only |
| Deployments | `request_dev_deploy`, `get_deployment` | Separate authorized service identity; guarded |
| Telemetry | `query_logs`, `get_trace`, `read_metrics` | Read-only, sanitized, time-bounded |
| Database diagnostics | `run_preapproved_query` | Read-only / parameterized / masked |

**Never** give the same agent a global Git token, production database write access, and deployment credentials merely for convenience.

## Design rules for agent interfaces

Each agent contract should specify: responsibility, required inputs, output schema and citations, allowed tools, forbidden actions, missing-data behavior, stopping conditions, escalation path, scoring rubric and owning human. Prefer structured outputs for handoffs, but keep human-readable Markdown as the review surface.

Example required implementation handoff:

```yaml
work_item: CLM-142
approved_spec_revision: v2
approved_design_revision: v3
scope_repositories: [clm-api]
allowed_paths: [src/main, src/test]
forbidden_operations: [production_deploy, database_write, weaken_approved_acceptance_tests]
maximum_repair_cycles: 3
```

This is an **illustrative policy contract**, not native Copilot syntax. Enforce it in tools, branch rules and CI too.

## Copilot vs Claude

There are multiple meanings of 'Claude': (1) a Claude-family **model provided through Copilot**, maintaining the Copilot harness; (2) the separate **Claude agent harness/tool** using its own account/SDK/permission semantics. Do not confuse them. Compare via controlled evals and corporate entitlements. The model picker selection can determine billing/provider; enterprise policy can disable alternate harnesses.

## Versioned agent release lifecycle

Proposal → test with sandbox eval dataset → human review → run on protected holdout → version and release → monitor outcomes → rollback on policy regression. Changes to tool descriptions, model selection, skill wording or context compression all count as behavior changes requiring evaluation.
