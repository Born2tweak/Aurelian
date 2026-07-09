# Adapter: ChatGPT Web

How Aurelian maps onto ChatGPT Web. Verify product-specific surface details against current OpenAI docs when they matter; the adapter routes by observed session capability first and product label second.

## Config surface mapping

| OS component | ChatGPT Web surface |
|---|---|
| `../core/01_CONSTITUTION.md` | Custom instructions, project instructions, or the portable bootstrap prompt in `../prompts/00_AURELIAN_BOOTSTRAP_PROMPT.md` |
| Task algorithms (`../core/03_EXECUTION_ENGINE.md`) | Paste the relevant algorithm or use an Aurelian project chat with stable instructions |
| Model routing (`../core/13_MODEL_ROUTER.md`) | Use ChatGPT Web primarily for research synthesis, architecture alternatives, taste review, prompt drafting, and cross-tool handoff notes |
| Research-to-execution (`../playbooks/18_RESEARCH_TO_EXECUTION_OS.md`) | Intake, discovery synthesis, research prompt generation, source-backed dossiers, roadmap drafting, and review-swarm synthesis |
| Project template | Attach or paste from `../templates/aurelian-project/docs/*`, `.aurelian/*`, and `AGENTS.md` when the web session lacks direct repo access |
| Verification (`../core/08_VERIFICATION_ENGINE.md`) | Source citations, generated checklists, and handoff requirements; repo claims remain unverified unless the session has direct file/command evidence |
| Handoff contract (`../core/13_MODEL_ROUTER.md` section 6) | Produce objective, constraints, inspected artifacts, confidence, forbidden actions, required verification, and exact output format for the repo-native executor |

## ChatGPT Web-specific notes

- Best role: broad ideation, unfamiliar-domain research, source synthesis, product/taste critique, architecture option framing, prompt drafting, and turning fuzzy intent into executable milestones.
- Avoid treating ChatGPT Web as the verifier for code changes unless the active session can inspect the repository, run commands, and review the diff. If it cannot produce command or diff evidence, it may advise but cannot close the verification ladder.
- In the Research-to-Execution OS, ChatGPT Web is strongest in stages 1-6 and 11: intake, discovery synthesis, research prompts, research quality review, knowledge synthesis, roadmap language, and review-swarm synthesis.
- For milestone execution, hand off to Codex, Cursor, Antigravity, Claude Code, or another repo-native harness with the full handoff contract from `../core/13_MODEL_ROUTER.md` section 6.
- When using external research, require source ranking, dates, uncertainty, and conflicts. Do not promote unsourced synthesis into project fact.
- Require explicit user approval before recommending push, deploy, delete, external service actions, credential use, purchases, or dependency additions.
- Completion reports must say what came from sources, what came from supplied artifacts, and what remains unverified in the live repo.
