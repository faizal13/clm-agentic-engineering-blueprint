---
name: ticket-to-design
description: Turn an authorized work item plus approved project context into a scoped impact assessment, HLD/LLD delta proposal, and reviewable acceptance/test plan. Use before implementation.
---

# Ticket to Design

When given a work item:

1. Read the ticket and record URL, revision, scope and authoritative owner. If access is unavailable, request the missing source rather than invent details.
2. Retrieve only relevant, permission-filtered approved BRD, SAD, C4, ADR, API/AsyncAPI, data and test baselines. Cite revision, owner and source link for each material fact.
3. Use allowed code search / code graph to identify candidate impacts. Explicitly inspect dynamic workflow, policy, event, DB and infra dependencies independently where available; label unverified links.
4. Enumerate business rule boundaries and unanswered questions. **Do not proceed** when a critical ambiguity remains.
5. Risk-classify the change; avoid unnecessary architecture documents for low-risk localized changes.
6. Produce a draft ticket brief, impact table, focused design delta/ADR candidate only when justified, and independent proposed test/eval scenarios using repository templates.
7. Include owner review actions, no implied approvals and no executable deployments.

Success means an architect and QA owner have an actionable, source-backed **draft** to review, not that code was written.
