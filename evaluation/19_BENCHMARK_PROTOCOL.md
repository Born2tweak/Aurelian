# 19_BENCHMARK_PROTOCOL -- Evidence-Based Comparisons

This protocol defines how to compare projects, milestones, models, and routing strategies without inventing benchmark numbers. It complements `17_EVALUATION_PROTOCOL.md`, `18_PROJECT_SCORECARD.md`, and `../core/16_EVALUATION_ENGINE.md`.

Benchmarks answer comparative questions. They do not prove universal superiority. A benchmark result is evidence about the tasks, constraints, and tools tested.

## 1. Benchmark Types

Use this protocol to compare:

1. Before vs after Aurelian.
2. Project vs project.
3. Milestone vs milestone.
4. Model vs model.
5. Routing strategy vs routing strategy.

## 2. Universal Benchmark Rules

1. **State the benchmark question.** What decision will the comparison change?
2. **Define units.** Name the task, project, milestone, model, route, prompt, or artifact being compared.
3. **Create a baseline.** Record the starting state before intervention.
4. **Control variables.** Keep repo, prompt, task, tools, timebox, model version, and verification environment as similar as possible.
5. **Declare metrics before running.** Choose quality, efficiency, risk, cost, coverage, or outcome metrics before seeing results.
6. **Collect evidence.** Use logs, diffs, tests, scores, screenshots, source tables, token data, review findings, and reports.
7. **Measure variance when possible.** Run multiple tasks or repeated trials when stochastic model behavior matters.
8. **Avoid causal overclaiming.** If controls differ, call the comparison approximate.
9. **Report limitations.** Name confounders, missing evidence, and non-comparable conditions.
10. **Do not invent numbers.** If a metric was not measured, say not measured.

## 3. Metrics Menu

Choose only metrics that fit the benchmark question.

| Metric class | Examples |
|---|---|
| Quality | scorecard category scores, defect count, review severity, task success |
| Verification | tests run, evidence ladder depth, unsupported claims, reproducibility |
| Efficiency | wall-clock time, agent turns, token usage, context reuse, manual intervention count |
| Cost | model cost, premium model calls, tool/runtime cost where measured |
| Risk | rollback readiness, security findings, data/money/public-contract exposure |
| Knowledge | docs updated, stale docs removed, trace links added, orphaned research reduced |
| Product | UX task success, accessibility findings, performance traces, visual defects |
| Research | source reliability, contradiction handling, confidence, implementation value |

## 4. Before Vs After Aurelian

Goal: determine whether loading Aurelian improved agent behavior or project outcomes.

Required controls:

1. Same or comparable task.
2. Same repository state or equivalent fixture.
3. Same model/harness where possible.
4. Same timebox and tool access where possible.
5. Same scoring rubric.

Measure:

- Scope control.
- Repository understanding.
- Plan quality.
- Implementation quality.
- Verification quality.
- Evidence-grounded reporting.
- Durable learning.
- Token/context efficiency if logs exist.
- Regressions introduced by added process or verbosity.

Use `17_EVALUATION_PROTOCOL.md` for the task-level rubric. Use `18_PROJECT_SCORECARD.md` when comparing project state before and after Aurelian adoption.

## 5. Project Vs Project

Goal: compare two projects for quality, maturity, risk, maintainability, product readiness, or investment priority.

Required controls:

1. Same scorecard or declared weight differences.
2. Comparable project type and maturity, or explicit normalization.
3. Comparable evidence depth.
4. Same evaluator where possible.

Measure:

- Overall score and category scores.
- Confidence per project.
- Evidence depth.
- Risk profile.
- Next milestone cost.
- Non-comparable dimensions.

Never rank projects from raw score alone when confidence or scope differs materially.

## 6. Milestone Vs Milestone

Goal: determine whether quality improved, regressed, or shifted across project checkpoints.

Required controls:

1. Same project.
2. Clear milestone boundaries.
3. Evidence from each milestone.
4. Same or comparable scorecard.

Measure:

- Category score trend.
- New risks introduced.
- Risks retired.
- Verification coverage change.
- Documentation freshness.
- Rollback readiness.
- Commit/review quality.
- Model routing or token efficiency changes when available.

Trend labels:

- **Improved:** evidence shows a meaningful positive change.
- **Regressed:** evidence shows a meaningful negative change.
- **Unchanged:** evidence shows no material change.
- **Mixed:** categories moved in different directions.
- **Not comparable:** scope, evidence, or scoring changed too much.

## 7. Model Vs Model

Goal: compare model performance on the same task class.

Required controls:

1. Same prompt or equivalent prompt.
2. Same repository state and tool permissions.
3. Same Aurelian files loaded, unless the benchmark is about loading strategy.
4. Same timebox, autonomy boundary, and verification requirements.
5. Same evaluator and scoring rubric.

Measure:

- Task success.
- Correctness and regression rate.
- Repo understanding.
- Scope control.
- Verification behavior.
- Unsupported claims.
- Review finding quality.
- Token usage and cost if available.
- Need for user intervention.

Do not generalize from one task to all tasks. Report the task distribution.

## 8. Routing Strategy Vs Routing Strategy

Goal: compare how work allocation across models, tools, or agents affects outcome quality and efficiency.

Required controls:

1. Same objective and project state.
2. Same available tools.
3. Clear route definitions.
4. Same verification standard.
5. Same handoff contract.

Measure:

- Route correctness by task type.
- Handoff loss.
- Duplicate work.
- Premium model usage that did or did not change outcome quality.
- Context efficiency.
- Verification closure rate.
- Review coverage.
- User-visible outcome quality.

Use `../core/13_MODEL_ROUTER.md` to define expected routing and `../core/16_EVALUATION_ENGINE.md` to score outcomes.

## 9. Benchmark Report Format

```text
Benchmark Report

Benchmark question:
Comparison type:
Units compared:
Scope:
Non-goals:
Evaluator/model/harness:
Date:

Baseline:

Controlled variables:

Variables that differed:

Metrics declared before measurement:

Evidence collected:

Results:
- metric:
  unit A:
  unit B:
  difference:
  confidence:
  evidence:

Interpretation:

Limitations and confounders:

Recommended decision:

Follow-up benchmark:
```

## 10. Invalid Benchmark Claims

Do not claim:

- "Aurelian improved quality by X" without measured baseline and post-Aurelian scores.
- "Model A is better than Model B" from different tasks or tool access.
- "Routing strategy is more efficient" without measured effort, token, cost, or intervention data.
- "Project A is higher quality" when Project A had deeper evidence and Project B was barely inspected.
- "Performance improved" without a performance measurement.
- "Token efficiency improved" without token or context-use evidence.

## 11. Minimum Benchmark Checklist

- Benchmark question stated.
- Units compared named.
- Baseline recorded.
- Metrics declared before measurement.
- Controls and differences listed.
- Evidence references included.
- Confidence assigned per result.
- Limitations stated.
- No invented numbers.
- Recommended decision follows from measured evidence.
