# 13_MODEL_ROUTER -- Allocating Work Across Models and Harnesses

The model router applies the governing theorem at the tool level: **intelligence is the allocation of attention under uncertainty toward the user's objective.** A model is not chosen because it is fashionable; it is chosen because its harness, context window, repo access, research surface, autonomy controls, taste, and verification affordances fit the next decision. Product facts move, so route by observed capability first and by product label second. Verify current tool behavior against the relevant adapter or official docs when it matters.

This file extends `02_COGNITIVE_ARCHITECTURE.md` and `07_DECISION_ENGINE.md`. It does not replace the Constitution, task algorithms, or proof standards.

## 1. Routing inputs

Before assigning work, score the task on these axes:

| Axis | Low | High |
|---|---|---|
| Task type | question, summary, small edit | multi-phase build, migration, architecture, review swarm |
| Token budget | tight context, short answer | large context, many artifacts, long synthesis |
| Repo access needs | no files or read-only snippets | full read/write/test/diff access |
| Research depth | known domain or local docs enough | external sources, source ranking, date checks, controversy |
| Taste/design judgment | mechanical or local convention obvious | UX, architecture, product judgment, naming, tradeoffs |
| Autonomy level | user wants steering | agent can execute milestones independently |
| Risk level | reversible docs or small internal change | data, security, money, production, public contract, irreversible work |
| Verification requirements | explanation only | tests, builds, visual checks, security review, diff audit |

If two axes conflict, route for the scarcest requirement: repo execution beats abstract reasoning; high risk beats speed; required verification beats convenience.

## 2. Tool roles

Use these as defaults, not dogma. The active session's actual tools decide.

| Tool | Best default role | Avoid as primary when |
|---|---|---|
| ChatGPT Web | Broad ideation, research synthesis, taste review, prompt drafting, user-facing explanation, cross-tool orchestration notes. | The task requires direct repo mutation, local command evidence, or precise line-level verification unavailable in the session. |
| Codex | Repository-grounded implementation, debugging, refactoring, tests, diff review, and evidence-grounded completion reports. | The core work is open-ended external research with little repo surface, unless web tools are available and source quality can be verified. |
| Claude Opus | Deep architecture, long-context synthesis, difficult code review, ambiguous design decisions, and high-judgment planning. | The task needs fast small edits or tight iterative shell feedback better handled by a repo-native agent. |
| Claude Sonnet | Balanced coding, planning, review, and cost-aware execution where speed matters and the task is well-scoped. | The task is unusually ambiguous, taste-heavy, or requires maximal deep synthesis. |
| Fable | Narrative synthesis, product/design framing, research-to-roadmap translation, and taste-sensitive articulation. | The task needs direct repo verification or low-level implementation evidence. |
| Cursor | Editor-native feature work, code navigation, targeted refactors, Cloud Agent tasks, and PR review loops in an IDE workflow. | The work requires detached long-running orchestration without clear repo boundaries or when editor context is noisy and untrusted. |
| Antigravity | Agentic IDE exploration, prototype-to-code loops, multi-file workspace work, and visual/product iteration when its project context is active. | The task requires capabilities not exposed in the current Antigravity session or high-assurance verification outside its harness. |
| Future tools | Route by capability: repo access, context, research, autonomy controls, verification, isolation, and handoff quality. | The tool's evidence surface is unknown, unauditable, or cannot satisfy the required proof standard. |

## 3. Routing algorithm

1. **Name the next decision.** Route the next irreversible or high-leverage decision, not the whole project by default.
2. **Identify mandatory affordances.** Does the next step require repo write access, shell execution, web research, visual rendering, secrets, deployment, or user approval?
3. **Eliminate tools that cannot produce the needed evidence.** A tool that cannot run the relevant check may advise, but it cannot be the verifier.
4. **Match judgment profile.** Use deep synthesis tools for ambiguity and taste; use repo-native tools for implementation and proof; use editor tools for local navigation and incremental edits.
5. **Set autonomy.** For reversible low-risk work, allow execution. For destructive, external, credentialed, financial, legal, or public-contract work, require an explicit checkpoint (`07_DECISION_ENGINE.md` section 1).
6. **Assign artifacts.** Every routed task gets an output shape: plan, source table, ontology map, patch, test result, review findings, ADR, traceability update, or handoff note.
7. **Verify before promotion.** Advice becomes an executable plan only after source review; code becomes accepted only after the verification ladder in `08_VERIFICATION_ENGINE.md`.

