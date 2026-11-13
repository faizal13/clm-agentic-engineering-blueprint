# Reference documentation and due diligence links

**Assembled:** 13 November 2026. Links and maturity change; reverify availability, exact schema, preview flags, account entitlements and enterprise policy before adoption. Standards may be paywalled. These links support the blueprint; they do not prove your organization's environment supports each feature.

## GitHub Copilot and VS Code

- [VS Code agent harness concepts](https://code.visualstudio.com/docs/agents/concepts/agent-harnesses) — model vs harness vs environment distinctions.
- [VS Code choose agent harness](https://code.visualstudio.com/docs/agents/run/agent-harnesses) — Copilot and Claude harness options and cautions.
- [VS Code agent skills](https://code.visualstudio.com/docs/agent-customization/agent-skills) — `.github/skills` and skill discovery.
- [VS Code configure AI for codebase](https://code.visualstudio.com/docs/agents/guides/customize-copilot-guide) — instructions, agents and skills.
- [VS Code migrate customizations](https://code.visualstudio.com/docs/agent-customization/migrate-customizations) — native paths and migrations.
- [VS Code hooks](https://code.visualstudio.com/docs/agent-customization/hooks) — preview hooks and policy limitations.
- [VS Code language models](https://code.visualstudio.com/docs/agent-customization/language-models) — custom endpoint options if evaluating BYOK later.
- [GitHub Copilot cloud agent: kick off task](https://docs.github.com/en/copilot/how-tos/copilot-on-github/use-copilot-agents/kick-off-a-task) — issue-to-PR cloud workflows.
- [GitHub Agentic Workflows](https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows) — `gh aw` markdown to GitHub Actions workflows.
- [GitHub Copilot SDK docs](https://github.com/github/copilot-sdk/blob/main/docs/README.md) — programmable agent sessions, evolving SDK.
- [GitHub Copilot SDK brand transition announcement, 28 Oct 2026](https://github.blog/changelog/2026-10-28-github-copilot-sdk-is-becoming-microsoft-copilot-sdk/).
- [GitHub Copilot Evals (Preview)](https://github.com/github/evals) and [VS Code extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-evals) — agent, skill and selected MCP evaluation workflows.
- [GitHub Actions deployment environments](https://docs.github.com/en/actions/how-tos/deploy/configure-and-manage-deployments/manage-environments) — environment protection and plan-specific feature limits.

## AI evals and model access

- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/research/demystifying-evals-for-ai-agents) — outcomes, tool traces, deterministic/model/human grading.
- [OpenAI evaluation best practices](https://developers.openai.com/api/docs/guides/evaluation-best-practices) — eval design and iteration practices.
- [LiteLLM provider catalog](https://docs.litellm.ai/docs/providers) — future options only.
- [LiteLLM subscriptions](https://docs.litellm.ai/docs/subscriptions) — future investigation of Copilot/Claude subscription routing; commercial, policy and compatibility diligence required.
- [AWS Step Functions developer guide](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html) — optional durable orchestration if native GitHub workflow becomes insufficient.
- [Model Context Protocol](https://modelcontextprotocol.io/) — external tool/context transport concept; tool permissions still enforced by systems.

## Code intelligence

- [GitNexus source](https://github.com/abhigyanpatwari/GitNexus) — indexing and code relationships.
- [GitNexus readme / license](https://github.com/abhigyanpatwari/GitNexus/blob/main/gitnexus/README.md) — PolyForm Noncommercial 1.0.0; commercial licensing needed for ordinary enterprise use.

## Architecture / SDLC standards and practical frameworks

- [ISO/IEC/IEEE 42010:2022](https://www.iso.org/standard/74393.html) — architecture description.
- [arc42](https://arc42.org/overview/) — software architecture template.
- [C4 model](https://c4model.com/) — context/container/component/code diagram viewpoints.
- [MADR](https://adr.github.io/madr/) — Markdown ADR pattern.
- [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html) — software product quality model.
- [ISO/IEC/IEEE 29148:2018](https://www.iso.org/standard/72089.html) — requirements engineering.
- [ISO/IEC/IEEE 29119-3:2021](https://www.iso.org/standard/79429.html) — test documentation.
- [ISO/IEC/IEEE 12207:2026](https://www.iso.org/standard/90219.html) — software lifecycle processes.

## Commercial and corporate-policy warnings

Licensing, model billing, terms-of-service, retention, source-code privacy and managed settings must be confirmed by organizational legal/security/platform teams. GitHub private repository settings are not a substitute for organization-approved data residency and access control.
