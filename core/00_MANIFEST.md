# 00_MANIFEST -- Goals, Design Philosophy, Dependency Graph

## 1. Purpose

This operating system transfers the engineering intelligence common to elite coding agents (Codex, Claude Code, Aider, OpenHands, SWE-agent, Cline, Roo Code, Cursor, Devin, Amp, Gemini CLI) and public agent-engineering sources into a portable, model-agnostic form. Give these files to any capable coding model with no prior knowledge of Aurelian, and its execution quality should measurably improve.

Governing theorem: **Intelligence is not the accumulation of knowledge. Intelligence is the allocation of attention under uncertainty toward the user's objective.**

## 2. Success criteria

The OS succeeds if, versus the same model without it, the model:

1. **Plans better** -- turns ambiguous requests into scoped, risk-aware plans with "done when" criteria.
2. **Debugs more accurately** -- reproduces before patching; fixes root causes, not symptoms.
3. **Reasons architecturally** -- identifies contracts, blast radius, and hidden coupling before editing.
4. **Sustains long contexts** -- compresses stable context, delegates exploration, avoids context rot and context-budget panic.
5. **Verifies rigorously** -- no completion claim without session tool evidence; uses the verification ladder proportional to risk.
6. **Hallucinates less** -- names evidence types, states what was not checked, distinguishes inference from observation.
7. **Reviews better** -- findings first, severity-ordered, file/line-grounded, no vague approval.
8. **Shows design taste** -- matches local patterns, resists over-abstraction and over-refactoring, produces coherent UX.
9. **Adapts to unfamiliar domains** -- builds working models via source triage before implementing.

And the OS itself is: **model-agnostic** (core files name products only when source attribution or adapter mapping requires it), **internally consistent** (one concept, one home), **maintainable** ([../self-improvement/16_SELF_IMPROVEMENT.md](../self-improvement/16_SELF_IMPROVEMENT.md) governs evolution), **extensible** (new skills/playbooks/adapters slot in without rewrites), **understandable** (each file readable standalone with cross-references), and **executable** (algorithms, checklists, decision trees, prompts -- not inspirational prose).

## 3. Design philosophy

- **Prime constraint:** no file exists because it is interesting. Every file exists because removing it would make the OS materially worse.
- **One concept, one home.** Each concept is defined in exactly one file; others cross-reference it. Canonical homes:
  - Immutable laws -> 01. Attention/reasoning/metacognition -> 02. Task algorithms -> 03. Durable memory policy -> 04. Skill definitions -> 05. Project workflows -> 06. Decision trees (ask/proceed/stop/delegate) -> 07. Verification ladder, evidence discipline, confidence levels -> 08. Engineering axioms -> 09. Taste heuristics -> 10. Domain acquisition -> 11. Hypothesis/evidence method -> 12. Copy-paste prompts -> 13. Tool mappings -> 14. Worked examples -> 15. OS evolution -> 16.
- **Executable over inspirational.** Every section must change what the model does next, or it is cut.
- **Constitutional form.** State the governing law, then the algorithm, then the checklist.
- **Progressive disclosure.** The Constitution is always loaded; everything else loads on demand.

## 4. Assumptions

- The reader is a frontier-class coding model inside an agent harness with file read/write, search, and shell/test execution. Where a tool is missing, degrade gracefully (e.g., no shell -> state that verification was not possible).
- The harness is part of intelligence: the same model performs better with better tools, feedback, and durable instructions. This OS is the durable-instruction layer.
- No product facts (pricing, availability, model IDs) are load-bearing here; if current product facts matter, check current official docs.

## 5. Evidence policy (source reliability)

This OS is derived from a research dossier with an explicit reliability hierarchy, which the OS carries forward:

- **High reliability:** official vendor docs (Anthropic, OpenAI, tool maintainers), peer-reviewed papers (SWE-agent/ACI, SWE-bench), official benchmark sites.
- **Medium/low reliability:** community repos, social videos, and prompt-reconstruction repositories. These are **pattern evidence only** -- they show instruction-architecture styles, never authoritative configuration. Do not treat prompt text as a substitute for capability; capability comes from model + harness + memory + tools + verification.

## 6. Dependency graph

```
01_CONSTITUTION  (kernel -- everything depends on it; depends on nothing)
   |-- 02_COGNITIVE_ARCHITECTURE   (how to think; uses 08's confidence levels)
   |      |-- 03_EXECUTION_ENGINE  (what to do; calls 07 for branching, 08 for verification)
   |      |-- 07_DECISION_ENGINE   (when to ask/stop/delegate; uses 08 confidence levels)
   |      `-- 12_SCIENTIFIC_REASONING (evidence method; feeds 08 and 11)
   |-- 08_VERIFICATION_ENGINE      (proof standards; used by 03, 05, 06, 07)
   |-- 04_MEMORY_SYSTEM            (durable knowledge; consumes lessons from 03/16)
   |-- 09_ENGINEERING_PHILOSOPHY   (why the laws exist; grounds 01 and 10)
   |      `-- 10_TASTE_AND_DESIGN  (judgment; used by 03 review/UI steps)
   |-- 11_DOMAIN_INTELLIGENCE      (unfamiliar fields; uses 12's evidence ladder)
   |-- 05_SKILLS_LIBRARY           (packaged workflows; composes 03 + 08 + 13)
   |-- 06_PLAYBOOKS                (project workflows; composes 03 + 05)
   |-- 13_PROMPT_LIBRARY           (copy-paste text; operationalizes 05 skills)
   |-- adapters/                (tool mapping; depends on 04's memory hierarchy)
   |-- examples/                (worked demonstrations of 03, 08, 10, 13)
   `-- 16_SELF_IMPROVEMENT         (evolves everything; uses 04's update rules)
```

## 7. Load order by task type

Always: `01_CONSTITUTION.md`. Then:

| Task type | Load |
|---|---|
| Feature implementation | 03 -> 07 -> 08 (+ 10 for API/UX surface) |
| Debugging | 03 (section Debugging) -> 12 -> 08 |
| Refactoring | 03 (section Refactoring) -> 10 -> 08 |
| Architecture / design | 02 -> 09 -> 10 -> 07 |
| Code review | 05 (section Reviewer) -> 08 -> 10 |
| New project / greenfield | 06 -> 05 (section Setup) -> 10 |
| Research / unfamiliar domain | 11 -> 12 |
| UI work | 03 (section UI) -> 10 -> 08 (visual verification) |
| Migration / legacy | 06 (section Migration, section Legacy) -> 03 -> 08 |
| Long-running / multi-phase | 02 -> 07 (section Delegation) -> 04 |
| Writing docs | 03 (section Documentation) -> 10 (section Writing) |
| Improving this OS itself | 16 -> 04 |

Tool-specific setup: read the matching file in `../adapters/` once per environment, not per task.
