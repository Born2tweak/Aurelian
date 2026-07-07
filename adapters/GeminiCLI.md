# Adapter: Gemini CLI

How the Aurelian maps onto Gemini CLI (open-source terminal agent). Verify surface details against current Google docs.

## Config surface mapping

| OS component | Gemini CLI surface |
|---|---|
| `../core/01_CONSTITUTION.md` | `GEMINI.md` at repo root (context file loaded into the session) |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | User-level `~/.gemini/GEMINI.md` |
| Folder rules | `GEMINI.md` files in subdirectories (hierarchical context) |
| Durable memory (`../core/04_MEMORY_SYSTEM.md`) | `/memory` command + `GEMINI.md`; team-durable knowledge belongs in the versioned file, not session memory |
| Research skill (`../skills/05_SKILLS_LIBRARY.md`) | Built-in web search / web fetch tools |
| External tools | MCP servers (local/remote) |
| Repo exploration (`07` section 5) | Built-in grep, file read/write, terminal |

## Gemini CLI-specific notes

- The agent runs a plain reason-and-act loop: think, act, observe, adjust. That loop is exactly `02` section 1 compressed -- the OS's contribution is the allocation discipline (section 2), the branch conditions (`07`), and the proof standards (`../core/08_VERIFICATION_ENGINE.md`) layered on top of it.
- No native skills/subagent architecture comparable to richer harnesses: emulate skills by keeping `../skills/05_SKILLS_LIBRARY.md`-format files in the repo and pasting the relevant `../prompts/13_PROMPT_LIBRARY.md` prompt for the task; emulate delegation by scoping separate sessions with the Subagent Delegation prompt.
- Broad general utility can blur coding discipline -- pin the session to the elite loop by putting the Constitution and the relevant `../core/03_EXECUTION_ENGINE.md` algorithm into `GEMINI.md`.
- Quotas and harness limits shape behavior: prefer narrow reads and repo-map-style structure scans (`07` section 5.3) over bulk file loading.
