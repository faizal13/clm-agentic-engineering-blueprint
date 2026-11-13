# 12 — Delivery pipeline, runtime verification and bounded remediation

## CI pipeline (deterministic foundation)

Commit → compile → lint/type/static analysis → unit tests → component/integration tests → contract tests → security/dependency/secret scans → required agent-eval suites → independent code review → approved artifact build and signature → DEV deployment job.

Do not use an LLM judge to determine whether a Maven test failed, a PR is approved, an artifact digest matches, or an API status is correct. Use structured machine outputs.

## DEV deployment contract

Deployment request contains `ticket_id`, `approved_commit_sha`, `artifact_digest`, `environment`, `approval_record`, `change_risk`, `rollback_reference` and `correlation_id`. The deploy service checks identity, protected branch/rules, artifact provenance and environment approval. Agents may request an approved workflow but cannot self-grant permission.

## Runtime verification (application-specific)

1. **Deployment health:** expected version/digest running, startup and probes healthy, key resources and dependencies reachable.
2. **API contract:** request/response/schema, authentication and authorization, expected error codes and idempotency.
3. **Business state:** CLM lifecycle transitions, approvals, revisions, deadlines and audit events consistent with accepted requirements.
4. **Process/event:** expected Flowable process state or equivalent; message publication/consumption, retries, duplicates and dead-letter behavior.
5. **Persistence:** **read-only, approved parameterized queries** verify business invariants, referential integrity and expected state; no raw confidential rows in agent prompts.
6. **Observability:** correlate logs, traces, metrics, alerts and deployment window; avoid log substring-only checks as the sole oracle.
7. **Quality:** latency/error budgets and security requirements where within risk classification.
8. **Acceptance:** evidence for every approved scenario; record version and environmental assumptions.

## Example: contract approval additional step

The evaluator should not merely check HTTP 200. It should verify: expected next approver identity/role; state transition occurred exactly once; authorized/unauthorized permissions behave correctly; audit record exists; downstream notifications/events are correct; retry does not duplicate state; below/equal/above boundary behavior matches approved policy.

## Repair policy

| Failure type | Agent activity | Gate |
|---|---|---|
| Compiler, formatter, lint | Patch code, rerun CI | 1–3 bounded attempts |
| Unit/integration failure | Diagnose and add compliant fix | Re-run all impacted + regression tests |
| Approved contract mismatch | Preserve contract, suggest fix | Contract changes require owner approval |
| Infrastructure transient error | Retry idempotently | Capped retries, classify cause |
| DEV app failure | Read sanitized telemetry, create new branch commit | Deploy **new immutable artifact** with approval and fresh validation |
| Unauthorized access/secret, data corruption, unknown high-impact state | **Stop** | Human incident response and rollback assessment |
| Repeated oscillating changes or exhausted budget | **Stop** | Report diagnostic timeline and evidence |

**Never:** directly hotpatch live containers, change acceptance criteria without sign-off, disable security checks, mutate production data, extend privilege scope in the loop, or merge the agent's own PR without mandatory review.

## Agent observability vs application observability

- **Agent:** role, model/harness versions, tool names and arguments (redacted), permission denials, trace, repair attempts, tokens, cost, duration, decisions and final artifact IDs.
- **Application:** deploy version, request/correlation IDs, traces/spans, logs, metrics, queue health, DB state checks, feature flags, errors and SLOs.
- **Join key:** `ticket_id → agent_run → PR → commit_SHA → CI_run → deployment_id → runtime_trace_id`.

Use OpenTelemetry where supported; apply sampling, least-privileged viewers, data minimization and retention. Capturing full prompts/source code into telemetry may be inappropriate for enterprise IP or privacy.

## Rollback and forward fix

Prefer tested artifact rollback for safe reversibility. For schema migrations, irreversible data changes or external side effects, rollback may be unsafe; use approved forward fix/incident response. Record which alternative is valid in the deployment plan **before** execution.

## Completion report

Acceptance is achieved only when all mandatory technical and business evidence passes at the expected artifact version and required humans confirm status. 'Agent reports success' is not a completion criterion.
