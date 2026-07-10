# 13_PROMPT_LIBRARY -- Copy-Paste Prompts

Ready-to-use prompts. Each is self-contained: paste it into any capable model, fill the `[brackets]`, done. They operationalize the skills of `../skills/05_SKILLS_LIBRARY.md`; the reasoning behind them lives in the core files, deliberately NOT restated here. A good prompt states goal, context, constraints, and "done when" -- these templates bake that shape in.

## Planner

```text
Task: [describe the task].
Read the relevant code first. Then produce a concise plan with: scope (what is
in and out), likely files, ordered steps (each independently verifiable), risks,
verification steps, and "done when" criteria. Ask questions only if the answer
cannot be discovered from the code or docs. Do not edit anything until the plan
is accepted or the work is clearly safe and reversible.
```

## Architect

```text
Design decision needed: [describe the problem and system context].
Name the forces (requirements, constraints, scale, team, existing system).
Propose 2-3 candidate designs. For each: what it optimizes, what it sacrifices,
and how hard it is to reverse. Recommend one, preferring designs that delay
irreversible commitment. Stress-test your recommendation: failure modes, scaling
limits, migration path away from it. Output a decision record: context,
decision, alternatives rejected and why, consequences.
```

## Reviewer

```text
Review this diff: [diff or PR link]. Stated intent: [intent].
Read enough surrounding code to judge contracts, not just the diff. Hunt in
this order: correctness/regressions, security, hidden contract breaks, edge
cases, performance on hot paths, maintainability, style (only where it violates
local convention). Report findings first, ordered by severity
(blocker/major/minor/nit), each with file:line, what breaks, and a concrete
suggestion. Separate "must fix" from "consider". No generic praise; if it
passes, state exactly what you checked.
```

## Debugger

```text
Bug: [symptoms, error output, how observed].
Reproduce the failure first and show the reproduction. Read the failing code
path, not just the failing line. Generate at least two hypotheses and state
what each predicts. Run the cheapest test that discriminates between them.
Isolate the root cause -- explain the mechanism, not just the location -- then
apply the smallest responsible patch. Verify the exact reproduction now passes
and nearby tests still pass. Report: cause, mechanism, fix, evidence, and
anything that remains uncertain. Do not claim "fixed" without showing the
passing result.
```

## Security Reviewer

```text
Security-review this change: [diff/paths].
Identify every trust boundary it touches (user input, network, filesystem,
subprocess, third-party data). Check: authn/authz on changed paths; input
validation and output encoding (SQL/shell/path/template/XSS injection);
secrets in code, logs, or client-visible config; unsanitized arguments to
shell/fs/network calls; new or changed dependencies and loosened settings.
Report only actionable findings with severity, file:line, the concrete risk,
and a suggested fix. If clean, list exactly what you checked.
```

## Performance Reviewer

```text
Performance problem: [symptom, metric, target].
Define the metric precisely (which percentile, what conditions). Measure the
baseline and record it. Profile to find the actual hot path -- do not optimize
by intuition. Estimate the ceiling of any fix before making it. Apply one
change at a time; re-measure under identical conditions; report numbers with
variance, not adjectives. Reject any optimization whose measured gain does not
justify its added complexity.
```

## Research

```text
Question: [the question] -- feeding this decision: [decision].
Rank and consult sources in this order: standards/official docs; peer-reviewed
or canonical texts; maintainer docs; primary practitioner writing; community
Q&A; social/secondary summaries. Inspect primary sources directly; check
dates. Extract claims with source and reliability grade. Surface conflicts
between sources rather than averaging them. Report: answer, sources with
grades and dates, confidence, and what remains uncertain.
```

## Research Pipeline Generator

For the complete standalone version, use [16_RESEARCH_PIPELINE_GENERATOR.md](16_RESEARCH_PIPELINE_GENERATOR.md).

```text
Project: [project idea, repository summary, or both].
Before implementation begins, generate the research pipeline this project needs.
Consider: domain knowledge, technical architecture, frontend, backend, AI/ML,
UX, UI, motion, accessibility, infrastructure, DevOps, testing, security,
product strategy, competitive analysis, legal/privacy, performance, scientific
validation, datasets, APIs, open-source ecosystem, resource atlas, and
build-vs-buy.

For every recommended research document include: filename, category,
specialist, purpose, why it exists, required inputs, expected outputs,
downstream dependencies, implementation importance, confidence, estimated
effort, and whether additional discovery is required first.

Also output: category triage, Research Dependency Graph, Research Execution
Order, discovery gate, and implementation readiness. Do not perform the
research or propose implementation before prerequisite discovery/research is
complete.
```

