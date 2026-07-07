# 06_PLAYBOOKS -- End-to-End Workflows by Project Type

Playbooks compose the algorithms of `../core/03_EXECUTION_ENGINE.md` and the skills of `../skills/05_SKILLS_LIBRARY.md` into full workflows. Every playbook begins with **Setup/Project Decomposition** (`../skills/05_SKILLS_LIBRARY.md`) and ends with the standard close: verify (`../core/08_VERIFICATION_ENGINE.md`), self-review (Reviewer, `../skills/05_SKILLS_LIBRARY.md`), evidence-grounded report, durable-lesson capture (`../core/04_MEMORY_SYSTEM.md`). Those shared bookends are not repeated below -- only what is distinctive per project type.

## 1. SaaS application build

1. Decompose into user-visible vertical slices; build a **walking skeleton** first: one thin path from UI -> API -> DB -> deploy, working end to end. Integration risk dies here, not in week four.
2. Order milestones by risk: third-party integrations (auth provider, billing, email) get spiked earliest.
3. Per slice: Feature algorithm (`../core/03_EXECUTION_ENGINE.md` section 1) with real states (empty/loading/error) from the start -- retrofit is costlier.
4. Auth and billing changes always get a Security Sweep before merge.
5. Checkpoint with the user after each slice -- a demoable increment, not a progress narrative.

## 2. AI-powered application build

Everything in section 1, plus:

1. Treat the model as an unreliable dependency: design for wrong, slow, and refused outputs from day one (timeouts, retries, fallbacks, user-visible uncertainty).
2. Build the **eval harness before the feature**: a small fixed set of input -> expected-quality cases you re-run after every prompt or model change. Prompt edits without evals are guesses.
3. Keep prompts in versioned files, not string literals; log model inputs/outputs (scrubbed of secrets) for debugging.
4. Cost and latency are product features: measure per-request tokens early.
5. Security Sweep extends to prompt injection: any user text or third-party content entering a prompt is a trust boundary.

## 3. React application

1. Map the existing state management, routing, and data-fetch conventions first; extend, don't introduce a second pattern.
2. Component work: colocate state at the lowest sufficient level; lift only when sharing forces it.
3. Follow UI algorithm (`../core/03_EXECUTION_ENGINE.md` section 8) -- every claimed state visually verified -- plus the Accessibility skill on new surfaces.
4. Derive state where possible instead of syncing it; effects are a last resort, and each one must state what external system it synchronizes with.
5. Performance work only via the Performance skill (profile first -- React DevTools, not intuition).

## 4. Next.js application

Everything in section 3, plus:

1. Choose rendering per route deliberately (static / server-rendered / client) based on data freshness and personalization -- record the choice and reason.
2. Respect the server/client boundary: secrets and heavy dependencies stay server-side; check what each client component pulls into the bundle.
3. Data fetching follows the framework's current canonical pattern -- verify against current docs (Research skill), because this framework's conventions move fast.
4. Verify both build output and runtime behavior; a passing dev server does not prove a passing production build.

## 5. CLI tool

1. Design the interface first: commands, flags, arguments, exit codes, and `--help` text -- this is the API contract.
2. Follow platform conventions: stdout for data, stderr for diagnostics; nonzero exit on failure; support piping; no interactive prompts when stdin isn't a TTY.
3. Errors are UX: every failure message says what happened and what to try.
4. Verify by running the actual binary against real invocations, including bad input, in a clean environment.

## 6. Backend service

1. Define the service contract first: endpoints/handlers, inputs, outputs, error semantics, idempotency.
2. Build in observability from the start: structured logs with request IDs, health endpoint, key metrics. An unobservable service is undebuggable in production.
3. Every external call gets a timeout and a failure story (retry? circuit-break? degrade?).
4. State the concurrency model explicitly; shared mutable state is guilty until proven safe.
5. Verification ladder runs to integration tests against real (containerized) dependencies, not just mocks.

## 7. Database work

1. Read the existing schema and its access patterns before proposing changes; the schema is a public contract for every consumer.
2. All schema changes ship as migrations (never manual edits), each with a rollback path, per the Migration algorithm (`../core/03_EXECUTION_ENGINE.md` section 9): expand -> migrate -> contract.
3. Destructive operations (drop, truncate, irreversible transforms) require explicit user confirmation (Constitution Art. V) and a tested backup.
4. Index decisions follow evidence: query plans on realistic data volume, not guesses.
5. Test migrations against a copy with production-shaped data; empty-database success proves little.

## 8. API design

1. Design from the consumer inward: write the ideal calling code first, then the API that supports it.
2. Contracts are promises (`09` section 1): version deliberately; additive changes are cheap, breaking changes need a migration story before release.
3. Be consistent above all -- naming, error shapes, pagination, auth -- internal consistency beats external fashion.
4. Error responses are part of the contract: stable codes, human-readable messages, no stack traces across the boundary.
5. Document with runnable examples per request/response; verify them by execution.

## 9. Migration project (framework/language/infra)

The Migration algorithm (`../core/03_EXECUTION_ENGINE.md` section 9) at project scale:

1. Inventory the full surface (automated search, not memory); classify each item: mechanical / needs judgment / needs redesign.
2. Migrate one representative vertical slice end-to-end first to flush unknown unknowns; only then estimate and batch the rest.
3. Old and new run side by side behind a switch until evidence retires the old (strangler pattern).
4. Mechanical batches get spot-review plus full test runs; judgment items get individual review.
5. Track a burn-down list in the repo so the migration survives session boundaries (`../core/04_MEMORY_SYSTEM.md` section 2).

## 10. Legacy codebase work

1. Assume every oddity is load-bearing until proven otherwise; the code is the spec, and the spec has customers.
2. Before changing anything: write characterization tests that pin current behavior -- including behavior that looks like a bug (it may be depended upon; ask before "fixing").
3. Change in the narrowest possible seams; resist structural churn (Constitution Art. IV, XII).
4. Improve only what the task touches ("boy scout" within the diff, never beyond it).
5. Document discovered landmines in the project instruction file as you go (`../core/04_MEMORY_SYSTEM.md` section 3).

## 11. Monorepo work

1. Establish the ownership map first: which packages exist, who owns them, how they depend on each other. Never edit across ownership boundaries without flagging it.
2. Scope reads and instructions per directory (folder-level instruction files, `../core/04_MEMORY_SYSTEM.md` section 1); deny generated/vendored trees from context.
3. Blast-radius analysis is mandatory: a shared-package change is verified by building/testing its **dependents**, not just itself.
4. Use the repo's own task runner and affected-target tooling for verification; hand-picked test scopes miss dependents.
5. Cross-cutting changes follow the Migration playbook (section 9), not one giant commit.
