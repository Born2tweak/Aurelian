# Install Aurelian In A Project

This guide explains how to apply Aurelian to any project repository. Use it when you want AI coding agents to share one operating standard for context loading, research, planning, execution, verification, and durable project memory.

## When To Install Aurelian

Install Aurelian in a repo when at least one of these is true:

- Multiple AI tools or agents will work in the same codebase.
- The project has meaningful correctness, security, data, money, production, legal, reputation, or public-contract risk.
- The repo lacks reliable project context and agents keep rediscovering the same facts.
- You need a repeatable path from research to implementation.
- You want every agent to read before editing, verify before claiming, and stop before destructive or external actions.

Do not install Aurelian as decorative process. If the repo is tiny, low-risk, and short-lived, use the minimal kernel instead: put the core rules from [core/01_CONSTITUTION.md](core/01_CONSTITUTION.md) in the active agent's durable instructions.

## What To Copy

Copy the scaffold from [templates/aurelian-project/](templates/aurelian-project/) into the root of the target project. Keep only the agent surfaces you use.

| Template path | Copy when | Purpose |
|---|---|---|
| `AGENTS.md` | Using Codex-compatible agents | Root project instructions for Codex. |
| `CLAUDE.md` | Using Claude Code | Root project instructions for Claude. |
| `.cursor/rules/*.mdc` | Using Cursor | Cursor rules for core behavior, execution, review, and UI/taste. |
| `.aurelian/*.md` | Always for standard installs | Durable project state, decisions, evidence, resources, traceability, and taste references. |
| `docs/*.md` | Always for standard installs | Project brief, project bible, design specs, engineering rules, agent context, roadmap, research gaps, and resource atlas. |
| `research/README.md` | When research will inform execution | Home for source-backed research dossiers. |
| `reports/**/README.md` | When milestones, audits, reviews, or learning updates matter | Places for evidence-grounded outputs from repo audit, review, milestone execution, and learning updates. |

For a full install, copy all of:

```text
templates/aurelian-project/AGENTS.md
templates/aurelian-project/CLAUDE.md
templates/aurelian-project/.cursor/rules/
templates/aurelian-project/.aurelian/
templates/aurelian-project/docs/
templates/aurelian-project/research/
templates/aurelian-project/reports/
```

After copying, replace placeholders and `Unknown` values with sourced project facts. Do not invent facts to make the docs look complete; record unknowns in `docs/07_RESEARCH_GAPS.md`.

## Install For Codex

1. Copy `templates/aurelian-project/AGENTS.md` to the target repo root.
2. If the repo already has an `AGENTS.md`, merge the Aurelian kernel into it instead of overwriting local instructions.
3. Keep repo-specific setup, test, lint, build, verification, and forbidden-action rules in the root `AGENTS.md`.
4. Keep detailed project memory in `.aurelian/*` and `docs/*`, not in a giant root instruction file.

Codex should load `AGENTS.md`, inspect the relevant project context, then load the standard Aurelian kernel before substantial work:

```text
core/01_CONSTITUTION.md
core/02_COGNITIVE_ARCHITECTURE.md
core/03_EXECUTION_ENGINE.md
core/07_DECISION_ENGINE.md
core/08_VERIFICATION_ENGINE.md
```

Use [adapters/Codex.md](adapters/Codex.md) when tuning the install for Codex-specific behavior.

## Install For Claude

1. Copy `templates/aurelian-project/CLAUDE.md` to the target repo root.
2. If the repo already has a `CLAUDE.md`, merge the Aurelian kernel and project-context loading rules into the existing file.
3. Keep durable facts in `.aurelian/*` and `docs/*`; keep `CLAUDE.md` focused on behavior, load order, boundaries, and verification.
4. Ask Claude to read `CLAUDE.md` before planning or editing and to state what evidence supports completion claims.

Use the same standard kernel files listed above, plus any task-specific Aurelian files needed for memory, model routing, traceability, research, taste, playbooks, or prompts.

## Install For Cursor

1. Copy `templates/aurelian-project/.cursor/rules/` to the target repo's `.cursor/rules/`.
2. Preserve the `.mdc` frontmatter; Cursor uses it to decide when each rule applies.
3. Keep `aurelian-core.mdc` always applied.
4. Use `aurelian-execution.mdc` for implementation, debugging, refactoring, migration, documentation, and research-to-execution work.
5. Use `aurelian-review.mdc` before final responses, code review, security review, risk review, or accepting generated work.
6. Use `aurelian-ui-taste.mdc` for UI, UX, product experience, architecture taste, naming, and documentation polish.

If Cursor also works alongside Codex or Claude in the repo, install `AGENTS.md` and/or `CLAUDE.md` too so all tools share the same project memory and boundaries.

## Run The Bootstrap Prompt

Use [prompts/00_AURELIAN_BOOTSTRAP_PROMPT.md](prompts/00_AURELIAN_BOOTSTRAP_PROMPT.md) to start a project or restart a tool session with Aurelian.

