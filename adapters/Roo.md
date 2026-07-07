# Adapter: Roo Code

How the Aurelian maps onto Roo Code (mode-based IDE agent). Verify surface details against current Roo docs.

## Config surface mapping

| OS component | Roo surface |
|---|---|
| `../core/01_CONSTITUTION.md` | Project custom instructions (`.roo/rules/`) -- applied across all modes |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | Global custom instructions |
| Folder / mode-scoped rules | Mode-specific rule files (`.roo/rules-{mode}/`) |
| Role specialization (`../core/03_EXECUTION_ENGINE.md` algorithms) | **Modes**: Architect <-> `../core/03_EXECUTION_ENGINE.md` section 5-6, Code <-> section 1/section 3, Debug <-> section 2, Ask <-> research/questions, Orchestrator <-> decomposition + delegation (`07` section 4) |
| `../skills/05_SKILLS_LIBRARY.md` skills | Custom modes -- one skill can become one custom mode with matched tool permissions (e.g., a Reviewer mode with read-only file access) |
| Subagent delegation | Orchestrator mode delegating subtasks to other modes |

## Roo-specific notes

- Roo's mode architecture natively enforces the OS's sequencing: **architect before code, debugger before patch, reviewer before completion.** Encode that ordering in the orchestrator's instructions.
- Custom modes' tool permissions are enforcement, not advice: give the Reviewer mode no edit permission and the Security Sweep mode no shell, and the Constitution's boundaries become structural.
- Mode/rule sprawl is the known failure: apply `../core/04_MEMORY_SYSTEM.md` section 3 pruning -- every mode and rule must fire regularly or be merged/removed; two modes with overlapping mandates will eventually disagree.
- High-token settings can eat context: keep per-mode instructions tight and let the OS files load on demand (MANIFEST section 7).
