# 26_PROJECT_EVALUATION_SKILL -- Evaluate Projects And Aurelian Itself

## Purpose

Evaluate a project, milestone, repository, product surface, research dossier, model route, or Aurelian adoption using evidence-backed scorecards. The skill produces executive summaries, category scores, strengths, weaknesses, risks, fixes, next milestones, trend comparisons, confidence levels, and evidence references.

Use this skill with `../core/16_EVALUATION_ENGINE.md`, `../evaluation/18_PROJECT_SCORECARD.md`, and `../evaluation/19_BENCHMARK_PROTOCOL.md`.

## Trigger

Use this skill when:

1. The user asks for project evaluation, scorecard, benchmark, audit score, quality review, maturity rating, or "how good is this?"
2. A milestone needs an evidence-backed closeout.
3. A project needs a before/after Aurelian comparison.
4. A model, routing strategy, prompt strategy, or agent workflow needs comparison.
5. A research-heavy project needs quality review before implementation.
6. A frontend, SaaS, AI product, library, framework, or greenfield project needs a reusable scorecard.
7. Existing evaluations are stale, inconsistent, unsupported, or missing trend analysis.

## Required Evidence

Minimum evidence depends on scope:

| Scope | Minimum evidence |
|---|---|
| Existing repository | file tree, core docs, package manifests, tests, verification commands, recent commits |
| Greenfield plan | brief, roadmap, architecture proposal, risk list, research plan, evaluation criteria |
| Frontend application | rendered screenshots or recordings, UX flow, accessibility/performance evidence where available |
| SaaS | architecture, auth/data surfaces, reliability and rollback plan, tests, release/deployment evidence |
| AI product | model routes, prompts, evals, safety/quality checks, data handling, user workflow evidence |
| Library/framework | public API, examples, docs, tests, compatibility policy, release/versioning evidence |
| Research-heavy project | source table, claim matrix, contradictions, confidence, implementation decisions |
| Aurelian effectiveness | baseline run, Aurelian run, same task class, scoring rubric, behavioral differences |

If required evidence is unavailable, mark the affected score as lower confidence or `N/A`. Do not compensate with speculation.

## Algorithm

1. **Define the evaluation question.** What decision will the evaluation change?
2. **State scope and non-goals.** Name artifacts, time range, project type, benchmark type, and excluded areas.
3. **Choose scorecard.** Select one scorecard from `../evaluation/18_PROJECT_SCORECARD.md` or compose a hybrid when the project type truly spans categories.
4. **Collect evidence.** Inspect relevant code, docs, tests, screenshots, research, commits, prompts, routes, and prior evaluations.
5. **Run checks when feasible.** Use existing tests, builds, lint, link checks, visual checks, accessibility checks, or benchmark scripts when they are in scope and available.
6. **Score subdimensions.** Assign 0-100, confidence, and evidence for every applicable subdimension.
7. **Compute category and overall scores.** Use declared weights. Do not hide low-confidence scores inside a high-confidence average.
8. **Write findings.** Separate strengths, weaknesses, current risks, immediate fixes, and long-term improvements.
9. **Compare trend.** Use previous reports only when scope, weights, and evidence are comparable. Otherwise say `not comparable`.
10. **Recommend milestones.** Convert the highest-risk gaps into ordered, independently verifiable milestones.
11. **Audit the report.** Remove unsupported claims, list unverified areas, and make evidence references inspectable.

## Scorecard Selection Guide

| Project type | Default scorecard |
|---|---|
| New product or repo plan | Greenfield project |
| Mature or inherited codebase | Existing repository |
| LLM, agent, recommender, or AI-native workflow | AI product |
| Multi-tenant app or hosted product | SaaS |
| User-facing web/app interface | Frontend application |
| Package, SDK, design system, internal framework | Library/framework |
| Scientific, regulated, domain-heavy, or research-first work | Research-heavy project |

When multiple scorecards apply, choose the one that matches the main risk. Add secondary categories only where they change the decision.

## Benchmark Use

Use `../evaluation/19_BENCHMARK_PROTOCOL.md` when comparing:

1. Before vs after Aurelian.
2. Project vs project.
3. Milestone vs milestone.
4. Model vs model.
5. Routing strategy vs routing strategy.

Benchmark reports must include baseline, task distribution, controls, metrics, evidence, confidence, and limitations. Never invent benchmark numbers.

## Output Format

```text
Project Evaluation Report

Evaluation question:
Project/artifact:
Project type:
Scorecard:
Scope:
Non-goals:
Evaluator/model/harness:
Date:

Executive Summary:

Overall Score:
Overall Confidence:

Category Scores:
- Engineering Quality:
- Product Quality:
- Research Quality:
- Execution Quality:
- Model Usage:
- Knowledge Quality:

Strengths:

Weaknesses:

Risks:

Immediate Fixes:

Long-term Improvements:

Recommended Next Milestones:

Trend Compared To Previous Evaluations:

Evidence References:

Unverified Areas:

Benchmark Notes:
- baseline:
- comparison method:
- limitations:
```

## Quality Gates

- The evaluation question is explicit.
- The scorecard matches the project type and risk.
- Every score has evidence and confidence.
- Benchmark comparisons have controlled conditions or state why they are approximate.
- Immediate fixes are actionable without a new strategy phase.
- Long-term improvements are milestone-shaped.
- Trend comparison is based on a comparable prior report or marked unavailable.
- Unsupported claims are removed or downgraded to hypotheses.

## Failure Modes

- Rating a project from README quality alone.
- Giving numeric scores without inspectable evidence.
- Averaging incomparable categories.
- Benchmarking different prompts, repos, tools, or task scopes and presenting the result as causal.
- Treating a lack of tests as a low score without checking whether other verification evidence exists.
- Treating model cost as waste without checking routing need and outcome quality.
- Treating research as complete because many documents exist.
- Hiding missing evidence in a confident executive summary.
