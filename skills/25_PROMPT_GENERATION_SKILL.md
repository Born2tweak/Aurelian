# 25_PROMPT_GENERATION_SKILL -- Generate Complete Prompt Suites

## Purpose

Create a complete, dependency-ordered, tool-aware prompt suite for a project idea, repository state, target artifact, current milestone, or unresolved problem. The skill uses `../core/15_PROMPT_GENERATION_ENGINE.md`, `../core/13_MODEL_ROUTER.md`, and `../core/14_TRACEABILITY_ENGINE.md` to produce prompts that are small enough to execute, rich enough to verify, and explicit about tool routing, evidence, stop conditions, traceability, and human approval gates.

## Trigger

Use this skill when:

1. A project or milestone needs a sequence of prompts rather than one broad prompt.
2. Work must move across tools such as ChatGPT Web, Codex, Claude Opus, Claude Sonnet, Fable, Cursor, Antigravity, or a future tool.
3. Research, audit, planning, execution, review, and deployment readiness must stay traceable.
4. Token budget, repo access, browser/research access, autonomy, risk, or output format constraints matter.
5. An earlier prompt failed because it was too broad, under-specified, missing evidence standards, or routed to the wrong tool.

Do not use this skill to answer the project question directly. It generates the prompts and manifest needed to do the work.

## Inputs

Accept:

- Project description, current objective, target artifact, milestone, issue, or unresolved problem.
- Current repo state, available docs, research reports, ADRs, roadmap, tests, designs, logs, and prior prompt outputs.
- Available models/tools and their actual capabilities: repo access, shell/tests, browser/research, screenshots, design tools, deployment, external services, subagents.
- Token constraints, risk constraints, autonomy level, desired output format, evidence requirements, and human approval boundaries.
- Existing traceability IDs from requirements, reports, issues, decisions, commits, tests, evidence logs, or milestones.

If inputs are thin, generate a discovery prompt first and mark downstream prompts as provisional.

## Algorithm

1. **State the objective.** Identify the project or milestone outcome and the artifact that must exist next.
2. **Inventory evidence.** List available local docs, repo paths, research, decisions, tests, logs, and supplied context. Mark unavailable repo or browser evidence explicitly.
3. **Select the smallest sufficient context.** Include full text only where the target agent must edit, audit, or verify exact details. Use summaries for stable context. Reference canonical documents instead of repeating them when the target tool can access them.
4. **Choose prompt categories.** Consider discovery, research planning, individual research reports, research criticism, contradiction review, knowledge synthesis, architecture decisions, repository audits, gap analysis, roadmap creation, milestone execution, testing, debugging, UI/taste review, security review, performance review, accessibility review, documentation updates, learning capture, pre-push review, and deployment readiness. Include only categories that feed the objective.
5. **Split by dependency.** Order prompts so each one has the context it needs: discovery before research, research before synthesis, synthesis before architecture, repo audit before gap analysis, gap analysis before roadmap, roadmap before milestone execution, execution before review, review before deployment readiness.
6. **Assign prompt class.** Use Generation Prompts for new artifacts, Analysis Prompts for critique/audit/verification, and Execution Prompts for repo changes, tests, commits, and milestones.
7. **Route with the Model Router.** Assign target and fallback tools based on required affordances, token budget, repo access, browser/research access, autonomy level, task risk, desired output format, evidence requirements, and stop conditions.
8. **Preserve traceability.** Carry IDs forward exactly across prompts. Upstream and downstream artifacts must be named in each prompt's metadata.
9. **Write prompt metadata.** Every prompt must include prompt ID, purpose, target tool/model, required inputs, expected outputs, upstream artifacts, downstream artifacts, risk level, estimated context size, evidence requirements, stop condition, fallback model/tool, approval gates, autonomy level, token budget, desired output format, and traceability IDs.
10. **Write prompt bodies.** Keep each body focused on one deliverable. Avoid duplicated operating-system text; reference Aurelian files or project docs instead.
11. **Add revision rules.** Tell downstream agents how to revise failed prompts based on evidence: split scope, add missing context, change route, tighten deliverable, strengthen evidence, or add stop conditions.
12. **Emit the Prompt Suite Manifest.** Include objective, dependency graph, execution order, prompt IDs, assigned model/tool, expected artifact, required context, token-efficiency notes, approval gates, completion status, artifact map, fallback routing, verification requirements, and open risks.
13. **Run the quality gate.** Reject prompts that are giant, duplicated, context-heavy without reason, premium-model wasteful, mixed research/execution without justification, missing deliverables, missing evidence standards, or missing stop conditions.

