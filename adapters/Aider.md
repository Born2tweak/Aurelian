# Adapter: Aider

How the Aurelian maps onto Aider (git-integrated terminal pair programmer). Verify surface details against current Aider docs.

## Config surface mapping

| OS component | Aider surface |
|---|---|
| `../core/01_CONSTITUTION.md` | Conventions file (e.g., `CONVENTIONS.md` loaded read-only via `/read` or config) -- Constitution + project facts per `../core/04_MEMORY_SYSTEM.md` section 2 |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | `.aider.conf.yml` (user and repo level) + always-loaded read-only files |
| Repo exploration (`07` section 5.3) | **Repo map** -- Aider's native concise map of classes/functions/signatures; this *is* the "read structure, not bodies" strategy |
| Scoped context (`02` section 2) | Files explicitly added to the chat -- add only what will be edited or contract-checked; the repo map covers the rest |
| Verification (`../core/08_VERIFICATION_ENGINE.md`) | `/test` and `/lint` commands, auto-test config; run the narrow rung after each edit |
| Diff review (`../core/08_VERIFICATION_ENGINE.md` section 2.6) | Git integration -- every change is a commit; review with `git diff`, undo with `/undo` |

## Aider-specific notes

- Aider is pair programming, not autonomous orchestration: the human drives file selection and sequencing, so the OS's `07` decision trees apply to the *human+agent pair* -- the user should ask Aider for a plan (`../prompts/13_PROMPT_LIBRARY.md` section Planner) before large edits.
- The repo-map technique generalizes: even outside Aider, prefer a compact symbol/signature map plus targeted full reads over bulk loading (`02` section 2).
- Git-per-edit is a checkpoint system (`../core/03_EXECUTION_ENGINE.md` section 6.4) for free: keep edits small so each commit is independently revertable -- blast-radius control by construction.
- No subagents: decompose by running focused sessions per subtask instead, carrying durable context in the conventions file.
