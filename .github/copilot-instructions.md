# Guidance for Copilot working in this BLUEPRINT repository

This repository contains **generic design/reference documentation**, not the real CLM application or an approved deployment workflow. Do not claim corporate connectivity or deployment success.

- Keep the **current** default stack as GitHub Copilot subscription + VS Code Copilot harness + allowed Claude model/tool; LiteLLM is **not implemented** here. Distinguish current, optional, and unverified tools.
- Never insert actual customer contracts, internal ticket data, secrets, private hostnames, source code or logs without organization approval.
- Prefer versioned baseline architecture and small change-specific deltas. Do not regenerate the full SAD or create redundant documents per ticket.
- Apply risk-tiered documentation and human architecture/QA/security approvals.
- Keep TDD for deterministic software and EDD for probabilistic agent and AI-system behaviors. A critical safety/authorization failure blocks approval regardless of aggregate quality score.
- Any deployment instructions in this repo are **illustrative only**. Never attempt to deploy, change DB data, bypass CI/branch protections or relax approved acceptance tests.
- When drafting architecture, cite authoritative requirements and code/data source revisions; explicitly mark missing context or assumptions.
- For tools/agent/skill configuration, consult the current official docs because schemas and availability change.
- Preserve immutable evidence identifiers in lifecycle designs: ticket, design, PR, commit, CI run, artifact digest, deployment and runtime trace.
