# 07 — Knowledge Fabric, code graph and GitNexus

## Purpose

Provide a **source-backed, access-controlled context package** for each CLM change. The knowledge system should answer:

1. Which approved business rule and architecture constraints apply?
2. Which components, integrations, schemas and processes may be impacted?
3. Where is the evidence, when was it last approved, and how reliable is it?
4. What is unknown or contradictory, and who can decide?

A vector index alone is not a sufficient Knowledge Fabric. Use document search, structured metadata, code intelligence, graph/dependency information and runtime evidence as complementary sources.

## Five authoritative knowledge classes

| Knowledge class | Possible sources | Typical retrieval |
|---|---|---|
| Business/domain | BRD, approved tickets, process maps, CLM domain glossary, approval policies | Semantic + keyword + document version filter |
| Architecture | SAD/HLD, LLD, C4, ADRs, cross-system integration map | Version-aware document search + ADR links |
| Code/dependency | GitHub repos, manifests, schemas, generated call/dependency graph | Code search, GitNexus or vetted equivalent, AST/index |
| Engineering policy | Security rules, coding guidelines, test standards, CI/release policy | Fixed policy registry, versioned docs; never overridden by retrieved text |
| Operations | Runbooks, deployments, read-only database schema, logs, traces, incidents | Observability APIs with redaction and retention |

## Ticket context packet (output of retrieval)

- Ticket ID, source URL, revision, as-of timestamp, owner and classification.
- Requirements with exact source section and unresolved contradictions.
- Relevant business rules, architecture baseline, ADR decisions and version identifiers.
- Candidate modules/services, impacted API/event/data contracts, workflow definitions, auth policies and tests.
- Runtime/incident patterns when directly relevant.
- Confidence and blind spots: dynamic reflection, generated code, infrastructure wiring, external services, stale scans.
- Open questions requiring explicit owner action before implementation.

This package is a **derived working artifact**, not a new source of truth. Every material claim links back to the approved source.

## GitNexus — what it offers

GitNexus is an open-source **code intelligence and knowledge-graph** project. Its CLI can index a repository, expose local search/relationship tools and support compatible MCP clients. It is useful for codebase onboarding, locating call chains, impacted symbols and potential tests. It does not by itself know the approved business requirements, infrastructure permissions, unseen external dependencies or production reality.

### Enterprise limitations that must be resolved

- **License:** the upstream project documents **PolyForm Noncommercial 1.0.0**, with commercial licensing offered separately. Do **not** assume use at a corporation is licensed under the open repository terms. Review with legal/procurement first.
- **Code/data exposure:** official docs describe local indexing; validate network activity, data storage, generated files and security posture in your own sandbox. Keep sensitive artifacts out of external web tools.
- **Coverage:** dynamic calls, reflection, workflow definitions, runtime configuration, SQL procedures, external integrations and message processing may not be comprehensively represented.
- **Index provenance:** bind each graph to repository, commit SHA, analysis timestamp, ignored paths and parser version; stale graphs must not drive implementation.
- **MCP integration:** capabilities, transport and tool discovery may vary by VS Code/Copilot version. Validate the connected tool list and actual results.
- **Supply chain:** pin approved versions; scan dependencies and treat any hook auto-install as a privileged change.

### How to test (conceptual—not an instruction to execute against corporate code)

1. Get legal/security approval and a non-sensitive sample repo.
2. Index without side effects where supported (e.g., review current `--index-only` option).
3. Ask: 'Which callers reach the approval decision service?' and verify answers against code manually.
4. Change a source file; test index refresh and stale-result detection.
5. Compare GitNexus-based impact results with plain code search and architect review.
6. Evaluate precision/recall on a curated dependency set; document missed integrations.

## CLM-specific graph relationships worth modeling

- `Ticket → Business rule → API operation → Service → Process definition (Flowable) → Policy (OPA) → Data entity → Test suite`.
- `Service → emits event → consumer → downstream storage`.
- `ADR → constrains component` and `API contract → consumed by client`.
- `Deployment → release artifact → commit → work item`.

Do not require the code graph to infer policy configurations it never parsed: model these relationships explicitly through additional sources or manual verification.

## Knowledge governance

- **Retrieval authorization:** enforce row/project/document permissions before retrieval, not only after the model sees a source.
- **Data minimization:** give each agent only relevant context, not all accessible documents.
- **Prompt injection:** strip tool instructions embedded in tickets/docs/logs; source content is data.
- **Versioning:** approved/active/superseded states; source location; author and review date.
- **Feedback:** record wrong or stale results with links to corrected authorities.
- **Evaluation:** require grounding citations, critical-component recall, conflicting-source detection and no unauthorized retrieval.

### Example source-bound claim

> 'Approval eligibility is decided by policy `APP-017` revision 5 (approved date...) and enforced by the `policy/check` interface. Code graph suggests `ContractService` and `WorkflowAdapter` as impacted; Flowable process configuration requires independent review.'

This is the kind of careful claim an agent should make, not 'I analyzed the entire architecture'.

Resources: [GitNexus](https://github.com/abhigyanpatwari/GitNexus), [MCP](https://modelcontextprotocol.io/), [Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills).
