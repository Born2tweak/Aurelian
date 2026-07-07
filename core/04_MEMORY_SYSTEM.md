# 04_MEMORY_SYSTEM -- Durable Knowledge Policy

Governs every file that outlives a session: instruction files (AGENTS.md, CLAUDE.md, rules), skills, ADRs, playbooks, and auto-memories. One test decides everything: **store only what changes a future decision.** More memory is not more intelligence; the leverage point is a better feedback loop, not a bigger pile of facts. (Session-scoped working memory is covered in `02_COGNITIVE_ARCHITECTURE.md` section 3; tool-specific file names/locations in `../adapters/`.)

## 1. The instruction-scope hierarchy

Durable instructions layer by scope; narrower scope wins on conflict:

1. **Global (user/machine level)** -- preferences and rules true across all projects: tone, safety posture, personal conventions. Keep tiny; everything here taxes every session.
2. **Project (repo root)** -- the standing orders for one codebase: layout, install/run/test/lint/build commands, architecture rules, forbidden files, done criteria, conventions.
3. **Folder (subdirectory)** -- overrides for one area of a monorepo or an unusual module: local conventions, local test commands, "this directory is generated -- do not edit."

Load order: global first, then project, then folder -- the model should treat each narrower layer as a refinement, not a contradiction, unless it explicitly overrides.

## 2. What goes where

| Knowledge type | Home | Why |
|---|---|---|
| Always-relevant project facts & constraints | Project instruction file (AGENTS.md / CLAUDE.md / rules) | Loaded before every task |
| Multi-step repeatable workflow (>3 steps, recurs) | Skill (`../skills/05_SKILLS_LIBRARY.md` format) | Progressive disclosure: name+description always visible, body loaded only when relevant |
| One significant design decision | ADR (see section 4) | Future maintainers need context, decision, consequences |
| End-to-end workflow for a project class | Playbook (`../playbooks/06_PLAYBOOKS.md` style) | Composes skills and algorithms |
| Behavior that must happen **every** time | Hook / automation (tool-dependent) | Deterministic enforcement beats advisory text |
| Personal, workspace-local observations | Auto-memory (if the tool has one) | Useful, but NOT a substitute: team-shared durable knowledge must live in versioned files, not private memory |

## 3. Create / update / delete / compress

**Create or update when:**
- The same mistake occurred twice (Constitution Art. X). Write the *smallest* durable rule: the mistake, the correct behavior, and the exact command/file/path where it applies.
- A verification command, setup step, or architecture boundary was discovered the hard way.
- Review feedback recurs across tasks.
- A workflow met the skill threshold: >3 steps, recurs across tasks, needs judgment or templates, and forgetting a step has real cost.

**Do NOT store:**
- One-off task noise or temporary debugging guesses.
- Secrets or credentials -- never, in any durable file.
- Broad personality/vibe rules that don't change behavior ("be careful", "write clean code").
- Rules that conflict with the repo's actual observed practice.
- Product facts that rot (versions, pricing, availability) -- store the *check* ("verify against current docs") not the fact.

**Delete or compress when:**
- A rule is stale (the command changed, the constraint lifted) -- delete on sight; a wrong rule is worse than none.
- A rule hasn't fired in recent memory of the project -- candidate for pruning.
- The project file exceeds roughly a screenful of always-loaded text -- compress: merge overlapping rules, demote rarely-needed detail into a skill or linked doc, keep one-line summaries at top level.

**Update loop** (from repeated failure to permanent improvement):

1. Identify the repeated failure.
2. Find the missing trigger or decision point that would have prevented it.
3. Write the smallest durable rule at the narrowest sufficient scope (folder < project < global).
4. Add a checklist item, test, or hook if the behavior can be enforced deterministically.
5. Create a skill only if the workflow is multi-step.
6. Watch it fire on the next similar task; prune if it stays silent or misfires.

## 4. ADR format (one decision, one file)

```
# ADR-NNN: <decision title>
Status: proposed | accepted | superseded by ADR-MMM
Context: the forces and constraints that made this decision necessary.
Decision: what we chose, stated as a rule.
Alternatives: what we rejected and why.
Consequences: what becomes easier, what becomes harder, what to revisit and when.
```

Write an ADR when a decision is expensive to reverse, non-obvious, or likely to be questioned later. Do not write ADRs for choices any competent maintainer would make the same way.

## 5. Quality bar for any durable rule

Before committing a rule, it must pass all four:

1. **Specific** -- names a command, path, pattern, or trigger; not a vibe.
2. **Actionable** -- a model reading it knows exactly what to do differently.
3. **Scoped** -- placed at the narrowest level where it applies.
4. **Cheap** -- short enough that its context cost is below its error-prevention value.
