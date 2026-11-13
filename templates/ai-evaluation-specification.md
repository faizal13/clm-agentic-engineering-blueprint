---
artifact_id: "EVALSPEC-<agent-or-feature>"
artifact_type: evaluation-specification
status: draft
owner: "<evaluation owner>"
revision: v1
system_under_evaluation: "<agent/skill/prompt/tool/model/workflow>"
---

# AI Evaluation Specification — <system/agent>

## Purpose, scope and risks
Task family and users, expected actions, allowed failure modes, severity classification, changes that trigger re-evaluation.

## Configuration fingerprint
Harness/extension version, model/provider/billing path, agent/skill/prompt file revisions, MCP tool versions, repo SHA, context index revision and judge rubric version.

## Datasets and provenance
| Dataset/split | Origin/sensitivity | Coverage | Access | Owner/version |
|---|---|---|---|---|
| Capability/dev | Synthetic/reviewed | ... | Engineers | ... |
| Regression | Resolved issues | ... | QA | ... |
| Protected holdout | Expert-created | ... | Restricted | ... |
| Adversarial | Prompt injection, bad permissions | ... | Security | ... |

## Evaluation cases
| Eval ID | Fixture/input | Reference behavior or environment outcome | Grader | Criticality |
|---|---|---|---|---|

## Deterministic gates
Schema, source revisions, bounded tool allowlist, unauthorized action count = 0, compile/tests, artifact digest, acceptance scenarios, latency and budget thresholds as defined.

## LLM judge rubric
Exact rubric with anchored scores; supporting source citations required; distinguish completeness, factual grounding, reasoning and clarity. Record judge model, calibration cases and disagreement policy.

## Repeated-trial design
Trial count, task stratification, first-pass and within-budget repair success, confidence intervals, failure taxonomy and regression baseline.

## Promotion rule
**Hard fails:** any critical security/data integrity/unauthorized tool action; failing approved business acceptance; unacceptable high-severity holdout regression. Weighted metrics cannot override.

**Other gates:** minimum performance on defined cases, confidence and critical case coverage, expert signoff for high risk, no significant unexplained drift in cost/latency.

## Evidence report and ownership
Where to find per-case traces (sanitized), dataset run manifest, human calibration samples, approval/rejection and rollback path.
