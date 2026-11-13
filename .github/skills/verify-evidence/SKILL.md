---
name: verify-evidence
description: Assemble a factual evidence manifest linking a code change to approved tests, CI checks, DEV deployment and runtime verification; do not self-approve.
---

# Verify Evidence

1. Record exact ticket/revision, approved specs, PR and reviewer decision, commit SHA, CI run, tested artifact digest and environment deploy ID.
2. Use approved tools to read *existing* machine-verifiable CI and runtime results. If access is missing, label not verified; don't fabricate outputs.
3. Verify all acceptance tests and security/policy gates were executed at the correct artifact version.
4. For applicable CLM flows check process state, API, relevant event, sanitized DB diagnostic, logs, traces, audit and negative authorization behavior.
5. Identify unresolved failures, stale evidence, environment drift and repair history. For critical unknown failures recommend escalation, not a green status.
6. Produce `templates/delivery-evidence.md` as a draft summary with links to systems of record.

This skill does not grant tool permissions. It must never deploy, modify data, bypass review or change approved tests.
