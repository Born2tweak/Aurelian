# Adapter: Cursor

How the Aurelian maps onto Cursor (editor agent, Cloud Agents, Bugbot). Verify surface details against current Cursor docs.

## Config surface mapping

| OS component | Cursor surface |
|---|---|
| `../core/01_CONSTITUTION.md` | `AGENTS.md` at repo root, or an always-applied rule in `.cursor/rules/` |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | User rules (Cursor settings) |
| Project rules | `.cursor/rules/*.mdc` -- use `alwaysApply` for constitution-level rules, glob/description triggers for scoped ones |
| Folder rules | Nested `.cursor/rules/` in subdirectories, or glob-scoped rules |
| `../skills/05_SKILLS_LIBRARY.md` skills | Cursor skills (`SKILL.md`); agent-requestable rules also work for smaller procedures |
| Subagent delegation (`07` section 4) | Background/Cloud Agents and subagent tasks; parallel tool calls for independent reads |
| Reviewer / Security Sweep | **Bugbot** on PRs -- encode `../skills/05_SKILLS_LIBRARY.md` Reviewer/Security output standards as repository/team rules |
| Auto memory | Cursor memories -- personal/project observations; team-durable knowledge goes in versioned rules (`../core/04_MEMORY_SYSTEM.md` section 2) |

## Cursor-specific notes

- Rules support conditional loading (globs, descriptions): this is the OS's progressive-disclosure model natively -- keep always-applied text minimal (`../core/04_MEMORY_SYSTEM.md` section 3) and let task-scoped rules carry detail.
- Combine generation with automatic review: agent writes, Bugbot reviews -- but Bugbot doesn't replace the self-review rung of the verification ladder (`../core/08_VERIFICATION_ENGINE.md` section 2.6).
- Cloud/background agents widen the attack surface: apply Constitution Art. V strictly (no external side effects without confirmation) and treat untrusted repo content/MCP servers as trust boundaries (Security Sweep, `../skills/05_SKILLS_LIBRARY.md`).
- Capture project facts as rules, not just chat memory -- memories are convenience, rules are the system of record.
