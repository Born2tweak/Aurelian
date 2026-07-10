# 16_EVALUATION_ENGINE -- Quality, Benchmarking, And System Effectiveness

The evaluation engine teaches Aurelian how to judge project quality and its own effect on engineering work. It turns "better" into evidence-backed scores, risks, fixes, trends, and next milestones. It extends `08_VERIFICATION_ENGINE.md`, `12_SCIENTIFIC_REASONING.md`, `13_MODEL_ROUTER.md`, `../evaluation/17_EVALUATION_PROTOCOL.md`, `../evaluation/18_PROJECT_SCORECARD.md`, and `../evaluation/19_BENCHMARK_PROTOCOL.md`.

Evaluation is not a vibe check. Every score must cite evidence, confidence, and what was not inspected. If evidence is missing, lower confidence or mark the score unavailable. Do not invent benchmark numbers.

## 1. When To Evaluate

Run an evaluation when:

1. Starting an existing repository audit.
2. Closing a milestone.
3. Comparing project state before and after Aurelian.
4. Choosing between model, routing, or prompting strategies.
5. Reviewing a generated project, AI product, frontend surface, SaaS app, library, or research-heavy project.
6. Preparing a roadmap, funding/demo checkpoint, release, handoff, or self-improvement cycle.
7. Recurring failures suggest Aurelian itself may need a rule, skill, prompt, or benchmark update.

## 2. Evaluation Inputs

Gather only the evidence needed for the evaluation scope:

| Evidence class | Examples |
|---|---|
| Repository structure | file tree, package manifests, module boundaries, public APIs, dependency graph |
| Implementation evidence | code, tests, configs, migrations, CI, release scripts, commits |
| Product evidence | screenshots, recordings, flows, accessibility checks, performance traces, bug reports |
| Research evidence | source tables, claim matrices, dated sources, contradiction logs, implementation notes |
| Execution evidence | milestone reports, roadmap, rollback plans, review findings, commit history |
| Model usage evidence | prompts, model routes, token logs, context summaries, handoff packets, eval traces |
| Knowledge evidence | docs, ADRs, architecture notes, resource atlas, stale/orphaned files, trace links |

Use current-session evidence when evaluating live work. Historical reports can inform trends, but they are not proof of the current state unless rechecked.

## 3. Scoring Model

Scores use a 0-100 scale.

| Band | Meaning |
|---|---|
| 90-100 | Excellent. Evidence shows strong quality with only minor improvements. |
| 75-89 | Good. Usable and maintainable, with clear gaps or risks to address. |
| 60-74 | Mixed. Valuable work exists, but important risks or quality gaps remain. |
| 40-59 | Weak. Significant defects, missing evidence, or unstable execution. |
| 0-39 | Critical. Quality cannot be trusted for the evaluated goal. |

Category scores should be averages or weighted averages of visible subdimensions. State the weights when they differ from equal weighting. A score without evidence is invalid.

Use confidence levels from `08_VERIFICATION_ENGINE.md`:

- **High:** directly inspected and verified in the current session.
- **Medium:** inferred from strong local evidence, authoritative docs, or historical artifacts.
- **Low:** based on incomplete evidence, stale artifacts, or unverified reports.

## 4. Required Categories

Evaluate every category that applies. Mark non-applicable categories as `N/A` with a reason.

### Engineering Quality

- Architecture quality.
- Maintainability.
- Modularity.
- Documentation completeness.
- Testing quality.
- Verification coverage.
- Traceability coverage.

### Product Quality

- UX quality.
- UI quality.
- Accessibility.
- Performance.
- Polish.
- Reliability.
- Usability.

### Research Quality

- Completeness.
- Contradictions surfaced.
- Implementation value.
- Confidence.
- Evidence quality.

### Execution Quality

- Milestone accuracy.
- Rollback readiness.
- Documentation freshness.
- Commit quality.
- Review coverage.

### Model Usage

- Token efficiency.
- Routing correctness.
- Unnecessary premium model usage.
- Context efficiency.
- Prompt reuse.

### Knowledge Quality

- Stale documents.
- Orphaned research.
- Undocumented implementation.
- Outdated architecture.
- Missing evidence.

## 5. Evaluation Algorithm

