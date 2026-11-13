# 01 — Enterprise strategy and current stack

## Present-state declaration (owner-supplied)

- GitHub Copilot subscription is available through the organization; VS Code, GitHub Copilot, custom agents/skills and Claude are current tools.
- LiteLLM is **not** currently used in this CLM engineering workflow. Previous LiteLLM/Bedrock ideas are **research paths**, not deployed design decisions.
- Organization previously reported access to AWS Bedrock and LiteLLM as enterprise capabilities, but **their allowed use, platform onboarding, model entitlements and governance for this project are unverified**.
- A separate `everything-copilot` repository exists; reuse its patterns after auditing current discovery paths and behavior, but do not alter it automatically.

## Core decision

Keep the **GitHub Copilot harness** as developer-facing orchestration. The **model** reasons and chooses proposed actions; the **harness** maintains agent state, invokes authorized tools, handles interactions and feedback. The **CI/CD system** validates and deploys. **Architecture and security governance** decide what is allowed. Do not collapse these responsibilities into one agent.

## Two immediate lanes

**Lane A — interactive Copilot:** ticket analysis, repository exploration, planning, coding, tests and PR preparation with a human developer reviewing changes. Optimize this first with native Copilot subscription models. Claude may be selected as a model under Copilot where available, or as a separately authenticated harness if explicitly permitted.

**Lane B — repository automation:** use GitHub issue/PR triggers, Copilot cloud agents (when enabled), GitHub Actions, and restricted automation for clearly scoped tasks. Add a durable cross-system controller only when asynchronous approval, deployment and telemetry workflows require it.

## LiteLLM + Bedrock: optional architectural choices, not dependencies

| Option | Model route | Harness remains Copilot? | Enterprise recommendation |
|---|---|---|---|
| Native Copilot | VS Code Copilot harness → GitHub Copilot model service | Yes | **Default now**: least migration and supported subscription experience. Not all inference passes a corporate gateway. |
| A: Copilot BYOK → gateway | Copilot harness → LiteLLM custom model endpoint → approved model provider, optionally Bedrock | Yes where supported and model tool-capable | Evaluate **only if** central model routing is required; BYOK/Agent Host controls may be experimental and do not cover every Copilot feature. |
| B1: Copilot BYOK → LiteLLM GitHub Copilot provider | Copilot harness → LiteLLM → GitHub Copilot upstream using individual account authorization | Potentially, subject to compatibility | **Research only**: subscription usage, enterprise policy, licensing, auth, streaming and tool calls must be verified. |
| B2: debug interception | Native Copilot traffic through an override/proxy | Uncertain | Do not rely on undocumented/debug endpoints for enterprise production. |
| Enterprise AI lane | Custom programmatic agent service → LiteLLM → Bedrock | Separate from Copilot | Useful later for background retrieval/evaluation/inference if justified and approved. |

**Important:** LiteLLM is a model gateway, *not* a replacement for the Copilot agent harness and not a durable deployment orchestrator. A direct Bedrock model call would typically use different billing/credentials from the GitHub Copilot subscription.

## Strategy principles

1. Preserve existing engineering controls and software architecture.
2. Prefer documented native capabilities over reverse-engineered service proxies.
3. Separate agent prompts/skills from nonnegotiable security policy.
4. Keep one authoritative source for each category of knowledge.
5. Require human approval of consequential design and acceptance criteria before autonomous coding.
6. Independent outcome verification, not the agent's self-report, decides success.
7. Protect source and business data, including logs used in evaluation and traces.
8. Start with a low-risk service, limited permissions, and measurable success criteria.

## Open diligence

- Confirm Copilot subscription tier, cloud agent entitlement, policy and per-model allowance.
- Distinguish Claude as Copilot-routed model vs a separate Claude subscription/API/harness.
- Confirm Jira/Azure DevOps issue system, repo topology, CI/CD provider, deployment tooling and environments.
- Determine whether corporate security mandates all inference via a gateway or only enterprise governance/auditing.
- Confirm corporate approval for GitNexus code indexing and commercial licensing.
- Establish who can approve architecture, test specification, PR, DEV deployment and production change.
