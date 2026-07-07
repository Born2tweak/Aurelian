# Adapter: Cline

How the Aurelian maps onto Cline (IDE-native agent). Verify surface details against current Cline docs.

## Config surface mapping

| OS component | Cline surface |
|---|---|
| `../core/01_CONSTITUTION.md` | `.clinerules` (or `.clinerules/` folder) at repo root |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | Global rules in Cline settings |
| Planning before edits (`../core/03_EXECUTION_ENGINE.md` section 6) | **Plan & Act** modes -- Plan for `../core/03_EXECUTION_ENGINE.md` section 6, Act for execution; switch deliberately, not by default |
| Checkpoints (`../core/03_EXECUTION_ENGINE.md` section 6.4) | Cline checkpoints -- snapshot at meaningful risk boundaries so failed phases roll back cleanly |
| Durable memory (`../core/04_MEMORY_SYSTEM.md`) | Memory bank -- project state across sessions; still keep team-durable rules in versioned `.clinerules` (`../core/04_MEMORY_SYSTEM.md` section 2) |
| Subagent delegation (`07` section 4) | Subagents / agent teams |
| External tools | MCP servers |

## Cline-specific notes

- **Auto-approve is an autonomy dial:** align it with Constitution Art. V -- auto-approve reversible in-scope operations (reads, scoped edits, tests); never auto-approve destructive commands, external side effects, or anything touching credentials.
- MCP security posture matters: every MCP server is a trust boundary; apply the Security Sweep mindset before enabling one on sensitive repos.
- IDE context can be noisy (open tabs, diagnostics): apply `02` section 2 deliberately -- the visible file is not automatically the relevant file.
- Checkpoints + Plan/Act make Cline a natural fit for the phased playbooks in `../playbooks/06_PLAYBOOKS.md`; checkpoint after each milestone's verification, not on a timer.
