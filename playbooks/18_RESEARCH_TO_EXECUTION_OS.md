# 18_RESEARCH_TO_EXECUTION_OS -- From Unknown Domain to Verified Change

This playbook turns research into execution without letting either side dominate. Research without implementation becomes theater; implementation without research becomes fluent guessing. The workflow composes `11_DOMAIN_INTELLIGENCE.md`, `12_SCIENTIFIC_REASONING.md`, `03_EXECUTION_ENGINE.md`, `07_DECISION_ENGINE.md`, `08_VERIFICATION_ENGINE.md`, `13_MODEL_ROUTER.md`, `14_TRACEABILITY_ENGINE.md`, and `../skills/23_RESEARCH_PIPELINE_GENERATOR.md`.

Use it when a project begins with material uncertainty: unfamiliar domain, new market, ambiguous product requirements, high-risk architecture, or a codebase whose behavior is not yet trusted.

## 1. Intake

1. State the user's objective, audience, constraints, and "done when" criteria.
2. Separate outcomes from proposed solutions.
3. Identify boundaries: in scope, out of scope, destructive/external actions requiring approval.
4. Classify risk: correctness, security, data, money, legal, production, public contract, reputation.
5. Choose the initial tool route (`../core/13_MODEL_ROUTER.md`) and evidence standard (`../core/08_VERIFICATION_ENGINE.md`).

Output: one-page task brief with assumptions, risks, and initial route.

## 2. Discovery

1. Inspect the repository, product artifacts, existing docs, issue trackers, and prior decisions.
2. Build a vocabulary list: domain terms, repo terms, synonyms, forbidden confusions.
3. Find constraints already encoded in code, tests, configs, ADRs, and docs.
4. Identify missing evidence: what cannot be known from local context.
5. Decide whether domain knowledge is load-bearing (`../core/11_DOMAIN_INTELLIGENCE.md` section 2).

Output: discovery notes with source paths and open questions.

## 3. Research Pipeline and Prompt Generation

1. Use `../skills/23_RESEARCH_PIPELINE_GENERATOR.md` to determine which research categories are needed, which reports should exist, their specialists, dependencies, confidence, implementation impact, estimated effort, and execution order.
2. Add `docs/research/00_PROJECT_DISCOVERY.md` first when repository/product discovery is not sufficient to scope the research suite.
3. Convert each recommended report into research prompts with the decision each answer feeds.
4. Demand source ranking, dates, conflict surfacing, and confidence labels.
5. Define the required artifact: claim table, ontology map, competitor scan, standard summary, API comparison, threat model, resource atlas, build-vs-buy matrix, or risk memo.
6. Set boundaries: no implementation advice without sources; no low-reliability claim promoted to fact.
7. Route prompts to the best research/synthesis tool using `../core/13_MODEL_ROUTER.md`.

Output: research pipeline, dependency graph, execution order, and executable research prompts with return formats.

## 4. Research Execution

1. Consult sources by reliability ladder: standards/official docs, canonical texts, maintainer docs, practitioner writing, community, social.
2. Inspect primary sources directly; avoid summaries of summaries.
3. Extract claims with source, date, reliability grade, and the decision they affect.
4. Separate consensus, controversy, stale facts, and vendor opinion.
5. Record uncertainty as a first-class output, not a footnote.

Output: source-backed research dossier.

## 5. Research Quality Review

1. Check that every important claim has a source and date.
2. Challenge the strongest assumptions: what observation would falsify them?
3. Look for missing higher-rung sources and conflicts between sources.
4. Downgrade claims based on weak or stale evidence.
5. Decide whether the dossier is sufficient for planning or needs another research pass.

Output: quality review with accepted claims, rejected claims, and unresolved uncertainty.

## 6. Knowledge Synthesis

1. Build the working model: entities, relationships, processes, invariants, failure modes, units, authorities.
2. Translate research into engineering constraints and product decisions.
3. Identify what belongs in durable memory, ADRs, prompts, tests, or code comments.
4. Compress stable context; keep uncertain and risky context expanded.
5. State readiness to execute using `../core/11_DOMAIN_INTELLIGENCE.md` section 5.

Output: synthesis memo plus any proposed durable artifacts.

## 7. Repository Audit

1. Search for the domain concepts in code, tests, docs, configs, and data models.
2. Map relevant modules, ownership boundaries, public contracts, and verification commands.
3. Identify existing behavior that matches, conflicts with, or ignores the synthesized model.
4. Read deeply anything that will be edited or defines a contract; read shallowly for structure elsewhere.
5. Establish baseline checks before changing behavior.

Output: repo audit map with likely edit surfaces and baseline evidence.

## 8. Gap Analysis

1. Compare the desired model against current repo behavior.
2. Classify gaps: missing capability, wrong behavior, stale docs, test coverage, architecture mismatch, security risk, UX mismatch.
3. Rank by risk, dependency order, and user value.
4. Identify reversible first moves and irreversible checkpoints.
5. Convert each gap into a verifiable milestone or explicit non-goal.

Output: ranked gap list with evidence and verification method per gap.

## 9. Adaptive Roadmap

1. Order milestones by risk retired, not by apparent ease.
2. Build a walking skeleton when integration risk exists.
3. Keep each milestone independently reviewable and revertible.
4. Assign tool routes per milestone: research, execution, review, verification.
5. Define checkpoint criteria: what evidence allows the next phase to begin.

Output: roadmap with milestones, owners/tools, risks, and evidence gates.

## 10. Milestone Execution

1. For each milestone, run the relevant `../core/03_EXECUTION_ENGINE.md` algorithm.
2. Make the smallest coherent change matching local patterns.
3. Verify narrowest-first as soon as the change is coherent.
4. Update the roadmap when evidence changes assumptions.
5. Stop at true boundaries: destructive, external, credentialed, financial, legal, or scope-changing actions.

Output: patch, test/build/log evidence, and updated milestone status.

## 11. Review Swarm

1. Split review by concern: correctness, security, architecture, UX, performance, docs.
2. Use `../core/13_MODEL_ROUTER.md` to assign independent reviewers only where their perspective reduces risk.
3. Require findings with file/line/source evidence and severity.
4. Merge and deduplicate findings; do not forward unsupported claims.
5. Verify fixes in the repo-native execution environment before closing the milestone.

Output: severity-ranked review findings, fix evidence, and residual-risk list.

## 12. Learning Update

1. Capture only durable lessons that change future decisions (`../core/04_MEMORY_SYSTEM.md`).
2. Update project instructions, ADRs, playbooks, prompts, or tests at the narrowest sufficient scope.
3. Delete or revise stale assumptions discovered during execution.
4. Report what was verified, what was not, and what should be researched or executed next.
5. Feed recurring misses into the smallest durable rule or checklist.
6. Update traceability links from research, decisions, specs, milestones, source files, tests, evidence, review, and lessons when the chain changes.

Output: evidence-grounded closeout and recommended next milestone.

## Completion checklist

- Objective, scope, and risk were stated.
- Research pipeline, dependency graph, and execution order were generated before individual reports were executed.
- Research claims were source-ranked and date-checked.
- Synthesis produced engineering constraints, not just prose.
- Repository audit read the edit surface and contracts.
- Roadmap milestones were independently verifiable.
- Each executed milestone has current-session evidence.
- Review findings were evidence-grounded and ranked.
- Durable lessons were captured only when they change future decisions.
- Traceability links connect research, decisions, specs, milestones, source files, tests, evidence, review, lessons, and updated research where those artifacts exist.
