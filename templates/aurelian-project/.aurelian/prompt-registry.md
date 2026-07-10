# Prompt Registry

## Purpose

Track generated prompt suites, prompt IDs, routing, evidence requirements, approval gates, and completion status for this project.

Do not invent facts. A prompt is registered only when it has a concrete objective, target tool/model, expected artifact, evidence standard, stop condition, and downstream use.

## Prompt Suite Manifest Format

### SUITE-YYYYMMDD-NN: Suite Title

1. Project or milestone objective:
2. Prompt dependency graph:
3. Execution order:
4. Prompt IDs:
5. Assigned model/tool:
6. Expected artifact from each prompt:
7. Required context:
8. Token-efficiency notes:
9. Approval gates:
10. Completion status:

## Prompt Entry Format

### PROMPT-ID: Prompt Title

- Suite ID:
- Prompt class: Generation | Analysis | Execution
- Purpose:
- Target tool/model:
- Fallback model/tool:
- Required inputs:
- Expected outputs:
- Upstream artifacts:
- Downstream artifacts:
- Risk level: low | medium | high | critical
- Estimated context size: small | medium | large | extra-large
- Token budget:
- Evidence requirements:
- Stop condition:
- Human approval required before:
- Autonomy level:
- Desired output format:
- Traceability IDs:
- Status: not started | in progress | blocked | complete | superseded
- Result artifact:
- Evidence:
- Notes:

## Routing Notes

Use current observed tool capability over product label. Common defaults:

- ChatGPT Web: broad research synthesis, architecture framing, prompt suite generation, taste critique, and handoff notes.
- Codex: repo-grounded execution, tests, diffs, docs edits, registry updates, and evidence-grounded completion reports.
- Claude Opus: deep architecture, large-context synthesis, high-risk contradiction review, and complex review.
- Claude Sonnet: balanced planning, execution, and review where scope is clear.
- Fable: narrative synthesis, product/design framing, research-to-roadmap translation, and taste-sensitive language.
- Cursor: editor-native repo work, audits, refactors, and milestone execution.
- Antigravity: agentic IDE exploration, prototype-to-code loops, and visual/product iteration.
- Future tools: route by repo access, command evidence, browser/research surface, context, autonomy controls, and handoff quality.

## Registry

Add newest prompt suites first.
