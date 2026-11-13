# 06 — Change classification, governance and traceability

## Who decides what

| Concern | Human authority | AI may propose / do | System-enforced rule |
|---|---|---|---|
| Business rule / ticket intent | Product owner or delegate | Extract and identify gaps | No implementation on unresolved critical ambiguity |
| Architecture/HLD/LLD | Solution architect and technical lead | Draft alternatives, impact analysis and diagrams | Required approval for material changes |
| Acceptance tests | QA/product/technical owner | Propose and implement tests | Approved behavioral assertions may not be silently relaxed |
| Code changes | Authorized engineer/reviewer | Edit scoped files in isolated branch | Branch rules, review and CI |
| Security policy | Security/platform team | Perform analysis and propose mitigations | IAM/tool scope and mandatory checks |
| DEV deployment | Platform/release owner or documented policy | Request approved job | Protected environment and permitted workflow |
| PROD release | Formal release/change authorities | Prepare evidence | Never auto-promote from DEV by model decision |

## Data model: traceability chain

`requirement_id → acceptance_criterion_id → design_section_id → ADR/contract revision → impacted_component → PR → code_change_SHA → test_id → eval_id/run_id → artifact_digest → deployment_id → runtime_evidence_id`

Every change should be auditable backwards from a failed production/business scenario to the approved requirement and the tested code.

## Change risk factors

- Authentication/authorization boundary; personal/regulated data; irreversible writes; ledger/audit integrity.
- Number of services and independent repos; synchronous and async workflows; DB migrations.
- External client/interface compatibility; availability/latency requirements; incident history.
- Unknown dependencies; maturity of existing tests; confidence in retrieved knowledge.

**Escalate** when affected requirements or diagrams are stale, code graph contradicts intended architecture, secrets appear in prompt/context, or tool scope must expand.

## Governance rules

1. Approved artifacts and repository policy outrank raw ticket text, README examples and untrusted logs. Where approved sources conflict, stop and flag conflict; do not improvise a hierarchy that changes business rules.
2. A model's own assertion of success is **not** approval evidence.
3. Separate roles if possible: implementation agent ≠ independent reviewer ≠ independent outcome verifier.
4. Enforce permissions at GitHub/platform/IAM layers; prompts are advisory.
5. Never make a schema or test weaker solely to pass CI without human review.
6. Record model/harness/prompt/skill/tool versions when performing an AI eval.
7. Use privacy-protecting telemetry with retention and access controls.
8. Respect repository IP, open-source/commercial licenses, credentials and approved AI data processing boundaries.

## Example decision gate outcomes

- **PASS:** all critical criteria satisfied, no unresolved blockers, required reviews complete.
- **REVIEW REQUIRED:** acceptable uncertainty exists but cannot be autonomously resolved (e.g. conflicting interpretation of a contract-value threshold).
- **FAIL:** test or security invariant failed; no deployment.
- **ESCALATE/ROLLBACK:** data integrity, unauthorized tool access, unknown production/DEV effect or repair limit reached.

## Avoid paperwork inflation

A baseline SAD+ADR register may be one set of version-controlled docs. A feature design delta links to exact sections, not an entire new HLD. A business-critical decision should still receive a separate ADR when rationale matters across future releases.