## 4. Routing matrix

| Work | Primary | Secondary / reviewer | Required evidence |
|---|---|---|---|
| Open-ended product idea | ChatGPT Web, Fable, Claude Opus | Codex for repo feasibility | Decision record or roadmap with assumptions named. |
| Research pipeline generation | ChatGPT Web, Claude Opus, Fable | Codex when repo discovery or file creation is needed | Research suite, document specs, dependency graph, execution order, confidence, and discovery gate. |
| Unknown technical domain | ChatGPT Web, Claude Opus | Codex if repo audit follows | Source ladder, claim table, uncertainty list (`11_DOMAIN_INTELLIGENCE.md`). |
| Existing repo feature | Codex, Cursor, Antigravity | Claude Sonnet/Opus for review when complex | Diff, targeted tests, lint/typecheck/build as applicable. |
| Debugging | Codex, Cursor | Claude Sonnet for hypothesis review | Reproduction, competing hypotheses, fix, exact passing reproduction. |
| Architecture decision | Claude Opus, ChatGPT Web | Codex for codebase constraints | Forces, alternatives, reversibility, ADR if durable. |
| UX/product taste | Fable, ChatGPT Web, Claude Opus | Codex/Cursor for implementation | Visual hierarchy rationale plus rendered/screenshot evidence if UI shipped. |
| High-risk security/data/money work | Codex with repo evidence | Claude Opus/Sonnet or dedicated reviewer | Full verification ladder, security sweep, explicit unresolved risk list. |
| Review swarm | Claude Opus, Codex, Cursor/Bugbot | ChatGPT Web for synthesis | Severity-ordered findings with file/line evidence; no forwarded unverified claims. |
| Documentation and prompts | ChatGPT Web, Fable, Claude Opus | Codex for repo consistency and links | Diff review; command/example verification when present. |

## 5. Token and context policy

1. Put the largest context where it buys the most certainty: architecture synthesis, research synthesis, and cross-file reasoning.
2. Keep execution agents on the files they will edit plus the contracts they must honor (`02_COGNITIVE_ARCHITECTURE.md` section 2).
3. Use summaries only for stable context. Expand around uncertainty, risk, and contracts.
4. When token budget is tight, route narrow implementation to repo-native agents and offload synthesis to a separate prompt with explicit return format.
5. Never let context size substitute for source quality, tests, or diff review.

## 6. Handoff contract

Every cross-tool handoff must include:

1. Objective and "done when" criteria.
2. Current evidence and confidence level.
3. Files, sources, or artifacts inspected.
4. Decisions already made and decisions still open.
5. Constraints and forbidden actions.
6. Verification required before completion can be claimed.
7. Trace IDs or parent/child links from `14_TRACEABILITY_ENGINE.md` when the task produces or changes durable artifacts.
8. Exact output format requested.

Do not hand off vibes. Hand off evidence, constraints, and the next decision.

## 7. Review swarm protocol

Use multiple tools only when independent perspectives reduce risk more than coordination costs.

1. Split by concern: correctness, security, architecture, UX, performance, docs.
2. Give each reviewer the same stated intent and relevant artifacts.
3. Require file/line/source evidence for every finding.
4. Merge findings yourself; deduplicate, rank by severity, and discard unsupported claims.
5. Verify fixes in the repo-native tool. A reviewer can identify risk; only current-session evidence can close it.

## 8. Future-tool admission test

A new tool enters the router only when its adapter or observed session can answer:

1. What durable instruction surface does it load?
2. What files can it read, write, and protect?
3. What commands, tests, browsers, or external tools can it run?
4. How does it expose diffs, logs, screenshots, sources, and failures?
5. What autonomy controls stop destructive or external side effects?
6. How does it preserve or discard memory?
7. What failure mode is it prone to: context noise, over-autonomy, shallow repo access, weak verification, stale product knowledge, or poor handoff?

Until those answers exist, treat the tool as advisory only.
