# 02 — Copilot / Claude capabilities to review as of November 2026

**Treat feature flags, previews, availability and plan entitlement as moving targets. Validate on managed corporate VS Code and GitHub; do not assume everything is enabled.** Official links are collected in [sources](../reference/sources.md).

## Prioritized capabilities

| Capability | Likely benefit | Adoption test |
|---|---|---|
| Copilot Agent Host and session continuity | Preserve agent state across supported clients | Run and resume a multi-file change; confirm host/session behavior and approvals |
| Custom agents `*.agent.md` | Clear specialist role, tools and boundaries | Test discovery, delegated work, model/tool constraints and handoff |
| Agent skills `.github/skills/*/SKILL.md` | Reusable on-demand engineering methods | Verify actual load/discovery; merely placing the file is not proof it was used |
| Repository instructions | Consistent project conventions | Check `.github/copilot-instructions.md` and scoped instruction applicability |
| Claude family models via Copilot | Compare design/review/coding quality without abandoning native harness | Confirm model availability, quotas and actual source of billing |
| Claude harness in VS Code | Alternate agent execution model when corporate policy permits | Compare tools, skills, file edit semantics and access model; do not assume same harness |
| GitHub Copilot cloud agents | Issue-to-PR delegation without local IDE session | Confirm administrator enablement, data permissions and PR review |
| GitHub Agentic Workflows (`gh aw`) | Bounded repo automation from events/schedules | Review generated workflow and permissions; start read-only |
| Copilot SDK (transitioning to Microsoft Copilot SDK) | Programmatic Copilot harness sessions | Prototype a small read-only workflow only if repository triggers are insufficient |
| GitHub Copilot Evals (Preview) | Repeatable tests for agents/skills/local supported MCP | Test one agent with independent outcome grading and saved comparison |
| Hooks / plugins (varying maturity) | Policy-like tool interception, packaging and distribution | Verify support matrix and enterprise enforcement; hooks alone are not sufficient security controls |
| GitHub Actions / environment rules | Deterministic CI and protected deployment | Verify branch protections, approvals and environment restrictions |

## Migration audit for `everything-copilot`

- Map top-level `agents/`, prior `.copilot/skills/` or other custom paths into the currently documented native Copilot directories (`.github/agents/`, `.github/skills/`, `.github/instructions/`). **Inspect before moving** because some existing setup scripts may intentionally transform paths.
- Validate frontmatter against the current documented schema, not historical examples.
- Treat agent roles, skills and workflows as separate concepts. Reusable methodology should usually be a skill; an independent tool/permission context justifies a custom agent.
- Check how the toolkit is installed across multiple repositories, how updates are distributed and how agents actually receive project context.
- Confirm Claude support: selected Copilot-routed Claude model does **not** imply the Anthropic Claude harness is active; provider-specific credentials and policies may apply.
- Evaluate model choice against tasks (coding, architecture review, grounding, tool reliability, cost), not an assumed universal best model.

## Evaluation baseline before upgrading

Freeze a set of ticket tasks, accepted architectural answers, coding tests and permission checks. Record the **exact extension/harness version, models, instructions, skills, tools and repository revision** for baseline runs. Re-run after every feature adoption. A higher average score cannot override a critical policy regression.

## Useful official references

- [Agent harness concepts](https://code.visualstudio.com/docs/agents/concepts/agent-harnesses)
- [Agent harness choices and Claude](https://code.visualstudio.com/docs/agents/run/agent-harnesses)
- [Agent skills](https://code.visualstudio.com/docs/agent-customization/agent-skills)
- [Customization migration](https://code.visualstudio.com/docs/agent-customization/migrate-customizations)
- [GitHub Copilot cloud tasks](https://docs.github.com/en/copilot/how-tos/copilot-on-github/use-copilot-agents/kick-off-a-task)
- [GitHub Agentic Workflows](https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows)
- [Copilot Evals Preview](https://github.com/github/evals)
