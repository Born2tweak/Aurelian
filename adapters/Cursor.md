# Adapter: Cursor

How Aurelian maps onto Cursor (editor agent, Cloud Agents, Bugbot, and IDE-native review loops). Verify surface details against current Cursor docs and the active workspace; route by observed capability first and product label second.

## Config surface mapping

| OS component | Cursor surface |
|---|---|
| `../core/01_CONSTITUTION.md` | `.cursor/rules/*.mdc` as the main Cursor instruction surface, especially an always-applied core rule |
| Global rules (`../core/04_MEMORY_SYSTEM.md` section 1) | User rules (Cursor settings) |
| Cross-tool project loader | `AGENTS.md` at repo root, shared with Codex and other AGENTS-aware tools |
| Project rules | `.cursor/rules/*.mdc` -- use `alwaysApply` for constitution-level rules, glob/description triggers for scoped execution, review, and UI/taste rules |
| Folder rules | Nested `.cursor/rules/` in subdirectories, or glob-scoped rules |
| `../skills/05_SKILLS_LIBRARY.md` skills | Cursor skills (`SKILL.md`); agent-requestable rules also work for smaller procedures |
| Model routing (`../core/13_MODEL_ROUTER.md`) | Cursor is a repo-native execution/editor route, not the default deep research route |
| Research-to-execution (`../playbooks/18_RESEARCH_TO_EXECUTION_OS.md`) | Use Cursor for repo audit, gap analysis, milestone execution, verification, and review after research artifacts and roadmap exist |
| Aurelian project template | `../templates/aurelian-project/.cursor/rules/*.mdc`, root `AGENTS.md`, `docs/*`, and `.aurelian/*` |
| Subagent delegation (`07` section 4) | Background/Cloud Agents and subagent tasks; parallel tool calls for independent reads |
| Reviewer / Security Sweep | **Bugbot** on PRs -- encode `../skills/05_SKILLS_LIBRARY.md` Reviewer/Security output standards as repository/team rules |
| Auto memory | Cursor memories -- personal/project observations; team-durable knowledge goes in versioned rules (`../core/04_MEMORY_SYSTEM.md` section 2) |

## Cursor-specific notes

- Cursor's best role is local editing, fast UI iteration, repo-aware debugging, small-to-medium implementation, targeted refactors, and visible-diff review inside the IDE.
- Use `.cursor/rules/*.mdc` as the primary Aurelian instruction surface for Cursor. Keep `aurelian-core.mdc` always applied and use task-scoped rules like `aurelian-execution.mdc`, `aurelian-review.mdc`, and `aurelian-ui-taste.mdc` from `../templates/aurelian-project/.cursor/rules/`.
- Use root `AGENTS.md` as the cross-tool project loader. It should point all capable tools to the same project facts, forbidden actions, verification commands, and Aurelian load order.
- Rules support conditional loading (globs, descriptions): this is the OS's progressive-disclosure model natively -- keep always-applied text minimal (`../core/04_MEMORY_SYSTEM.md` section 3) and let task-scoped rules carry detail.
- In the Model Router, route Cursor when the next decision needs editor-native repo context, fast iteration, local diffs, targeted tests, or visual/UI feedback. Route deep external research to ChatGPT Web, Claude Opus, Fable, or another research-capable tool unless Cursor has the right external context and source-review surface.
- In the Research-to-Execution OS, use Cursor for milestone execution only after `docs/06_IMPLEMENTATION_ROADMAP.md` exists or the milestone is otherwise explicitly scoped with objective, files, constraints, risks, and verification gates.
- Evidence-gated milestone execution in Cursor means: read the milestone, inspect the relevant repo surface, implement the smallest coherent change, run the narrowest meaningful check, review the diff, then record/report evidence before advancing.
- Use Cursor for UI/taste passes with `docs/03_PRODUCT_EXPERIENCE_BIBLE.md` and `.aurelian/taste-reference.md` loaded, plus `aurelian-ui-taste.mdc`. For shipped UI claims, require rendered or screenshot evidence.
- Avoid using Cursor as the primary deep research engine unless it has the required external context, source quality controls, and date checks. Unsourced chat synthesis should not become project fact.
- Combine generation with automatic review: agent writes, Bugbot reviews -- but Bugbot doesn't replace the self-review rung of the verification ladder (`../core/08_VERIFICATION_ENGINE.md` section 2.6).
- Cloud/background agents widen the attack surface: apply Constitution Art. V strictly (no external side effects without confirmation) and treat untrusted repo content/MCP servers as trust boundaries (Security Sweep, `../skills/05_SKILLS_LIBRARY.md`).
- Require manual approval before push, deploy, delete, external service actions, credential use, purchases, or dependency additions.
- Require verification before claiming success. If Cursor cannot run the needed command, inspect the relevant render, or review the diff in the active session, report that limitation and downgrade confidence.
- Capture project facts as rules, not just chat memory -- memories are convenience, rules are the system of record.