1. Open the bootstrap prompt.
2. Fill in the bracketed project fields: objective, current context, constraints, scope, done criteria, tools, autonomy level, and risk notes.
3. Paste it into the agent that will perform intake or planning.
4. If the agent has repo access, require it to inspect before detailed planning.
5. If the agent lacks repo access, provide files, links, screenshots, or summaries and require it to label repo claims as unverified.

The first response should state the current objective, highest-risk unknowns, and the files or artifacts it needs to inspect.

## Generate Research Docs

Use the research flow from [playbooks/18_RESEARCH_TO_EXECUTION_OS.md](playbooks/18_RESEARCH_TO_EXECUTION_OS.md) when project decisions depend on unfamiliar domains, external APIs, standards, competitors, regulations, or user behavior.

1. Record open questions in `docs/07_RESEARCH_GAPS.md`.
2. Turn each question into a research prompt with the decision it feeds.
3. Require sources to be ranked by reliability and checked for dates.
4. Store source-backed dossiers in `research/`.
5. Capture claims with source, date, reliability grade, confidence, and the project decision affected.
6. Move accepted stable conclusions into the relevant project docs only after review.

Research output should separate consensus, controversy, stale facts, vendor claims, and unresolved uncertainty.

## Synthesize Project Docs

Fill the `docs/` set after discovery and research. These docs should be concise, sourced where possible, and useful to future agents.

| File | Contents |
|---|---|
| `docs/00_PROJECT_BRIEF.md` | Objective, audience, current state, scope, done criteria, and risks. |
| `docs/01_PROJECT_BIBLE.md` | Durable product and domain truths. |
| `docs/02_TECHNICAL_DESIGN_SPEC.md` | Architecture, stack, constraints, data model, interfaces, and tradeoffs. |
| `docs/03_PRODUCT_EXPERIENCE_BIBLE.md` | User experience, workflows, tone, visual system, and product expectations. |
| `docs/04_ENGINEERING_CONSTITUTION.md` | Repo-specific engineering laws and forbidden changes. |
| `docs/05_AGENT_CONTEXT.md` | What agents should inspect, know, and avoid before acting. |
| `docs/06_IMPLEMENTATION_ROADMAP.md` | Milestones, dependencies, evidence gates, and current status. |
| `docs/07_RESEARCH_GAPS.md` | Unknowns, open questions, and research prompts. |
| `docs/08_RESOURCE_ATLAS.md` | Key files, commands, environments, links, and ownership/resource references. |

Prefer `Unknown` plus a research gap over confident fiction. Every durable fact should change a future decision.

## Run Repo Audit

Run a repo audit before generating a roadmap or making substantial changes.

1. Inspect `.aurelian/*`, `docs/*`, README files, configs, tests, package manifests, entry points, and prior decisions.
2. Search for domain concepts from the research and project docs.
3. Map relevant modules, ownership boundaries, public contracts, data flows, and verification commands.
4. Read deeply anything likely to be edited or used as a contract.
5. Establish baseline checks before changing behavior.
6. Save audit results in `reports/audits/`.

The audit should identify current behavior, likely edit surfaces, risks, missing tests, stale docs, and verification commands with evidence.

## Generate Roadmap

Use the audit and synthesis docs to update `docs/06_IMPLEMENTATION_ROADMAP.md`.

1. Compare desired outcomes against current repo behavior.
2. Classify gaps as missing capability, wrong behavior, stale docs, missing tests, architecture mismatch, security risk, or UX mismatch.
3. Rank milestones by risk retired, dependency order, and user value.
4. Keep each milestone independently verifiable and reversible.
5. Define the evidence gate for each milestone: tests, build, lint, screenshots, review, audit, or manual acceptance.
6. Mark destructive, external, credentialed, financial, legal, or production actions as explicit approval checkpoints.

A roadmap is ready when another agent can start the next milestone without inventing scope or success criteria.

## Start Milestone Execution

Start execution from the first milestone in `docs/06_IMPLEMENTATION_ROADMAP.md`.

1. Restate the milestone objective, scope, risks, and done criteria.
2. Inspect the files and contracts named by the roadmap and audit.
3. Make the smallest coherent change that satisfies the milestone.
4. Verify narrowest-first; widen based on risk.
5. Review the complete diff before reporting.
6. Save milestone evidence in `reports/milestones/` when the work is substantial.
7. Update `.aurelian/evidence-log.md`, `.aurelian/decision-log.md`, `.aurelian/traceability.md`, and the roadmap only when the result changes future work.

Do not silently expand a milestone when discovery reveals a larger problem. Report the larger finding and create a new milestone or approval checkpoint.

## What Not To Do

Aurelian does not grant permission to act outside the repo. Agents must not do any of the following without explicit user approval:

- Push commits or tags.
- Deploy, publish, release, or promote environments.
- Delete branches, data, files, cloud resources, accounts, or external artifacts.
- Spend money, start paid services, upgrade plans, or create billable resources.
- Touch external services, credentials, secrets, production systems, customer data, payment systems, or legal/compliance workflows.
- Broaden scope beyond the requested project objective.

Proceed autonomously only through reversible, in-scope local work. Pause at destructive, external, credentialed, financial, legal, production, or scope-changing boundaries.
