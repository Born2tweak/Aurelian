# 18_PROJECT_SCORECARD -- Reusable Evaluation Scorecards

This file defines reusable scorecards for evaluating projects with `../core/16_EVALUATION_ENGINE.md` and `../skills/26_PROJECT_EVALUATION_SKILL.md`. Scorecards are templates, not score generators. Every score requires evidence, confidence, and references.

Use a 0-100 scale. Use `N/A` when a category does not apply. Do not invent scores for missing evidence.

## 1. Universal Categories

All scorecards draw from these categories:

| Category | Subdimensions |
|---|---|
| Engineering Quality | architecture quality, maintainability, modularity, documentation completeness, testing quality, verification coverage, traceability coverage |
| Product Quality | UX quality, UI quality, accessibility, performance, polish, reliability, usability |
| Research Quality | completeness, contradictions, implementation value, confidence, evidence quality |
| Execution Quality | milestone accuracy, rollback readiness, documentation freshness, commit quality, review coverage |
| Model Usage | token efficiency, routing correctness, unnecessary premium model usage, context efficiency, prompt reuse |
| Knowledge Quality | stale documents, orphaned research, undocumented implementation, outdated architecture, missing evidence |

## 2. Subdimension Scoring Anchors

Use these anchors for every subdimension:

| Score | Anchor |
|---|---|
| 0-20 | Missing, misleading, broken, or unsupported by evidence. |
| 21-40 | Present but weak, stale, partial, or risky. |
| 41-60 | Adequate in places, with material gaps. |
| 61-80 | Solid and useful, with known improvements. |
| 81-100 | Strong, current, verified, and maintainable for the evaluated scope. |

Confidence is separate from score. A promising area with thin evidence may score medium-high but confidence must be low or medium.

## 3. Greenfield Project Scorecard

Use for a new repository, product plan, or implementation roadmap before substantial code exists.

| Category | Default weight | Evaluate |
|---|---:|---|
| Engineering Quality | 20 | architecture plan, modularity plan, verification strategy, technical risk handling |
| Product Quality | 20 | UX flow, UI direction, accessibility plan, performance targets, reliability expectations |
| Research Quality | 20 | domain/resource/technical research completeness, contradictions, implementation value |
| Execution Quality | 20 | milestone plan, rollback strategy, review gates, documentation plan |
| Model Usage | 10 | planned routing, context strategy, prompt reuse, cost awareness |
| Knowledge Quality | 10 | project docs, ADR plan, evidence references, research-to-implementation links |

Strong evidence includes project brief, architecture proposal, research pipeline, risk register, roadmap, and verification plan.

## 4. Existing Repository Scorecard

Use for inherited or active codebases.

| Category | Default weight | Evaluate |
|---|---:|---|
| Engineering Quality | 30 | current architecture, maintainability, modularity, test quality, verification coverage |
| Product Quality | 15 | user-facing behavior, reliability, performance, accessibility, UX/UI where applicable |
| Research Quality | 10 | domain/resource research behind current decisions |
| Execution Quality | 15 | commit quality, milestone accuracy, rollback readiness, review coverage |
| Model Usage | 10 | routes, prompts, context usage, unnecessary premium model use during recent work |
| Knowledge Quality | 20 | docs freshness, architecture accuracy, traceability, stale/orphaned docs, missing evidence |

Strong evidence includes file tree, package manifests, tests, CI, docs, ADRs, recent commits, reports, and known issue history.

## 5. AI Product Scorecard

Use for LLM, agentic, recommender, generation, retrieval, or AI-native workflow products.

| Category | Default weight | Evaluate |
|---|---:|---|
| Engineering Quality | 20 | architecture, isolation, observability, testability, modular AI boundaries |
| Product Quality | 20 | user workflow, reliability, latency, transparency, recoverability, accessibility |
| Research Quality | 15 | model/task research, eval design, safety evidence, dataset/source quality |
| Execution Quality | 15 | eval gates, rollback readiness, review coverage, incident and release practice |
| Model Usage | 20 | routing correctness, token efficiency, prompt reuse, context efficiency, premium-model discipline |
| Knowledge Quality | 10 | prompt docs, model decisions, eval evidence, stale assumptions, undocumented behavior |

Strong evidence includes prompts, evals, model routes, cost/token traces, failure examples, safety notes, UX flows, and release checks.

