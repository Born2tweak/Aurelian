# Traceability Graph

## Purpose

Track the knowledge graph connecting project artifacts from vision through discovery, research, reasoning, decisions, specs, milestones, source files, tests, evidence, review, lessons, and updated research.

Do not invent links. Record only inspected artifacts, clearly marked assumptions, or explicit placeholders for missing links.

## Status Values

- `planned`: expected but not started.
- `active`: current and used for decisions.
- `verified`: supported by current evidence.
- `superseded`: replaced by a newer artifact.
- `archived`: retained for history but not used for active decisions.

## Confidence Values

- `high`: directly observed in current command output, tests, reviews, or equivalent evidence.
- `medium`: supported by strong local patterns, canonical docs, or maintained project records but not freshly executed.
- `low`: plausible, incomplete, stale, or not yet inspected.

## Artifact Entry Format

```text
### TRACE-ID: Artifact Title

- Type: vision | discovery | research | engineering-reasoning | decision-record | technical-spec | product-spec | milestone | source-file | test-evidence | evidence | review | lesson | roadmap-update | commit | implementation-report
- Location:
- Status: planned | active | verified | superseded | archived
- Confidence: high | medium | low
- Parents:
- Children:
- Rationale:
- Evidence references:
- Owner/tool:
- Last verified:
- Supersedes:
- Superseded by:
```

## Canonical Chain

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

Small tasks may start from a bug report, issue, failing test, or user request instead of a full vision artifact. The chain is complete enough when a future agent can answer why the work exists, what evidence supports it, what changed because of it, and what must be revisited if it changes.

## Artifact Graph

Add newest active entries first.

## Missing Links

Track known gaps without inventing links.

```text
### YYYY-MM-DD: Missing Link Title

- Artifact:
- Missing: parent | child | evidence | status | confidence | location
- Why it matters:
- Recommended action:
- Owner/tool:
```

## Conflicts

Track active artifacts that disagree until a decision resolves them.

```text
### YYYY-MM-DD: Conflict Title

- Artifact A:
- Artifact B:
- Conflict:
- Evidence:
- Recommended resolution:
- Status: planned | active | verified | superseded | archived
```

## Traceability Reports

Use this format for audits and milestone closeouts.

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