## Prompt Suite Generator

For the complete standalone version, use [17_PROMPT_SUITE_GENERATOR.md](17_PROMPT_SUITE_GENERATOR.md).

```text
Project or milestone: [project idea, repository state, target artifact,
current milestone, or unresolved problem].
Available models/tools: [ChatGPT Web, Codex, Claude Opus, Claude Sonnet,
Fable, Cursor, Antigravity, future tools, and actual capabilities].
Constraints: [token budget, repo access, browser/research access, autonomy
level, task risk, desired output format, required evidence, approval gates].

Generate a complete, dependency-ordered prompt suite. Include prompts for only
the categories needed to move the work forward: discovery, research planning,
individual research reports, research criticism, contradiction review,
knowledge synthesis, architecture decisions, repository audits, gap analysis,
roadmap creation, milestone execution, testing, debugging, UI/taste review,
security review, performance review, accessibility review, documentation
updates, learning capture, pre-push review, and deployment readiness.

For every prompt include: prompt ID, class (Generation/Analysis/Execution),
purpose, target tool/model, fallback model/tool, required inputs, expected
outputs, upstream artifacts, downstream artifacts, risk level, estimated
context size, token budget, evidence requirements, stop condition, approval
gates, autonomy level, desired output format, traceability IDs, and prompt
body.

Also output: recommended workflow, routing decisions, Prompt Suite Manifest,
complete ordered prompt suite, fallback routing, artifact map, verification
requirements, approval gates, and open risks. Avoid giant prompts, duplicated
instructions, unnecessary full context, premium-model waste, mixed
research-plus-implementation without justification, missing deliverables,
missing evidence standards, and missing stop conditions.
```

## Teacher

```text
Explain [concept] to [audience: e.g., a developer new to this codebase].
Start from what they already know and build one step at a time. Lead with why
it matters, then the core mental model, then one concrete worked example, then
the common mistakes and edge cases. Prefer plain language; introduce each term
of art exactly once, with a definition. End with a short check: two or three
questions the learner should now be able to answer, with the answers.
```

## Designer

```text
Design/implement this UI: [description].
First state the user's primary intent on this surface and what the eye should
see first, second, third. Use the existing design system and components;
extend rather than fork. Build all real states: empty, loading, error,
long-content, and responsive breakpoints. Enforce hierarchy through size,
position, contrast, spacing, and grouping -- motion only where it explains
change. Verify visually: screenshot every state you claim works, including
mobile width. Check keyboard reachability and labels on interactive elements.
```

## Honest Advisor

```text
Stress-test this idea: [idea]. Do not optimize for agreement.
First steelman it: the strongest version and the conditions under which it
wins. Then attack: the most likely failure modes ranked by probability x cost,
the hidden costs (maintenance, migration, opportunity cost), and the
load-bearing assumptions with what evidence would falsify each. End with a
straight verdict -- proceed / proceed with changes / don't -- the single
strongest reason, and what evidence would change your mind.
```

## Tool-Grounded Status Update

```text
Before reporting progress, audit each claim against a tool result from this
session. If a claim is not verified, say it is not verified. If a command
failed, include the relevant failure output verbatim. State what was skipped
and what was not checked. Do not imply completion from intent, and do not end
with a promise of work you can do now -- do it now.
```

## Subagent Delegation

```text
Use a subagent for [bounded task]. It should inspect [paths/sources], answer
[specific questions], cite file paths or URLs for every claim, and return only:
findings, risks, and recommended next actions in [format]. It must not edit
files. If it cannot answer a question from evidence, it must say so rather
than infer.
```

## Durable Instruction Update

```text
The same mistake occurred twice: [mistake]. Write one concise durable rule
covering: the mistake, the correct behavior, and the exact command/file/path
where it applies. Place it at the narrowest scope that covers it (folder <
project < global). Prefer an always-on instruction file for project behavior;
create a skill only if the workflow is multi-step. Keep it under three lines.
```

## Setup / Decomposition

```text
New project/repo: [context and goal].
Before writing code, produce: the goal (outcome, for whom, verified how); which
repo areas matter and which are out of bounds; the install/run/test/lint/build
commands, each confirmed by actually running it; the non-negotiable
architecture rules and conventions found in the code; milestones ordered by
risk, each producing something independently verifiable; and explicit "done"
criteria. Record the durable parts in the project's instruction file.
```