1. **State scope.** Name project, artifact, milestone, comparison, time range, and non-goals.
2. **Select scorecard.** Use the closest scorecard from `../evaluation/18_PROJECT_SCORECARD.md`; adapt weights only when the scope requires it.
3. **Collect evidence.** Inspect files, reports, tests, screenshots, sources, commits, prompts, routes, and logs needed for the scorecard.
4. **Score subdimensions.** Give each subdimension a 0-100 score, confidence level, and evidence reference.
5. **Score categories.** Combine subdimensions into category scores. Explain any weighting.
6. **Score overall.** Combine category scores into an overall score. Exclude `N/A` categories from the denominator.
7. **Identify strengths.** Name the qualities that are evidenced and reusable.
8. **Identify weaknesses and risks.** Separate present defects from future risks.
9. **Prioritize fixes.** Immediate fixes should be small, high-leverage, and evidence-backed. Long-term improvements should become milestones.
10. **Compare trend.** Compare to the previous evaluation only if a previous report exists and the scopes are comparable.
11. **Recommend milestones.** Convert the highest-risk gaps into ordered, verifiable milestones.
12. **Audit honesty.** Remove unsupported claims, downgrade confidence where evidence is thin, and list what was not checked.

## 6. Required Report Shape

Every evaluation report must include:

```text
Evaluation Report

Project/artifact:
Evaluation type:
Scope:
Non-goals:
Evaluator/model/harness:
Date:

Executive Summary:

Overall Score: 0-100
Overall Confidence: high | medium | low

Category Scores:
- Engineering Quality: score, confidence, evidence
- Product Quality: score, confidence, evidence
- Research Quality: score, confidence, evidence
- Execution Quality: score, confidence, evidence
- Model Usage: score, confidence, evidence
- Knowledge Quality: score, confidence, evidence

Strengths:

Weaknesses:

Risks:

Immediate Fixes:

Long-term Improvements:

Recommended Next Milestones:

Trend Compared To Previous Evaluations:
- improved | regressed | unchanged | not comparable | no previous evaluation
- evidence:

Evidence References:
- path, command, screenshot, source, commit, report, or log

Unverified Areas:

Scoring Notes:
- weights, exclusions, assumptions, confidence downgrades
```

## 7. Evidence Reference Rules

Evidence references must be specific enough for another evaluator to inspect:

- Files: path plus section, heading, or line when available.
- Commands: command plus relevant result.
- Screenshots/recordings: path or URL, viewport, state, date.
- Sources: URL/path, date checked, reliability grade, claim supported.
- Commits: hash, branch, and relevant files.
- Model traces: prompt, route decision, model/harness, token/cost evidence if available.

Unsupported opinions can appear only as hypotheses or open questions, not findings.

## 8. Self-Evaluation Of Aurelian

When evaluating Aurelian itself, score:

1. Whether agents read the right files before acting.
2. Whether scope control improved.
3. Whether plans became more risk-aware and verifiable.
4. Whether implementation became more idiomatic and maintainable.
5. Whether verification claims became evidence-grounded.
6. Whether reports became more honest and actionable.
7. Whether model routing reduced waste or improved outcomes.
8. Whether durable knowledge was updated only when it changed future decisions.
9. Whether recurring failures turned into smaller, better rules.
10. Whether the OS added ceremony without improving decisions.

Use `../evaluation/17_EVALUATION_PROTOCOL.md` for direct Aurelian-vs-baseline task comparisons and `../evaluation/19_BENCHMARK_PROTOCOL.md` for benchmark design.

## 9. Failure Modes

- Producing a score because the report template has a score field.
- Comparing projects with different scopes without normalizing the comparison.
- Treating test existence as verification coverage without checking what tests prove.
- Treating attractive UI as product quality without usability, accessibility, and reliability evidence.
- Treating research volume as research quality without source ranking and implementation value.
- Treating premium model usage as quality.
- Penalizing low token use when it caused context starvation, or rewarding high token use when it added no evidence.
- Recording trends when the previous evaluation used different scope or weights.

## 10. Completion Checklist

- Scope and non-goals stated.
- Scorecard selected or adapted with weights.
- Every score has confidence and evidence.
- Missing evidence lowered confidence or marked `N/A`.
- Strengths, weaknesses, risks, immediate fixes, long-term improvements, and next milestones are separated.
- Trend comparison cites a previous comparable report or says none exists.
- No benchmark numbers are invented.
- Unverified areas are explicit.