## Checklist

- Objective and target artifact are explicit.
- Every selected prompt category feeds a downstream artifact or decision.
- Complex work is split into dependency-ordered prompts.
- Each prompt has exactly one primary deliverable.
- Every prompt has the required metadata.
- Context is the smallest sufficient set for the target tool.
- Canonical docs are referenced instead of duplicated when accessible.
- Traceability IDs are preserved exactly.
- Model-specific variants do not change project truth.
- Premium models are reserved for high-judgment, high-risk, or large-context work.
- Research and implementation are separated unless combining them is justified.
- Evidence requirements and stop conditions are explicit.
- Human approval gates are named for destructive, external, credentialed, financial, legal, public-contract, push, deploy, delete, purchase, or dependency-addition actions.
- The Prompt Suite Manifest includes dependency graph, execution order, artifact map, fallback routing, approval gates, verification requirements, and completion status.

## Example

A user says: "We need to add a billing portal to this SaaS repo."

The skill does not write one mega-prompt. It emits:

1. Discovery prompt for Codex to inspect billing-related repo paths and existing auth/account models.
2. Research planning prompt for ChatGPT Web or Claude Opus to identify current billing provider docs and compliance questions.
3. Individual research prompts for provider APIs, security/privacy, UX expectations, and testing strategy.
4. Research criticism and contradiction review prompts.
5. Knowledge synthesis prompt producing implementation constraints.
6. Architecture decision prompt producing an ADR.
7. Repo audit and gap analysis prompts for Codex/Cursor.
8. Roadmap prompt for a reversible milestone sequence.
9. Execution prompts for each milestone.
10. Testing, security, accessibility, performance, documentation, learning capture, pre-push, and deployment readiness prompts with evidence gates.

Every prompt carries IDs such as `REQ-BILLING-PORTAL`, `ADR-BILLING-001`, and `MILESTONE-BILLING-02` through upstream and downstream artifacts.

## Failure Modes

- Creating one giant prompt that asks for discovery, research, implementation, testing, and deployment at once.
- Copying the same long Aurelian rules into every prompt instead of referencing canonical files.
- Sending entire repos or research folders where a summary and selected files would suffice.
- Assigning Claude Opus or another premium model to repetitive low-risk execution.
- Asking an agent with no repo access to verify code changes.
- Asking an agent with no browser access to independently validate current external facts.
- Producing prompts without explicit artifacts, evidence requirements, stop conditions, or approval gates.
- Changing traceability IDs between variants.
- Treating a generated prompt suite as complete without a manifest and quality gate.

## Output Format

```text
Prompt Suite

Project or milestone objective:

Available inputs:
- Repository state:
- Project documents:
- Current objective:
- Available models/tools:
- Token constraints:
- Risk constraints:
- Autonomy level:

Recommended workflow:

Routing decisions:
- Prompt ID:
  Target tool/model:
  Why this route:
  Fallback:

Prompt dependency graph:

Execution order:
1. Prompt ID
   Purpose:
   Assigned model/tool:
   Expected artifact:

Complete ordered prompt suite:
- Prompt ID:
  Prompt class:
  Purpose:
  Target tool/model:
  Fallback model/tool:
  Required inputs:
  Expected outputs:
  Upstream artifacts:
  Downstream artifacts:
  Risk level:
  Estimated context size:
  Token budget:
  Evidence requirements:
  Stop condition:
  Human approval required before:
  Autonomy level:
  Desired output format:
  Traceability IDs:
  Prompt body:

Prompt Suite Manifest:
- Project or milestone objective:
- Prompt dependency graph:
- Execution order:
- Prompt IDs:
- Assigned model/tool:
- Expected artifact from each prompt:
- Required context:
- Token-efficiency notes:
- Approval gates:
- Completion status:

Artifact map:

Verification requirements:

Fallback routing:

Open risks and stop conditions:
```
