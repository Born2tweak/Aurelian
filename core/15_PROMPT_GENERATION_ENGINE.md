# 15_PROMPT_GENERATION_ENGINE -- Generating Tool-Aware Prompt Suites

This engine turns an objective, repository state, milestone, target artifact, or unresolved problem into the smallest complete prompt suite needed to move work forward. It extends `13_MODEL_ROUTER.md`, `14_TRACEABILITY_ENGINE.md`, `02_COGNITIVE_ARCHITECTURE.md`, `07_DECISION_ENGINE.md`, and `08_VERIFICATION_ENGINE.md`: route by tool capability, preserve traceability, compress stable context, preserve uncertainty, and require evidence before completion claims.

Prompt generation is not prompt decoration. A generated prompt is a work order with inputs, outputs, evidence standards, stop conditions, and handoff contracts.

## 1. Inputs

Before generating prompts, collect only the context needed to route and sequence the work:

| Input | Required content |
|---|---|
| Objective | Project idea, milestone, target artifact, repo gap, failing behavior, or decision needed. |
| Current state | Repository summary, relevant docs, open tasks, known evidence, current blockers, and prior decisions. |
| Available tools | ChatGPT Web, Codex, Claude Opus, Claude Sonnet, Fable, Cursor, Antigravity, future tools, or local equivalents. |
| Capabilities | Repo read/write, shell/tests, browser/research, design tools, screenshots, deployment, external services, subagents. |
| Constraints | Token budget, time budget, autonomy level, risk level, forbidden actions, required approvals, output format. |
| Traceability | Existing IDs for requirements, research reports, ADRs, decisions, issues, milestones, commits, tests, and evidence logs. |

If inputs are too thin to produce a reliable suite, generate a discovery prompt first instead of inventing context.

## 2. Prompt Classes

Every prompt belongs to exactly one class.

| Class | Creates or changes | Use for |
|---|---|---|
| Generation Prompts | New artifacts. | Discovery notes, research plans, research reports, synthesis memos, ADR drafts, roadmaps, docs, prompt manifests. |
| Analysis Prompts | Judgments about existing artifacts. | Criticism, contradiction review, repo audits, gap analysis, UI/taste review, security review, performance review, accessibility review, pre-push review. |
| Execution Prompts | Repository or milestone action. | Code edits, tests, debugging, milestone execution, documentation updates, commits, deployment readiness checks. |

Do not ask one agent to research and implement in the same prompt unless the task is low-risk, the sources are already supplied, and the prompt explains why combining the phases is cheaper than splitting them.

## 3. Prompt Categories

Consider these categories, then include only those needed for the objective:

- discovery
- research planning
- individual research reports
- research criticism
- contradiction review
- knowledge synthesis
- architecture decisions
- repository audits
- gap analysis
- roadmap creation
- milestone execution
- testing
- debugging
- UI/taste review
- security review
- performance review
- accessibility review
- documentation updates
- learning capture
- pre-push review
- deployment readiness

Every selected category must feed a downstream decision or artifact. Skipped high-risk categories need a reason.

## 4. Required Prompt Metadata

Every generated prompt must include:

```text
Prompt ID:
Prompt class: Generation | Analysis | Execution
Purpose:
Target tool/model:
Fallback model/tool:
Required inputs:
Expected outputs:
Upstream artifacts:
Downstream artifacts:
Risk level: low | medium | high | critical
Estimated context size: small | medium | large | extra-large
Token budget:
Evidence requirements:
Stop condition:
Human approval required before:
Autonomy level:
Desired output format:
Traceability IDs:
```

Metadata is part of the prompt, not an afterthought. A prompt without an explicit deliverable, evidence requirement, and stop condition is invalid.

## 5. Routing Model

Use `13_MODEL_ROUTER.md` to create model-specific variants without changing project truth.

| Target | Default prompt variant |
|---|---|
| ChatGPT Web | Research synthesis, broad prompt suite generation, architecture alternatives, taste critique, artifact maps, and handoff notes. Mark repo claims unverified unless files/commands are supplied by the session. |
| Codex | Repo-grounded execution, audits, debugging, tests, diffs, documentation updates, prompt registry edits, pre-push review, and evidence-grounded completion reports. |
| Claude Opus | Deep architecture, large-context synthesis, difficult contradiction review, high-risk roadmap generation, and complex review prompts. |
| Claude Sonnet | Balanced planning, coding, review, and cost-aware execution where the scope and evidence standards are clear. |
| Fable | Narrative synthesis, product/design framing, research-to-roadmap translation, and taste-sensitive prompt language. |
| Cursor | Editor-native implementation, targeted refactors, repo audits, IDE review loops, and milestone execution with local context. |
| Antigravity | Agentic IDE exploration, prototype-to-code loops, visual/product iteration, and multi-file workspace execution when active project context is available. |
| Future tools | Route by observed capability: context, repo access, command evidence, browser/research surface, autonomy controls, review quality, and handoff clarity. |

If the best reasoning model lacks repo access, route it to produce a plan or analysis artifact, then hand off execution to a repo-native tool. If the repo-native tool lacks browser access, give it sourced summaries and require it to mark external claims as supplied, not independently verified.

## 6. Context Selection

Use the smallest sufficient context.

