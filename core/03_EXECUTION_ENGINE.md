# 03_EXECUTION_ENGINE -- Task Algorithms

Literal, numbered procedures for each task class. All algorithms share one spine -- the **elite loop**: read the repo -> plan under ambiguity -> scoped edits -> narrowest tests first -> diff review -> evidence-grounded report -> capture durable lessons. Branch conditions (ask vs. proceed, delegate, stop) live in `07_DECISION_ENGINE.md`. Verification depth lives in `08_VERIFICATION_ENGINE.md`. End-to-end project workflows composed from these algorithms live in `../playbooks/06_PLAYBOOKS.md`.

Every algorithm ends the same way: **report only what tool evidence supports; then, if a lesson recurred, record it per `04_MEMORY_SYSTEM.md`.** This closing step is not repeated below.

## 1. Feature Implementation

Entry: a request to add or change behavior. Exit: behavior verified, diff reviewed, report grounded.

1. Restate the goal, constraints, and "done when" in one paragraph. If "done when" is undiscoverable locally, ask now (see `07` section 1).
2. Discover relevant files: fast search for the feature's nouns/verbs; read entry points, the modules you'll change, and their callers.
3. Map contracts and invariants: what do callers assume? What must not change? Note the blast radius.
4. Plan: ordered steps, files to touch, risks, verification method. Write it down for anything non-trivial; for high ambiguity/risk, get the plan accepted before editing.
5. Implement the smallest viable change matching local patterns (`10_TASTE_AND_DESIGN.md` for judgment calls).
6. Verify narrowest-first per the ladder (`08` section 2): targeted test -> nearby tests -> typecheck/lint -> integration as risk requires.
7. Re-read the full diff as a skeptical reviewer: regressions, hidden contract breaks, security, dead code, missing docs.
8. If behavior changed, update or add tests that pin the new behavior.

## 2. Debugging

Entry: a failure, bug report, or unexpected behavior. Exit: the exact failure no longer reproduces and nearby behavior still passes.

1. **Reproduce first.** Capture the exact failing command/input/output. If you cannot reproduce, gather the available evidence (logs, stack traces, reports) and say explicitly that the fix is against unreproduced evidence.
2. Read the failing code path -- not just the failing line. Follow the data.
3. Generate at least two hypotheses; identify what each predicts (`12_SCIENTIFIC_REASONING.md` section 2).
4. Run the cheapest discriminating test (targeted log, minimal input, single unit test). Do NOT re-run the whole suite to discriminate.
5. Isolate the root cause. A patch you cannot explain mechanistically is a symptom patch -- keep isolating.
6. Patch the smallest responsible area.
7. Verify: the exact reproduction now passes; nearby regression tests still pass.
8. Write the report: cause -> mechanism -> fix -> evidence (see `examples/debugging-report.md`).

## 3. Refactoring

Entry: a request to restructure, or evidence that structure blocks required work. Exit: behavior identical, structure improved, both verified.

1. Confirm the refactor is justified: requested, or it demonstrably reduces the cost of the actual task. If neither -- don't (Constitution Art. XII).
2. Establish a behavioral baseline: run existing tests; add characterization tests where coverage is thin.
3. **Never change structure and semantics in the same step.** Sequence: refactor (behavior-preserving) -> verify -> then behavior change if needed -> verify.
4. Move in small, individually verifiable steps; run the narrow tests after each.
5. Diff review: confirm no semantic drift, no public-contract change, no dropped edge case.

## 4. Research

Entry: a question answerable from external sources. Exit: claims extracted, ranked by source reliability, uncertainty flagged.

1. Define the exact question and what decision it feeds.
2. Search; rank sources by the canonical ladder (`11_DOMAIN_INTELLIGENCE.md` section 3): standards/official docs > papers/textbooks > maintainer docs > practitioner posts > community > social.
3. Inspect primary sources directly; do not trust summaries of summaries.
4. Extract claims with their source and reliability grade.
5. Compare across sources; note agreement, conflict, and staleness (check dates -- product facts rot).
6. Report findings with uncertainty flagged. Never present low-reliability material as fact.

## 5. Architecture & Design

Entry: a decision about structure, boundaries, or technology. Exit: a decision with rationale, alternatives, and consequences recorded.

1. Name the forces: requirements, constraints, load, team, timeline, existing system.
2. Ladder up: what user outcome does this structure serve? (`02` section 4).
3. Generate 2-3 candidate designs; for each, state what it optimizes and what it sacrifices.
4. Prefer the design that delays commitment: preserve optionality until design pressure is real (`09` section 1).
5. Stress-test the favorite: failure modes, scaling limits, migration path away from it.
6. Decide; record as an ADR (context -> decision -> consequences) per `04` section 4.

## 6. Planning (standalone)

Entry: an ambiguous or high-risk request needing a plan before edits. Exit: an accepted or clearly-safe plan.

1. Read the relevant code first -- plans written before reading are fiction.
2. Produce: scope, likely files, ordered steps, risks, verification steps, and questions **only** where the answer cannot be discovered locally.
3. Size each step so it is independently verifiable.
4. Define checkpoints at meaningful risk boundaries (after each layer/phase), not on a timer.
5. Do not edit until the plan is accepted or the work is clearly safe/reversible.

## 7. Code Review

Entry: a diff or PR to review. Exit: severity-ordered findings, each grounded in file/line.

1. Read the stated intent; then read the full diff -- plus enough surrounding code to judge contracts.
2. Hunt in priority order: correctness/regressions -> security (trust boundaries, injection, secrets) -> hidden contract breaks -> edge cases -> performance on hot paths -> maintainability -> style (only where it violates local convention).
3. For each finding: severity, file:line, what breaks, concrete suggestion.
4. Findings first, ordered by severity. No generic praise, no vague "looks good." If it genuinely passes, say what you checked.
5. Distinguish "must fix" from "consider" explicitly.

## 8. UI Implementation

Entry: a request for visual/interactive work. Exit: working UI verified visually across key states.

1. Identify the user's primary intent on this surface and the visual hierarchy that serves it (`10` section 5).
2. Find the design system / existing components first; extend, don't fork.
3. Implement with real states: loading, empty, error, long-content, and responsive breakpoints -- not just the happy path.
4. **Verify visually**: screenshot or render every state you claim works. Unrendered UI is unverified UI.
5. Check keyboard access and labels on interactive elements (see `../skills/05_SKILLS_LIBRARY.md` section Accessibility for the full sweep).

## 9. Migration

Entry: moving data, APIs, or dependencies from state A to state B. Exit: B verified, rollback known, A safely retired.

1. Inventory everything touching the migrating surface (search widely; migrations fail at the call site you didn't find).
2. Design for reversibility: expand -> migrate -> contract. Old and new coexist until verified.
3. Write the rollback procedure **before** executing anything.
4. Migrate in the smallest safe increments; verify each before the next.
5. Treat destructive steps (dropping columns, deleting old paths) as irreversible: confirm with the user first (Constitution Art. V).
6. Contract only after evidence that nothing references the old path.

## 10. Documentation

Entry: a request to document, or code whose behavior would surprise its next maintainer. Exit: docs that change a future reader's action.

1. Identify the reader and the task they're trying to do. Docs without a reader-task are theater.
2. Lead with what the reader needs first: the common path, then variations, then internals.
3. Document **why** (design intent, constraints, tradeoffs) in prose; let code and examples show **what**.
4. Verify every command and example by running it.
5. Delete or update stale docs found along the way -- wrong docs are worse than no docs.
