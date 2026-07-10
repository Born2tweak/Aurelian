# 14_TRACEABILITY_ENGINE -- Knowledge Graph And Evidence Chain

The traceability engine connects every engineering artifact into one evidence-backed knowledge graph. It extends `04_MEMORY_SYSTEM.md`, `08_VERIFICATION_ENGINE.md`, `12_SCIENTIFIC_REASONING.md`, and `13_MODEL_ROUTER.md`: memory decides what should persist, verification decides confidence, scientific reasoning decides what counts as evidence, and traceability records how one artifact affects the next.

Purpose: an agent or maintainer should be able to start from any implementation decision and walk upstream to the vision, research, reasoning, and decision record that justified it, then walk downstream to source files, tests, evidence, reviews, lessons, and updated research.

## 1. Traceability Contract

Every durable engineering artifact should expose this metadata, either in front matter, a heading block, a table row, a log entry, or a linked `.aurelian/traceability.md` registry entry:

```text
Trace ID:
Artifact type:
Location:
Status: planned | active | verified | superseded | archived
Confidence: high | medium | low
Parents:
Children:
Rationale:
Evidence references:
Owner/tool:
Last verified:
Supersedes:
Superseded by:
```

Rules:

1. **Trace IDs are stable.** Do not recycle an ID after an artifact is renamed, moved, superseded, or archived.
2. **Parents explain why the artifact exists.** A source file can have a spec, milestone, ADR, bug report, or research claim as a parent.
3. **Children show downstream impact.** Research with no child may be valid background, but it has no demonstrated engineering impact.
4. **Evidence references are pointers, not copied logs.** Link to `.aurelian/evidence-log.md`, test output, review reports, screenshots, commits, issues, source paths, or external sources.
5. **Confidence follows `08_VERIFICATION_ENGINE.md`.** High confidence requires current observed evidence, tests, or equivalent checks; medium can come from strong local patterns or authoritative docs; low is unverified.
6. **Status is explicit.** Stale, replaced, or abandoned artifacts become `superseded` or `archived`; do not leave dead decisions looking active.

## 2. Artifact Types

Use these types consistently:

| Type | Examples | Typical parents | Typical children |
|---|---|---|---|
| `vision` | product thesis, project brief, business goal | user objective | discovery, project bible |
| `discovery` | repo audit, stakeholder notes, gap analysis | vision | research, specs, roadmap |
| `research` | research dossier, source table, domain model | discovery, open question | reasoning, ADR, spec |
| `engineering-reasoning` | synthesis memo, tradeoff analysis, feasibility note | research, discovery, repo audit | decision record, spec |
| `decision-record` | ADR, decision log entry | reasoning, research, evidence | spec, milestone, roadmap |
| `technical-spec` | design spec, API spec, architecture spec | decision record, research | milestone, source file, test plan |
| `product-spec` | product bible, UX spec, acceptance criteria | vision, research, decision record | milestone, source file, review |
| `milestone` | roadmap item, implementation plan | spec, decision record | source file, report, commit |
| `source-file` | code, config, migration, schema | milestone, spec, ADR | test, commit, review |
| `test-evidence` | unit test, integration test, build/lint log, screenshot | source file, spec, milestone | evidence, review |
| `evidence` | evidence log entry, command output, source inspection | test, source file, review | verification status, review |
| `review` | code review, review swarm report, audit report | source file, evidence, milestone | lesson, follow-up milestone |
| `lesson` | learning report, retrospective, durable rule | review, evidence | updated research, memory, roadmap |
| `roadmap-update` | milestone queue change, scope change, risk reprioritization | evidence, review, lesson | milestone |
| `commit` | local or remote commit | source file, test evidence, report | release note, review, deployment evidence |
| `implementation-report` | closeout, milestone report | milestone, source files, tests | review, lesson, roadmap-update |

## 3. Canonical Lifecycle Chain

A full implementation chain should be walkable in both directions:

```text
Vision
-> Discovery
-> Research
-> Engineering Reasoning
-> Decision Record
-> Technical Specification
-> Milestone
-> Source Files
-> Tests
-> Evidence
-> Review
-> Lessons Learned
-> Updated Research
```

Not every task needs every node. Small fixes may start at a bug report, issue, or failing test. The rule is not ceremony; the rule is that every durable artifact must have enough upstream and downstream links to answer:

