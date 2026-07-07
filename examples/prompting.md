# Example: Prompting an Agent

Goal: get a coding agent to fix a flaky test in CI.

## Bad prompt

```
The tests are flaky, can you fix them? It's probably something with async.
Make sure everything passes. Also clean up anything else that looks off.
Thanks!
```

**Why it fails:** No goal an agent can verify ("flaky" -- which test, how often, what output?). No context (where's CI config? how to run the suite locally?). A guess presented as a diagnosis ("probably async") that anchors the agent toward one hypothesis before evidence (`../core/12_SCIENTIFIC_REASONING.md` section 2). "Clean up anything that looks off" is an open invitation to unbounded blast radius (Art. IV, VI). No done-when -- "everything passes" is true the moment the flake doesn't fire.

## Good prompt

```
Goal: fix the flaky test `checkout.spec.ts > "applies coupon at checkout"`.
It fails roughly 1 in 5 CI runs but passes locally for everyone.

Context: CI logs from three failing runs are attached. Run the suite with
`npm test`; this single file with `npx vitest run checkout.spec.ts`. CI
uses 2 vCPUs (dev machines have 10+), so timing differs. The test spins up
a mock payment server in beforeEach.

Constraints: do not increase timeouts as the fix -- that's been tried twice
and the flake returned. Do not modify other tests. Do not touch the
production checkout code unless you find a real race in it -- if you do,
stop and report the race before patching production code.

Done when: you can make the failure reproduce deliberately (e.g., under
constrained CPU or forced scheduling), explain the mechanism, and show 20
consecutive green runs of the file with your fix under the same conditions
that reproduced it. Report cause, mechanism, fix, and evidence.
```

**Why it works:** The four load-bearing parts of a delegation prompt are all present -- **goal** (one named test, with observed failure rate), **context** (commands, logs, the CPU asymmetry that explains "passes locally"), **constraints** (what NOT to do, including a boundary that escalates production changes back to the user -- Art. V), and **done-when** (a falsifiable standard: reproduce first, then 20 green runs *under the reproducing conditions*, not on the developer's fast machine). Note it shares the failed-timeout history -- negative knowledge that saves the agent from re-walking dead ends, and it demands mechanism, blocking a pattern-matched sleep() patch (`../core/03_EXECUTION_ENGINE.md` section 2.5).
