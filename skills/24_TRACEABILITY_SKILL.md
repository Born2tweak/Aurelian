# 24_TRACEABILITY_SKILL -- Audit The Engineering Knowledge Graph

## Purpose

Use this skill to follow, audit, repair, or report the evidence chain connecting Aurelian artifacts: vision, discovery, research, reasoning, decisions, specs, milestones, source files, tests, evidence, reviews, lessons, updated research, commits, implementation reports, and roadmap updates.

The skill operationalizes `../core/14_TRACEABILITY_ENGINE.md`.

## Trigger

Use this skill when:

1. A task asks for traceability, knowledge graph, evidence chain, impact analysis, stale-doc detection, orphan detection, or lifecycle audit.
2. A milestone is planned, completed, reviewed, superseded, or archived.
3. Research, specs, ADRs, roadmap items, implementation reports, test evidence, reviews, commits, or lessons need to be connected.
4. The project has `.aurelian/traceability.md`.
5. An agent needs to determine whether code is undocumented, a spec is unimplemented, research had no downstream impact, or active decisions conflict.

## Inputs To Inspect

Start with the narrowest set that can answer the question:

- `.aurelian/traceability.md`
- `.aurelian/project-state.md`
- `.aurelian/decision-log.md`
- `.aurelian/evidence-log.md`
- `.aurelian/resource-index.md`
- `docs/00_PROJECT_BRIEF.md`
- `docs/01_PROJECT_BIBLE.md`
- `docs/02_TECHNICAL_DESIGN_SPEC.md`
- `docs/03_PRODUCT_EXPERIENCE_BIBLE.md`
- `docs/06_IMPLEMENTATION_ROADMAP.md`
- `docs/07_RESEARCH_GAPS.md`
- `docs/08_RESOURCE_ATLAS.md`
- `research/`
- `reports/milestones/`
- `reports/reviews/`
- `reports/audits/`
- `reports/learning/`
- ADRs, issues, commits, tests, and source files relevant to the scope.

Do not read the entire repository by default. Expand only along parent/child links, named paths, specs, tests, or search results relevant to the trace question.

## Algorithm

1. **Define scope.** Name the artifact, milestone, module, decision, research dossier, or lifecycle segment being audited.
2. **Load the graph.** Read `.aurelian/traceability.md` and any directly linked entries. If the registry does not exist, build a provisional graph from decision logs, evidence logs, specs, reports, git history, and source paths.
3. **Walk upstream.** Follow parents until reaching a vision, user request, issue, discovery note, or canonical source. Record missing parents and weak rationale.
4. **Walk downstream.** Follow children through specs, milestones, source files, tests, evidence, review, lessons, and roadmap or research updates. Record missing children and unsupported impact claims.
5. **Check each node.** Confirm ID, type, location, status, confidence, rationale, evidence references, parent links, child links, and last verified date.
6. **Detect graph defects.** Look for orphans, stale documentation, conflicting decisions, undocumented code, unimplemented specs, and research with no downstream impact.
7. **Verify references.** Check that linked files, headings, commits, commands, tests, reports, and evidence entries exist when local context allows. Do not claim a link is valid without inspecting it.
8. **Repair if in scope.** Add or update trace links only when the evidence is clear and the change is reversible. Mark uncertain links as low confidence instead of inventing certainty.
9. **Report.** Use the standard Traceability Report format.

## Defect Detection Rules

### Orphaned Artifacts

Flag an artifact when it has no parent and is not an allowed root, or when it has no child despite claiming downstream impact. Recommend one of: link, archive, split, merge, or delete from the registry.

### Stale Documentation

Flag docs when linked files or commands no longer exist, active docs point to superseded decisions, the last verified date predates related implementation changes, or the doc conflicts with current source/test evidence.

### Conflicting Decisions

Flag conflicts between active artifacts that prescribe incompatible architecture, product behavior, APIs, ownership, data models, verification standards, or risk posture. Recommend the smallest decision update that resolves the conflict.

### Undocumented Code

Flag code when it changes meaningful behavior but lacks a parent milestone, spec, ADR, issue, or implementation report. Generated files, trivial helpers, and mechanical churn may inherit the parent module's trace entry.

### Unimplemented Specifications

Flag active specs that have no child milestone, source file, test, or implementation report. Mark partial implementation when only some acceptance criteria have evidence.

### Research With No Downstream Impact

Flag research that has no child reasoning memo, decision record, spec, roadmap update, test plan, or explicit archived status. Recommend linking it to impact, creating a downstream decision, or archiving it as background.

## Repair Guidelines

When adding or updating traceability:

1. Prefer linking existing artifacts over creating new prose.
2. Keep rationale short and evidence-specific.
3. Mark confidence honestly using `../core/08_VERIFICATION_ENGINE.md`.
4. Use `superseded` instead of rewriting history.
5. Preserve canonical IDs from ADRs, tickets, commits, and reports.
6. If a link is plausible but not inspected, record it as `low` confidence or leave it out.

## Checklist

- Scope and artifact types were named.
- Parents and children were followed in both directions.
- IDs, statuses, confidence levels, rationale, and evidence references were checked.
- Missing links were separated from conflicts and staleness.
- Orphaned work, undocumented code, unimplemented specs, and unused research were explicitly considered.
- Local paths, reports, evidence entries, tests, or commits were sanity-checked before being reported valid.
- Recommended actions distinguish must-fix, should-fix, optional, and follow-up research or decision work.

## Output Format

```text
Traceability Report

1. Artifact summary
- Scope:
- Artifacts inspected:
- Graph roots:
- Current statuses:

2. Upstream dependencies
- Artifact:
- Parents:
- Rationale:
- Evidence:

3. Downstream dependencies
- Artifact:
- Children:
- Claimed impact:
- Evidence of impact:

4. Missing links
- Artifact:
- Missing parent/child/evidence/status:
- Why it matters:

5. Conflicting artifacts
- Artifact A:
- Artifact B:
- Conflict:
- Recommended resolution:

6. Stale artifacts
- Artifact:
- Staleness signal:
- Last verified:
- Recommended update:

7. Orphaned work
- Artifact:
- Orphan reason:
- Keep/link/archive recommendation:

8. Verification status
- Verified:
- Partially verified:
- Unverified:
- Commands, sources, or reviews inspected:

9. Confidence assessment
- Overall confidence: high | medium | low
- Confidence by chain segment:
- Main uncertainty:

10. Recommended actions
- Must fix:
- Should fix:
- Optional:
- Follow-up research or decision needed:
```

## Failure Modes

- Treating traceability as a narrative summary instead of a graph of specific artifacts.
- Creating IDs without linking real paths, evidence, or decisions.
- Marking confidence high because the chain is plausible rather than verified.
- Letting old active decisions coexist with newer incompatible decisions.
- Recording research but never linking it to a downstream decision or archiving it.
- Auditing only upstream rationale and ignoring downstream tests, evidence, review, and lessons.
- Demanding per-file bureaucracy for trivial/generated files instead of using module or milestone-level trace entries.
