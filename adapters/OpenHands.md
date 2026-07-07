# Adapter: OpenHands

How the Aurelian maps onto OpenHands (open-source agent platform + SDK). Verify surface details against current OpenHands docs.

## Config surface mapping

| OS component | OpenHands surface |
|---|---|
| `../core/01_CONSTITUTION.md` | Repo instruction file (AGENTS.md-style microagents / repo config) + system-prompt customization via the SDK |
| Task algorithms (`../core/03_EXECUTION_ENGINE.md`) | SDK task planning/decomposition -- encode the algorithms as agent instructions or custom tools |
| Context economy (`02` section 2-3) | Built-in automatic context compression -- still apply the hoarding/starvation rules; compression is mechanism, not judgment |
| Security Sweep (`../skills/05_SKILLS_LIBRARY.md`) | Built-in security analyzer -- run it, then hand-verify top findings (a scanner pass is not the full sweep) |
| Subagent delegation (`07` section 4) | Delegation across agents; Slack/GitHub/Linear automation for workflow triggers |
| Verification (`../core/08_VERIFICATION_ENGINE.md`) | Sandboxed workspace (Docker/VM) -- run the ladder inside the sandbox; sandbox results are session tool evidence |

## OpenHands-specific notes

- OpenHands's thesis matches the OS's assumption (`00` section 4): **the harness is part of intelligence.** Strong agent-computer interfaces, workspace isolation, and context compression are model multipliers -- invest in tool quality, not just prompt text.
- Because agents here can run long and autonomously, Constitution Art. V and VII do the heavy lifting: define the destructive-action boundary in the agent config *before* launch, and require the completion audit (`../core/08_VERIFICATION_ENGINE.md` section 5) in the final-report template.
- Self-hosting means security configuration is yours: workspace isolation settings, credential scoping, and MCP/tool allowlists are trust boundaries.
- When building custom tools via the SDK, follow the ACI research lesson: LM-friendly commands, concise feedback, guardrails -- interface design improves the same model.
