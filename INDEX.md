# Aurelian Index

This index defines the repository structure, recommended load order, and purpose of each file.

## Load Order

1. [core/01_CONSTITUTION.md](core/01_CONSTITUTION.md)  
   Always load first. It defines the non-negotiable laws.

2. [core/02_COGNITIVE_ARCHITECTURE.md](core/02_COGNITIVE_ARCHITECTURE.md)  
   Load when the task requires sustained reasoning, context management, subagents, or uncertainty handling.

3. [core/03_EXECUTION_ENGINE.md](core/03_EXECUTION_ENGINE.md)  
   Load for implementation, debugging, refactoring, research, review, UI, migration, and documentation tasks.

4. [core/07_DECISION_ENGINE.md](core/07_DECISION_ENGINE.md)  
   Load when the agent must decide whether to ask, proceed, stop, delegate, search, verify, or escalate.

5. [core/08_VERIFICATION_ENGINE.md](core/08_VERIFICATION_ENGINE.md)  
   Load before final claims, code review, risky changes, testing plans, or completion reports.

6. Load supporting files by task:

| Task | Add |
|---|---|
| Installing Aurelian into a project repo | [INSTALL_AURELIAN_IN_PROJECT.md](INSTALL_AURELIAN_IN_PROJECT.md) |
| Durable instructions or memory | [core/04_MEMORY_SYSTEM.md](core/04_MEMORY_SYSTEM.md) |
| Engineering judgment or architecture | [core/09_ENGINEERING_PHILOSOPHY.md](core/09_ENGINEERING_PHILOSOPHY.md), [core/10_TASTE_AND_DESIGN.md](core/10_TASTE_AND_DESIGN.md) |
| Unknown domains | [core/11_DOMAIN_INTELLIGENCE.md](core/11_DOMAIN_INTELLIGENCE.md), [core/12_SCIENTIFIC_REASONING.md](core/12_SCIENTIFIC_REASONING.md) |
| Model/tool routing | [core/13_MODEL_ROUTER.md](core/13_MODEL_ROUTER.md) |
| Reusable workflows | [skills/05_SKILLS_LIBRARY.md](skills/05_SKILLS_LIBRARY.md) |
| Project-type workflows | [playbooks/06_PLAYBOOKS.md](playbooks/06_PLAYBOOKS.md) |
| Copy-paste task prompts | [prompts/13_PROMPT_LIBRARY.md](prompts/13_PROMPT_LIBRARY.md) |
| Tool setup | One file from [adapters/](adapters/) |
| Project template | [templates/aurelian-project/](templates/aurelian-project/) |
| Worked examples | [examples/README.md](examples/README.md) |
| Evaluating the system | [evaluation/17_EVALUATION_PROTOCOL.md](evaluation/17_EVALUATION_PROTOCOL.md) |
| Improving Aurelian | [self-improvement/16_SELF_IMPROVEMENT.md](self-improvement/16_SELF_IMPROVEMENT.md) |

## File Map

### Top-Level Guides

- [README.md](README.md): overview, installation modes, repository map, provenance, and core rule.
- [INSTALL_AURELIAN_IN_PROJECT.md](INSTALL_AURELIAN_IN_PROJECT.md): official guide for applying the project template, agent loaders, bootstrap prompt, research docs, repo audit, roadmap, and milestone execution to any repository.

### Core

