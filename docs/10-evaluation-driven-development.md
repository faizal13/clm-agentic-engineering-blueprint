# 10 — TDD + Evaluation-Driven Development (EDD)

## The correct distinction

Traditional test-driven development (TDD) remains required for deterministic code. Evaluation-Driven Development (EDD) adds a **behavioral and reliability specification** for LLM-powered features and agents. EDD doesn't replace unit, contract, integration or runtime acceptance tests. All remain necessary.

**Why:** Agent responses vary in wording, tool selection and intermediate steps. Exact-output assertions often reject valid variants and may miss hallucinations, unsafe tool calls or omitted constraints.

## What EDD measures in this blueprint

1. **Outcome:** did the software actually behave as approved (tests, API/DB/business state)?
2. **Process and safety:** did the agent follow authorization, source grounding, approved design, and change scope?
3. **Reliability and efficiency:** how consistently can it succeed across tasks, repeated trials, models and versions, without excess time/cost?

Separate results by dimension. A severe unauthorized tool call or data-integrity violation is a hard fail even with 99% quality score.

## Eval first workflow

1. Define system/agent under evaluation and intended use.
2. Produce an **Evaluation Specification** with reviewed target outcomes, scenario classes, graders and safety gates **before** optimizing prompts or adding complex agent loops.
3. Build task fixtures with source-of-truth reference documents, expected machine-verifiable state and seeded failure conditions.
4. Run baseline agent/harness/model/skill configuration; save all versions and traces.
5. Improve instructions, tool descriptions, retrieval or model choice.
6. Compare on the same dev/regression set and fresh protected holdout; repeat stochastic trials.
7. Approve only when mandatory constraints pass, confidence in reliability is adequate and significant regressions are absent.
8. Monitor real permitted use, convert incidents into regression cases and re-evaluate after any model/tool/harness update.

## Three grader families

| Grader | Suitable for | Avoid using it for |
|---|---|---|
| Deterministic code | JSON/YAML schema; required artifacts; tool allowlist; real tests; unauthorized diffs; latency limit; secret scans; API/DB assertions | Subjective correctness without explicit oracle |
| LLM-as-judge with calibrated rubric | Grounded explanation, completeness, tradeoffs, logical consistency, clarity of design | Sole security/release approval, objective runtime truth |
| Human subject matter expert | Ambiguous business rules, architecture tradeoffs, calibration, high-risk scenarios | Replacing scalable repeatable checks everywhere |

Model judges are biased and fallible. Provide references/citations, evaluate against human-labeled calibration sets, test answer-order/verbosity biases and audit disagreements. Don't use the same model to invent requirements, generate answers and automatically validate the resulting business truths.

## Dataset partitions

- **Development/capability**: representative but challenging scenarios actively used to improve the agent.
- **Regression**: previously accepted behavior and known past defects; expected to remain near-perfect.
- **Protected holdout**: scenarios not exposed to prompt optimization to detect overfitting; access-controlled.
- **Adversarial/security**: prompt injection through ticket, doc, code comment, log; unauthorized tool requests; fake approvals.
- **Real-world incident feedback**: sanitized failure cases added with provenance and human labels.

## Versions to record

`eval_suite_revision`, `dataset_split`, `fixture_revision`, `ticket_revision`, `approved_spec_revision`, `harness_version`, `model_id`, `agent_file_SHA`, `skill_file_SHA`, `MCP_tool_version`, `retrieval_index_revision`, `judge_model_and_rubric_revision`, `temperature_or_sampling`, `run_seed_if_supported`, `cost`, `duration`, `trace_reference`.

## Decision rule (example only)

```
REJECT if any critical invariant fails
REJECT if required acceptance test or scope/permission check fails
REVIEW if confidence intervals are too wide or judge disagreement is material
REVIEW if any high-severity holdout case regresses
CONSIDER APPROVAL only if defined quality thresholds and all human gates pass
```

Do not let a blended quality score 'compensate' for an unauthorized deployment or bypassed acceptance check.

## Practical CLM evaluations

- Ticket ambiguity: the agent asks which threshold equality case applies; it does not invent policy.
- Architecture grounding: the agent cites approved ADR version and uses current Flowable/OPA contract only if discovered in actual project context.
- Code correctness: independent tests confirm exact business state and event behavior.
- Retrieval accuracy: critical affected components identified, unsupported claims labeled as hypotheses.
- Safety: malicious ticket requests for production secrets are ignored; tool policy denies access.
- Reliability: run a sample of cases multiple times and record both first-pass success and success within bounded repair budget.

**Metrics:** first-attempt success, eventual pass within retries, hard-policy violations, regression failures, judge/human agreement, cost per accepted change, median/p95 latency, critical-component recall and evidence completeness. A 8/10 success count is only an estimate from a small sample, not proof of production reliability.

Further reading: [Anthropic: Demystifying evals](https://www.anthropic.com/research/demystifying-evals-for-ai-agents), [GitHub Copilot Evals Preview](https://github.com/github/evals).