## 6. SaaS Scorecard

Use for hosted multi-user products, business apps, internal platforms, and subscription services.

| Category | Default weight | Evaluate |
|---|---:|---|
| Engineering Quality | 25 | service boundaries, data model, auth/authz, maintainability, tests |
| Product Quality | 25 | primary workflows, reliability, performance, accessibility, polish, usability |
| Research Quality | 10 | market/user/domain evidence, integration research, compliance assumptions |
| Execution Quality | 20 | deployments, rollback, migrations, commits, reviews, milestone accuracy |
| Model Usage | 5 | routing and context discipline where AI-assisted work is used |
| Knowledge Quality | 15 | operational docs, ADRs, runbooks, stale docs, traceability |

Strong evidence includes architecture docs, auth/data flows, tests, CI/CD, deployment notes, rollback plans, screenshots, analytics or user evidence when available.

## 7. Frontend Application Scorecard

Use for web apps, dashboards, product surfaces, editors, design systems, and interactive interfaces.

| Category | Default weight | Evaluate |
|---|---:|---|
| Engineering Quality | 20 | component architecture, state boundaries, maintainability, testability |
| Product Quality | 40 | UX, UI, accessibility, performance, polish, responsiveness, reliability, usability |
| Research Quality | 10 | UX/UI/resource research, design references, accessibility standards |
| Execution Quality | 10 | review coverage, visual verification, milestone accuracy, docs freshness |
| Model Usage | 5 | prompt/model efficiency for generated UI or design automation |
| Knowledge Quality | 15 | product bible, design tokens, component docs, stale screenshots, undocumented behavior |

Strong evidence includes screenshots, recordings, accessibility scans, performance traces, component docs, visual tests, and UX task flows.

## 8. Library / Framework Scorecard

Use for packages, SDKs, reusable modules, internal frameworks, design systems, and public APIs.

| Category | Default weight | Evaluate |
|---|---:|---|
| Engineering Quality | 40 | API design, modularity, compatibility, maintainability, tests, examples |
| Product Quality | 10 | developer experience, usability, reliability, performance |
| Research Quality | 10 | ecosystem comparison, standards, compatibility research |
| Execution Quality | 15 | versioning, release notes, commit quality, review coverage, rollback/deprecation plan |
| Model Usage | 5 | routing/prompt discipline when AI supports development |
| Knowledge Quality | 20 | API docs, examples, ADRs, migration guides, traceability, stale docs |

Strong evidence includes public API docs, examples, tests, changelog, compatibility matrix, versioning policy, issue history, and release process.

## 9. Research-Heavy Project Scorecard

Use for projects where correctness depends on domain research, scientific evidence, standards, competitive analysis, legal/privacy constraints, or unfamiliar ecosystems.

| Category | Default weight | Evaluate |
|---|---:|---|
| Engineering Quality | 15 | architecture response to research constraints, testability, traceability into code |
| Product Quality | 10 | user impact and usability implied by research-backed decisions |
| Research Quality | 35 | completeness, contradictions, implementation value, confidence, evidence quality |
| Execution Quality | 15 | research-to-roadmap conversion, milestone accuracy, review coverage |
| Model Usage | 10 | research routing, context efficiency, prompt reuse, unnecessary premium model use |
| Knowledge Quality | 15 | orphaned research, stale sources, missing evidence, undocumented implementation |

Strong evidence includes source tables, claim matrices, contradiction logs, dated source checks, implementation decision links, and research review notes.

## 10. Report Matrix

Use this compact matrix inside reports when useful:

```text
Category | Weight | Score | Confidence | Key evidence | Main gap
Engineering Quality | | | | |
Product Quality | | | | |
Research Quality | | | | |
Execution Quality | | | | |
Model Usage | | | | |
Knowledge Quality | | | | |
```

## 11. Trend Rules

Trend can be reported only when:

1. A prior evaluation exists.
2. Scope and scorecard are comparable.
3. Evidence references are available for both evaluations.
4. Weight changes are stated.

If those conditions fail, write `not comparable` or `no previous evaluation`.

## 12. Scorecard Adaptation Rules

Adapt weights only when:

1. The project type has a clearly different risk profile.
2. The evaluation question requires emphasis on a subset of categories.
3. The adapted weights are declared before scoring.
4. The report explains why the default scorecard was not sufficient.

Do not adapt weights after seeing the scores.
