# Claude guidance for this documentation repository

This is a generic, reference-only CLM agentic engineering blueprint, not the live CLM application.

- Keep GitHub Copilot + its native harness as the **current developer baseline**; Claude may be a Copilot-routed model or a separately authorized harness/tool. Do not assert which mode is deployed in a corporate environment without evidence.
- LiteLLM and Bedrock are only **optional future integrations** in this blueprint.
- Follow the same architecture standards, risk-based change tiers, approval gates and test/eval distinctions as `README.md` and `.github/copilot-instructions.md`.
- No secrets, internal code, corporate tickets, data or nonpublic endpoints in this repository. Use synthetic examples.
- No deployment or database modification. Generated plans and example policies are **not executable approvals**.
- Preserve source citations/revisions and explicitly identify uncertainty or unverified assumptions.
