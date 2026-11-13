# 14 — Staged roadmap and measures

## Important: plan, not an ongoing automated task

This is a sequencing guide. **Nothing here has been implemented against your CLM project.** No corporate system connection, deployment or code modification is implied.

## Phase 0 — Discovery and baseline

- Confirm actual entitlement and policy for Copilot, Claude model selection/Claude harness, cloud agents and CI.
- Audit `everything-copilot` custom agent/skills paths, frontmatter, hooks, installers and current VS Code behavior.
- Inventory CLM repos, ticket system, approved architecture corpus, API schemas, environments and existing automated tests.
- Define baseline task/eval suite and measure manual ticket-to-PR/DEV lead time.

**Exit:** grounded inventory, risk-approved pilot scope, baseline metrics.

## Phase 1 — Documentation and knowledge foundation

- Agree on baseline SAD structure (arc42 + C4), ADR and document metadata conventions.
- Define risk-based minimum artifact matrix and architecture/QA signoff workflow.
- Set up **read-only** approved Knowledge Fabric retrieval over a small scope; GitNexus only if commercial license and security review permit.
- Create ticket context packet with citations, outdated-source warnings and open questions.

**Exit:** one ticket produces a correct, reviewed requirements + context + impact packet.

## Phase 2 — Ticket-to-design gate

- Create requirements and design roles/skills with reviewed schema outputs.
- Draft focused HLD/LLD delta, NFR and independent acceptance/eval plan.
- Human approval records are versioned and machine-readable; implementation blocked before approval.

**Exit:** approved implementation-ready design contract.

## Phase 3 — Approved plan to verified PR

- Run Copilot implementation agent on isolated branch/worktree.
- TDD, CI, security and design conformance checks; protected PR and independent review.
- EDD suite tests agents/skills, retrieval grounding and policy behavior; compare model/harness versions.

**Exit:** reliable, reviewable PR for a low-risk scoped ticket.

## Phase 4 — DEV deployment and outcome checks

- Integrate existing release process, artifact digest and protected DEV environment.
- API, process, DB/read-only diagnostics, events and log/trace assertions.
- Evidence manifest links ticket, SHA, CI, DEV deploy and all accepted test scenarios.

**Exit:** repeatable, independently verified DEV delivery.

## Phase 5 — Bounded remediation and platform governance

- Diagnose CI/runtime failures with sanitized telemetry; allow capped in-branch fixes.
- Explicit stop/rollback policy; compare cost/reliability against manually supervised delivery.
- Extend from one service/ticket category only after empirical success.

**Exit:** improved reliability without security or architectural regressions.

## Metrics and acceptance economics

| Metric | Purpose |
|---|---|
| Median and p90 ticket-to-DEV elapsed time | End-to-end business value |
| Human review minutes per accepted change | Avoid shifting work into QA overhead |
| First-pass PR acceptance | Implementation quality |
| Post-deploy acceptance rate | Real-system correctness |
| Escaped defect/regression severity | Risk-adjusted delivery outcome |
| Critical policy violations | Non-negotiable safety |
| First-attempt vs bounded-retry success | Autonomous reliability without hiding loops |
| Retrieval grounding/critical dependency recall | Knowledge Fabric effectiveness |
| Cost per accepted change, compute/minutes, tokens | Commercial sustainability |
| Rollback/escalation frequency | Operational control |

A high percentage of AI-generated lines of code is not a success metric.

## Evaluation experiment design

Compare current manual+Copilot practice to the new process on matched, sanitized ticket samples. Track ticket complexity, missing context, codebase age, participant review effort and defects. Require repeated trials and explicit risk classification before concluding that the new workflow is better.