1. Include full text for files the agent must edit, verify, or critique line-by-line.
2. Include summaries for stable background that has already been verified.
3. Reference canonical documents instead of repeating them when the target tool can access them.
4. Expand context around uncertainty, public contracts, security/data/money boundaries, and task-specific invariants.
5. Do not send full repository trees, long research dossiers, or entire conversations when a manifest and artifact map are sufficient.
6. Preserve traceability IDs exactly; do not rename requirements, reports, ADRs, tests, issues, or milestones unless the prompt asks for an ID migration.

Token efficiency is a correctness concern: context overload makes prompts less reliable.

## 7. Suite Generation Algorithm

1. **State the objective.** Name the user outcome, target artifact, current milestone, or unresolved problem.
2. **Inventory available evidence.** List repo docs, research reports, ADRs, tests, designs, logs, and current tool capabilities.
3. **Classify risk.** Identify correctness, security, data, money, legal, production, accessibility, performance, reputation, and irreversible-action risk.
4. **Choose categories.** Select the prompt categories needed to retire uncertainty and produce the target artifact.
5. **Split by dependency.** Discovery precedes research; research precedes synthesis; synthesis precedes architecture; audit precedes gap analysis; gap analysis precedes roadmap; roadmap precedes execution; execution precedes review and readiness checks.
6. **Assign prompt class.** Generation, Analysis, or Execution.
7. **Route each prompt.** Pick target and fallback tools using the routing model, mandatory affordances, token budget, and risk.
8. **Define metadata.** Fill every required metadata field.
9. **Write prompt bodies.** Keep each body focused on one deliverable. Reference canonical docs rather than duplicating them.
10. **Add approval gates.** Mark destructive, external, credentialed, financial, legal, public-contract, push, deploy, delete, purchase, and dependency-addition actions.
11. **Emit the manifest.** Record dependency graph, order, required context, token notes, approval gates, artifacts, and status.
12. **Self-critique.** Check the suite against the failure modes in section 11 before returning it.

## 8. Standard Prompt Suite Manifest

Every generated suite must include this manifest:

```text
Prompt Suite Manifest

Project or milestone objective:

Prompt dependency graph:

Execution order:

Prompts:
- Prompt ID:
  Assigned model/tool:
  Prompt class:
  Expected artifact:
  Required context:
  Token-efficiency notes:
  Approval gates:
  Completion status: not started | in progress | blocked | complete | superseded

Artifact map:
- Upstream artifacts:
- Generated artifacts:
- Downstream artifacts:

Verification requirements:

Fallback routing:

Open risks:
```

## 9. Evidence and Stop Conditions

Every prompt must state what counts as enough evidence.

| Work type | Minimum evidence |
|---|---|
| Research report | Sources ranked by reliability, dates checked, claims mapped to decisions, uncertainty and conflicts surfaced. |
| Research criticism | Accepted/rejected claims, missing sources, stale facts, contradictions, and readiness verdict. |
| Synthesis | Inputs listed, stable conclusions separated from uncertainty, implementation constraints named. |
| Architecture decision | Forces, alternatives, reversibility, recommendation, consequences, and ADR-ready output. |
| Repo audit | Paths inspected, contracts found, baseline checks identified, unknowns named. |
| Execution | Diff, commands/tests/builds/logs as applicable, and self-review against the changed surface. |
| UI/taste | Screenshots or render evidence for shipped UI claims, plus hierarchy/accessibility notes. |
| Security/performance/accessibility | Findings grounded in file/line/source evidence and required checks or measurements. |
| Deployment readiness | Build/test status, environment/config checks, rollback notes, and approval gates. |

Stop conditions must be explicit: completion, insufficient input, failed evidence gate, user approval required, tool missing, contradiction found, or scope changed.

## 10. Revision Loop For Failed Prompts

When a prompt fails, revise from evidence rather than taste:

1. Record the failure: missing context, wrong route, unclear deliverable, overloaded scope, weak evidence standard, absent approval gate, tool limitation, or ambiguous stop condition.
2. Identify the smallest prompt change that would have prevented the failure.
3. Preserve project truth and traceability IDs while changing wording, context, route, or split.
4. If a prompt was too large, split it by dependency and pass only summaries downstream.
5. If a prompt used an expensive model for repetitive low-risk work, reroute the repetition and reserve the premium model for synthesis or review.
6. Update the suite manifest status and token-efficiency notes.

## 11. Failure Modes

Avoid:

- giant unfocused prompts
- duplicated instructions copied into every prompt
- sending full context when summaries are sufficient
- using premium models for repetitive low-risk work
- asking agents to research and implement simultaneously without justification
- prompts with no explicit deliverable
- prompts with no evidence standard
- prompts with no stopping condition
- model-specific variants that change project truth
- losing traceability IDs between upstream and downstream artifacts
- omitting approval gates for destructive, external, credentialed, financial, legal, public-contract, push, deploy, delete, purchase, or dependency-addition actions

## 12. Output Contract

A prompt-generation run returns:

1. Recommended workflow.
2. Routing decisions and fallbacks.
3. Complete ordered prompt suite.
4. Prompt Suite Manifest.
5. Artifact map.
6. Token-efficiency notes.
7. Approval gates.
8. Verification requirements.
9. Open risks and stop conditions.

The suite is complete only when every prompt has metadata, a single deliverable, evidence requirements, a stop condition, and a downstream place to land.
