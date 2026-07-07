# Adapter: OpenAI Codex

How the Aurelian maps onto Codex (CLI, app, cloud, GitHub review). Verify surface details against current Codex docs -- they move.

## Config surface mapping

| OS component | Codex surface |
|---|---|
| `../core/01_CONSTITUTION.md` | `AGENTS.md` at repo root (loaded before work) -- paste the Constitution at the top, then project facts per `../core/04_MEMORY_SYSTEM.md` section 2 |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | Global `AGENTS.md` (user level, e.g. `~/.codex/AGENTS.md`) |
| Folder rules | `AGENTS.md` in subdirectories (layers over the root file) |
| `../skills/05_SKILLS_LIBRARY.md` skills | Codex skills -- one skill per file, keep the Purpose/Trigger header as the description so progressive disclosure works |
| Hooks/enforced behavior | Codex hooks and automations |
| Subagent delegation (`07` section 4) | Codex subagents -- explicitly requested; they cost tokens, so apply the section 4 tree before spawning |
| Reviewer skill | Codex GitHub code review -- repo guidance steers it; keep review standards in `AGENTS.md` |

## Codex-specific notes

- Codex's own best practices already match the elite loop: goal/context/constraints/done-when prompts, plan first when ambiguous, verify, review, update `AGENTS.md` after repeated mistakes. The OS adds the decision trees (`07`) and proof standards (`../core/08_VERIFICATION_ENGINE.md`) Codex docs leave implicit.
- Codex performs measurably better when it can verify its work: always give it reproduction steps, test/lint/precommit commands in `AGENTS.md` (Setup skill, `../skills/05_SKILLS_LIBRARY.md`).
- Concurrent threads/worktrees can conflict on shared files -- apply `07` section 4.3 (serialize or repartition).
- Keep the root `AGENTS.md` within a screenful (`../core/04_MEMORY_SYSTEM.md` section 3); demote detail into skills.