- [core/00_MANIFEST.md](core/00_MANIFEST.md): goals, design philosophy, dependency graph, evidence policy, and task load order.
- [core/01_CONSTITUTION.md](core/01_CONSTITUTION.md): the kernel; immutable laws every other file assumes.
- [core/02_COGNITIVE_ARCHITECTURE.md](core/02_COGNITIVE_ARCHITECTURE.md): how the agent allocates attention, memory, and reasoning effort.
- [core/03_EXECUTION_ENGINE.md](core/03_EXECUTION_ENGINE.md): numbered task algorithms.
- [core/04_MEMORY_SYSTEM.md](core/04_MEMORY_SYSTEM.md): durable knowledge policy.
- [core/07_DECISION_ENGINE.md](core/07_DECISION_ENGINE.md): branch conditions and decision trees.
- [core/08_VERIFICATION_ENGINE.md](core/08_VERIFICATION_ENGINE.md): proof standards, confidence levels, and completion rules.
- [core/09_ENGINEERING_PHILOSOPHY.md](core/09_ENGINEERING_PHILOSOPHY.md): operational axioms behind the Constitution.
- [core/10_TASTE_AND_DESIGN.md](core/10_TASTE_AND_DESIGN.md): engineering and design taste.
- [core/11_DOMAIN_INTELLIGENCE.md](core/11_DOMAIN_INTELLIGENCE.md): how to enter unfamiliar fields safely.
- [core/12_SCIENTIFIC_REASONING.md](core/12_SCIENTIFIC_REASONING.md): hypothesis testing, evidence, causality, and measurement.
- [core/13_MODEL_ROUTER.md](core/13_MODEL_ROUTER.md): routing work across models, harnesses, research tools, execution agents, reviewers, and future tools.

### Workflow Modules

- [skills/05_SKILLS_LIBRARY.md](skills/05_SKILLS_LIBRARY.md): installable skills such as Planner, Reviewer, Debugger, Security Sweep, Honest Advisor, and Documentation Steward.
- [playbooks/06_PLAYBOOKS.md](playbooks/06_PLAYBOOKS.md): end-to-end workflows for SaaS, APIs, CLIs, monorepos, migrations, legacy code, and greenfield projects.
- [playbooks/18_RESEARCH_TO_EXECUTION_OS.md](playbooks/18_RESEARCH_TO_EXECUTION_OS.md): full research-to-execution workflow from intake through discovery, research, synthesis, repo audit, roadmap, execution, review swarm, and learning update.
- [prompts/00_AURELIAN_BOOTSTRAP_PROMPT.md](prompts/00_AURELIAN_BOOTSTRAP_PROMPT.md): portable paste-in bootstrap prompt for starting a project with Aurelian in any capable tool.
- [prompts/13_PROMPT_LIBRARY.md](prompts/13_PROMPT_LIBRARY.md): portable prompts for agents that cannot load the full repository.

### Tooling

- [adapters/Aider.md](adapters/Aider.md)
- [adapters/Antigravity.md](adapters/Antigravity.md)
- [adapters/ChatGPTWeb.md](adapters/ChatGPTWeb.md)
- [adapters/ClaudeCode.md](adapters/ClaudeCode.md)
- [adapters/Cline.md](adapters/Cline.md)
- [adapters/Codex.md](adapters/Codex.md)
- [adapters/Cursor.md](adapters/Cursor.md)
- [adapters/GeminiCLI.md](adapters/GeminiCLI.md)
- [adapters/OpenHands.md](adapters/OpenHands.md)
- [adapters/Roo.md](adapters/Roo.md)

### Templates

- [templates/aurelian-project/](templates/aurelian-project/): reusable project scaffold with `AGENTS.md`, `CLAUDE.md`, Cursor rules, project docs, research/report folders, and `.aurelian` state files.

### Examples

- [examples/README.md](examples/README.md)
- [examples/planning.md](examples/planning.md)
- [examples/refactoring.md](examples/refactoring.md)
- [examples/code-review.md](examples/code-review.md)
- [examples/debugging-report.md](examples/debugging-report.md)
- [examples/prompting.md](examples/prompting.md)

### Governance

- [CHANGELOG.md](CHANGELOG.md)
- [LICENSE.md](LICENSE.md)
- [evaluation/17_EVALUATION_PROTOCOL.md](evaluation/17_EVALUATION_PROTOCOL.md)
- [self-improvement/16_SELF_IMPROVEMENT.md](self-improvement/16_SELF_IMPROVEMENT.md)

## Public Identity

Use **Aurelian** as the public-facing name. Historical research provenance should not define the brand.
