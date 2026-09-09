# Reliability and research

[Back to the overview](../README.md)

Aurelian treats reliability as something to investigate with evidence. Instructions, passing tests, and an execution log answer different questions. None alone establishes that the final result satisfies the user's objective.

## Development cases

These cases come from separate Runtime, Trust Core, and KinematicIQ development records inspected on September 9, 2026. They explain design motivations; the underlying source and raw session logs are not bundled here. Commit identifiers refer to those separate repositories.

### Recovery that consistently did nothing

An interrupted Runtime worker could leave its lease active. The restarted scheduler treated the work as already running and selected nothing. A determinism test could still pass because two resumed runs produced the same empty outcome.

The revised check requires the expected milestones to complete without duplicate completion. The recorded recovery change reclaims the restarting worker's own lease while preserving peer ownership boundaries.

Evidence locators: Runtime `EXECUTION_LEDGER.md`, findings `DEF-RT-002` and `F-003`; `tests/test_loop_end_to_end.py`; execution-loop commit `bf58456` and continuation `9d62679`.

Agreement establishes consistency; successful recovery also requires the intended work to finish.

### An upstream label mismatch affected later verification

A KinematicIQ trial wrote a camera-source value of `real-camera` where the frame adapter required `live-camera`. Verification rejected the camera milestone, and the subsequent upload milestone failed its whole-repository check.

The correction normalized the label and produced new completion evidence for both milestones. This illustrates why the stage reporting a failure can differ from the stage that introduced it.

Evidence locators: KinematicIQ candidate `04b10c9`, subsequent candidate `db2fb87`, correction `f83f65f`; Runtime `EXECUTION_LEDGER.md`, July 28 continuation; recorded trial execution results.

These trials used predefined implementation functions. They demonstrate orchestration and candidate verification rather than a model independently inventing the feature sequence.

### Evidence for the wrong candidate

Trust Core binds evidence to an execution and repository snapshot. Its tests exercise changes after capture, mismatched execution context, and foreign evidence. The Runtime orders implementation and commit before snapshot capture.

Evidence locators: Trust Core `src/aurelian_trust/core.py`, `verify` and `complete`; `tests/test_core.py`; `tests/test_core_semantics.py`; inspected revision `4f3c8d8`.

The corresponding framework practice is preserving requirement, artifact, and verification links through the [traceability contract](../core/14_TRACEABILITY_ENGINE.md).

## Verification scope

A September 9, 2026 check of the separate Runtime ran `test_lease.py`, `test_recovery.py`, `test_failure_policy.py`, and `test_authority_boundary.py`: **37 tests and 4 subtests passed**. This is a dated result for selected tests, not a badge for this Markdown repository, a full-suite rerun, a fresh execution of every historical trial, or proof of production reliability.

The [evaluation protocol](../evaluation/17_EVALUATION_PROTOCOL.md) defines a comparison between an agent with and without Aurelian. The [benchmark protocol](../evaluation/19_BENCHMARK_PROTOCOL.md) adds measurement guidance. These are evaluation procedures, not reported benchmark wins.

## Potential research connections

Agent workflows connect task interpretation, context selection, planning, tool choice, execution, observations, subsequent actions, and verification. Instrumenting those stages could help distinguish an upstream cause from where an error becomes visible.

Questions to investigate include:

- Does changing supplied context resolve a failure while holding the task and tools fixed?
- Does correcting a tool observation change downstream behavior?
- Can an evaluator distinguish stale evidence from evidence for the current candidate?
- Does independent review expose requirement failures missed by the implementation agent's tests?
- Does recovery resume intended work without repeating completed side effects?

Define outcomes and interventions in advance, preserve intermediate observations, repeat runs where model variation matters, and record failures as well as successes. Log observable actions and outputs; do not assume access to hidden model reasoning.

These are potential extensions of the engineering work. Causal diagnoses and measured improvements require their own experimental evidence.
