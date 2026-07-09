# Adapter: Antigravity

How Aurelian maps onto Antigravity (agentic IDE/workspace harness). Verify surface details against current Antigravity docs or the active session; route by actual repo, command, browser, and diff capabilities.

## Config surface mapping

| OS component | Antigravity surface |
|---|---|
| `../core/01_CONSTITUTION.md` | Project instructions or repo instruction file, preferably the template `AGENTS.md` plus any Antigravity-specific project rules |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | User/global instructions if available; keep team-durable rules versioned in the repo |
| Project state | `../templates/aurelian-project/.aurelian/*` and `../templates/aurelian-project/docs/*` |
| Model routing (`../core/13_MODEL_ROUTER.md`) | Use for agentic IDE exploration, prototype-to-code loops, multi-file workspace work, and visual/product iteration when its project context is active |
| Research-to-execution (`../playbooks/18_RESEARCH_TO_EXECUTION_OS.md`) | Repo audit, gap analysis, milestone execution, review preparation, and learning updates after research artifacts exist |
| Verification (`../core/08_VERIFICATION_ENGINE.md`) | Terminal output, tests, builds, browser/screenshots when available, and diff review inside the active workspace |
| Handoff contract (`../core/13_MODEL_ROUTER.md` section 6) | Accept or emit milestone briefs with objective, inspected files, constraints, forbidden actions, evidence, and required checks |

## Antigravity-specific notes

- Best role: workspace-native exploration, prototype-to-code iteration, small-to-large multi-file edits, visual/product loops, and turning an accepted roadmap into repo changes with visible evidence.
- Use Antigravity for execution after the Research-to-Execution OS has produced enough context to avoid fluent guessing: project brief, relevant research, repo audit, and milestone roadmap when the work is material.
- Treat the Aurelian project template as the durable project surface: `AGENTS.md` for cross-tool loading, `docs/06_IMPLEMENTATION_ROADMAP.md` for evidence-gated milestone execution, `docs/03_PRODUCT_EXPERIENCE_BIBLE.md` and `.aurelian/taste-reference.md` for UI/taste work, and `.aurelian/evidence-log.md` for durable proof notes when useful.
- Avoid using Antigravity as the primary verifier for claims it cannot observe. If the active harness cannot run the relevant test, inspect the rendered UI, or show the diff, downgrade the claim and hand off to a tool that can.
- Apply Constitution Art. V strictly: require manual approval before push, deploy, delete, external service actions, credential use, purchases, or dependency additions.
- Before claiming completion, run the narrowest meaningful checks, review the actual diff, and report what remains unverified.
