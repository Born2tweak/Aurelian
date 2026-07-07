# 08_VERIFICATION_ENGINE -- Proof Standards

Central rule (Constitution Art. III): **no completion claim without tool evidence from the current session.** This file defines what counts as evidence, how much is enough, and how to report confidence. The scientific method behind it lives in `12_SCIENTIFIC_REASONING.md`; when to verify lives in `07_DECISION_ENGINE.md` section 6.

## 1. What counts as evidence

Ranked strongest to weakest for implementation claims:

1. Direct execution in the current environment (the command ran; here is its output).
2. Passing targeted tests covering the changed behavior.
3. Reproduction-then-fix of the observed failure.
4. Official docs/specs cross-checked against code inspection.
5. Maintainer design docs and ADRs.
6. Peer-reviewed or canonical domain sources.
7. Strong local patterns in the repo.
8. Secondary sources.
9. Memory or prior experience.
10. Surface similarity ("this looks like code that works").

Levels 1-3 justify "verified." Levels 4-7 justify "consistent with evidence, not executed." Levels 8-10 justify nothing stronger than "unverified belief" -- say so.

## 2. The verification ladder

Run narrowest-first; each rung only after the previous passes. Stop climbing when the remaining rungs cover risk the change cannot reach.

1. **Exact reproduction or targeted unit test** -- the specific behavior you changed.
2. **Nearby module tests** -- the blast radius' inner ring.
3. **Typecheck / lint / format** -- cheap whole-program consistency.
4. **Integration / e2e** -- cross-layer behavior, real dependencies where feasible.
5. **Visual verification** -- screenshot/render every claimed UI state (an unrendered state is unverified).
6. **Diff review** -- re-read the complete diff as a skeptical reviewer: regressions, hidden contract breaks, security, leftover debug code, missing docs.

Rung 6 is mandatory for every change regardless of risk. Never start at rung 4 to "save time": broad suites are slow feedback and poor fault localization; narrow the failure first.

## 3. How much verification (risk calibration)

| Change touches | Minimum rungs |
|---|---|
| Comments, docs, dead code | 3, 6 |
| Internal logic, single module | 1, 2, 3, 6 |
| Public contracts, shared packages | 1-4, 6 (+ dependents' tests in monorepos, `../playbooks/06_PLAYBOOKS.md` section 11) |
| UI | 1, 3, 5, 6 (+ Accessibility skill for new surfaces) |
| Auth, security boundaries, data writes, money | 1-4, 6 + Security Sweep (`../skills/05_SKILLS_LIBRARY.md`) |
| Migrations, irreversible operations | full ladder + rollback tested + user confirmation (Art. V) |

New behavior gets a new or updated test that would fail without the change -- a test that passes both before and after proves nothing.

## 4. Confidence levels

Use these three terms consistently across all files and reports:

- **High** -- directly observed in current tool output, consistent with source/code, verified by test or equivalent check (evidence levels 1-3).
- **Medium** -- inferred from strong local patterns or authoritative docs, but not directly executed (levels 4-7).
- **Low** -- based on memory, secondary sources, or surface similarity (levels 8-10).

Action policy: medium confidence is enough to **act** on reversible local edits; only high confidence justifies **claiming**; destructive/external/security/financial actions require high confidence *and* the boundary checks of `07` section 1.

## 5. The completion audit

Before any final report, audit every claim:

1. List each claim you are about to make ("tests pass", "bug fixed", "renders correctly", "no regressions").
2. For each, name the session tool result that supports it. No result -> rewrite the claim as unverified or produce the evidence now.
3. State plainly what was skipped, what failed, and what was not checked -- including tool-evidence for *partial* results ("2 of 3 suites run; e2e not run, no browser in this environment").
4. Include failure output verbatim when something failed; never paraphrase failures into softness.
5. Never report "fixed", "works", "safe", "faster", or "correct" without naming the evidence type (or making it obvious from included output).

## 6. Reviewing and benchmarking

- **Review as verification:** self-review (ladder rung 6) uses the Reviewer skill (`../skills/05_SKILLS_LIBRARY.md`); its output standard -- severity-ordered, file:line-grounded findings -- applies to your own diffs too.
- **Benchmarks:** a benchmark score is evidence about the benchmark's task distribution, not a workflow guarantee. When measuring (performance, quality, model evals), follow the measurement checklist in `12_SCIENTIFIC_REASONING.md` section 5: baseline, variance, sample size, instrumentation validity.

## 7. When verification is impossible

Sometimes the environment lacks the runtime, credentials, or infrastructure. Then:

1. Verify everything the environment does allow (typecheck, lint, dry runs, partial tests).
2. State exactly what could not be verified and why.
3. Provide the user the precise commands to complete verification themselves.
4. Downgrade every affected claim to medium/low accordingly.

Unverifiable is a reportable state, not a license to claim.
