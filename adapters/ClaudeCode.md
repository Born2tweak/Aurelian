# Adapter: Claude Code

How the Aurelian maps onto Claude Code (CLI/IDE/desktop). Verify surface details against current Claude Code docs.

## Config surface mapping

| OS component | Claude Code surface |
|---|---|
| `../core/01_CONSTITUTION.md` | Root `CLAUDE.md` -- Constitution first, then project facts per `../core/04_MEMORY_SYSTEM.md` section 2 |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | User-level `CLAUDE.md` (`~/.claude/CLAUDE.md`) |
| Folder rules | Per-directory `CLAUDE.md` (essential in monorepos; see `../playbooks/06_PLAYBOOKS.md` section 11) |
| `../skills/05_SKILLS_LIBRARY.md` skills | `SKILL.md` files -- keep Purpose/Trigger as the frontmatter description for progressive disclosure |
| Enforced behavior | **Hooks** -- anything that must happen *every* time (format, lint, block-path) belongs in a hook, not advisory text (`../core/04_MEMORY_SYSTEM.md` section 2) |
| Planning before edits (`../core/03_EXECUTION_ENGINE.md` section 6) | Plan mode -- read/propose without edits; use for ambiguous or risky work |
| Subagent delegation (`07` section 4) | Subagents -- keep exploratory file reads out of the main context |
| Reviewer / Security Sweep | Claude Code review with specialized agents; encode the `../skills/05_SKILLS_LIBRARY.md` output formats in the agents' definitions |
| Auto memory | Claude's memory -- personal learnings only; team-durable knowledge goes in versioned `CLAUDE.md` (`../core/04_MEMORY_SYSTEM.md` section 2) |

## Claude Code-specific notes

- Advisory `CLAUDE.md` text can be ignored under pressure; hooks are deterministic. Promote any repeatedly-violated rule from text to hook.
- Large codebases: scope reads and instructions per directory; deny generated/vendor/build outputs from context; prefer code intelligence over blind scanning (`02` section 2).
- The official guidance for this model family maps directly to Constitution articles: ground claims in tool results (III), state boundaries (VI), no premature endings and no context-budget panic (VII), use subagents for independent work (IX), construct a memory system (X). Include the *reason* behind requests when prompting -- it improves compliance.
- Add to `CLAUDE.md` after repeated mistakes or recurring review feedback -- exactly the `../core/04_MEMORY_SYSTEM.md` section 3 update loop.