1. Why does this exist?
2. What evidence supports it?
3. What changed because of it?
4. What would become stale if it changed?

## 4. ID Scheme

Use short, sortable IDs. Prefer the artifact class plus date or sequence:

```text
VIS-YYYYMMDD-short-name
DISC-YYYYMMDD-short-name
RES-YYYYMMDD-short-name
REAS-YYYYMMDD-short-name
ADR-YYYYMMDD-short-name
SPEC-YYYYMMDD-short-name
MS-YYYYMMDD-short-name
SRC-path-or-module
TEST-path-or-suite
EVID-YYYYMMDD-short-name
REV-YYYYMMDD-short-name
LESSON-YYYYMMDD-short-name
ROAD-YYYYMMDD-short-name
COMMIT-shortsha
```

When a project already has ADR numbers, issue IDs, ticket IDs, or commit SHAs, keep those canonical IDs and add them as aliases in the traceability registry.

## 5. Graph Operations

### Follow Dependencies

1. Start from the target artifact.
2. Walk parents until reaching the originating vision, user request, issue, or discovery artifact.
3. Walk children until reaching tests, evidence, review, lessons, roadmap updates, or release artifacts.
4. Check that every status transition is evidence-backed.
5. Stop at archived or superseded nodes unless the question is historical.

### Identify Orphaned Artifacts

An artifact is orphaned when it has no parent and no clear root role, or no child despite claiming downstream impact.

Root artifacts allowed without parents:

- Vision or project brief.
- User request or issue imported as a root objective.
- External standard or canonical source recorded as a resource.

Everything else needs at least one parent.

### Detect Stale Documentation

Documentation is stale when:

1. It points to source files, commands, APIs, tests, or dependencies that no longer exist.
2. Its parent decision, research, or spec is superseded but the doc still claims active status.
3. Its `Last verified` date is older than a related source-file or decision change that could invalidate it.
4. It conflicts with current test evidence, review findings, or implementation reports.

### Identify Conflicting Decisions

Two artifacts conflict when they prescribe incompatible behavior, ownership, architecture, data model, UX, verification standard, or risk posture.

Resolve conflicts by precedence:

1. Current user instruction and project non-negotiables.
2. Active accepted ADR or decision record.
3. Verified source and tests.
4. Current project bible, technical spec, and roadmap.
5. Older docs, unverified reports, and archived notes.

Do not silently choose between conflicting active decisions. Record the conflict and recommend a decision update.

### Detect Undocumented Code

Source is undocumented when it implements behavior that:

1. Has no parent milestone, spec, ADR, issue, or implementation report.
2. Changes a public contract, data model, security boundary, user workflow, or product behavior without a decision or spec link.
3. Has tests or evidence but no rationale.

Small mechanical files can inherit traceability from a parent module or milestone. Do not require per-file ceremony for generated files or obvious local helpers.

### Detect Unimplemented Specifications

A spec is unimplemented when it has active status but no child milestone, source file, test, or implementation report. A spec is partially implemented when children exist but the evidence only covers part of its acceptance criteria.

### Detect Research With No Downstream Impact

Research has no demonstrated impact when it has no child reasoning memo, decision record, spec, roadmap update, test plan, or explicit archived status. Either link it to the decision it informed, create the missing downstream artifact, or archive it as background.

## 6. Traceability Report

Use this report for audits, milestone closeouts, stale-doc checks, and review swarms:

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

## 7. Integration Points

Project templates should keep `.aurelian/traceability.md` as the graph registry. Other durable files remain specialized:

- `.aurelian/project-state.md` tracks current work.
- `.aurelian/decision-log.md` tracks decisions.
- `.aurelian/evidence-log.md` tracks observations.
- `.aurelian/resource-index.md` tracks canonical resources.
- `.aurelian/traceability.md` links artifacts across those files and the repository.

For large projects, `.aurelian/traceability.md` can be an index that points to per-domain graph files. Keep the entry format stable so agents can compare and audit links mechanically.

## 8. Quality Bar

A traceability entry is useful only if it changes future behavior. Before adding or updating one, check:

1. Does it name a real artifact path, source, command, commit, report, or decision?
2. Can a future agent follow it without guessing?
3. Does it distinguish evidence from rationale?
4. Does it mark confidence and status honestly?
5. Would an upstream change reveal what downstream work must be revisited?

If the answer is no, write less and link better.
