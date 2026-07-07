# 05_SKILLS_LIBRARY -- Installable Skills

Standardized, self-contained skills. Each follows one schema: **Purpose / Trigger / Algorithm / Checklist / Example / Failure Modes / Output Format.** Install them per your tool's skill mechanism (`../adapters/`); load a skill's body only when its trigger fires (progressive disclosure). Skills compose the algorithms of `../core/03_EXECUTION_ENGINE.md` with the standards of `../core/08_VERIFICATION_ENGINE.md`; copy-paste prompt versions live in `../prompts/13_PROMPT_LIBRARY.md`.

---

## Security Sweep

- **Purpose:** Check shipped work the way a careful security reviewer would, before it merges.
- **Trigger:** Any diff touching auth, input handling, shell/file/network operations, dependencies, config, secrets, or data at a trust boundary. Also before any release.
- **Algorithm:**
  1. Identify trust boundaries the diff touches or creates (user input, network, files, subprocesses, third-party data).
  2. Check auth and authorization on every new or changed path -- who can reach this, and should they?
  3. Check input validation and output encoding at each boundary (injection: SQL, shell, path, template, XSS).
  4. Check secrets: hardcoded credentials, secrets in logs, env vars leaked to clients, committed .env files.
  5. Check filesystem/shell/network calls for unsanitized arguments and overly broad permissions.
  6. Check dependency and config changes: new packages (typosquats, maintenance status), loosened settings.
  7. Run security linters/tests if the repo has them.
- **Checklist:** trust boundaries listed / authz on changed paths / injection surfaces checked / no secrets in code/logs / shell/fs args sanitized / deps reviewed / linters run.
- **Example:** A diff adds an export endpoint. Sweep finds it reads `req.query.path` into `fs.readFile` -- path traversal. Finding: `HIGH, api/export.ts:41, unsanitized path from user input reaches fs; suggest resolving against a whitelisted root.`
- **Failure modes:** reviewing only the diff without its callers; reporting theoretical risks with no reachable path; drowning real findings in style nits.
- **Output format:** actionable findings only, severity-ordered, each with file:line, the concrete risk, and a suggested fix. If clean, state exactly what was checked.

---

## Planner

- **Purpose:** Convert ambiguity into executable, verifiable work.
- **Trigger:** Vague requests, multi-file changes, high-risk edits, or any task where the wrong interpretation wastes significant work.
- **Algorithm:** `../core/03_EXECUTION_ENGINE.md` section 6. In brief: read the relevant code first; produce scope, likely files, ordered verifiable steps, risks, verification method; ask only what local evidence cannot answer; hold edits until accepted or clearly safe.
- **Checklist:** code read before planning / every step independently verifiable / risks named / "done when" explicit / questions minimized.
- **Example:** see `../examples/planning.md`.
- **Failure modes:** planning from the issue text alone; steps like "implement the feature" (not executable); asking the user things `grep` could answer.
- **Output format:** Goal / Scope (in/out) / Steps (numbered, each with verification) / Risks / Done-when / Open questions (only user-answerable ones).

---

## Reviewer

- **Purpose:** High-signal review of a diff or PR that catches what matters.
- **Trigger:** Any completed diff -- yours (self-review before reporting) or others'.
- **Algorithm:** `../core/03_EXECUTION_ENGINE.md` section 7 (intent -> full diff + context -> hunt by severity -> grounded findings).
- **Checklist:** read surrounding code, not just the diff / correctness before style / every finding has file:line / must-fix vs consider separated / no vague approval.
- **Example:** see `../examples/code-review.md`.
- **Failure modes:** "LGTM" without reading; nitpicking style while missing a regression; findings without locations or suggestions.
- **Output format:** findings first, severity-ordered (blocker/major/minor/nit), each: `severity, file:line, what breaks, suggestion`. Close with what was verified.

---

## Architect

- **Purpose:** Make structural decisions that survive contact with the future.
- **Trigger:** New system/module design, technology selection, boundary disputes, "how should we structure X".
- **Algorithm:** `../core/03_EXECUTION_ENGINE.md` section 5 (forces -> user outcome -> 2-3 candidates with tradeoffs -> prefer delayed commitment -> stress-test -> ADR).
- **Checklist:** >=2 real alternatives considered / each option's sacrifice named / migration path away from the choice exists / decision recorded as ADR (`../core/04_MEMORY_SYSTEM.md` section 4).
- **Example:** Choosing queue vs. cron for background jobs: candidates compared on failure semantics, ops burden, and reversal cost -- not on fashion.
- **Failure modes:** pattern worship (choosing microservices/event-sourcing because famous); designing for imaginary scale; presenting one option as inevitable.
- **Output format:** Forces / Options (each: optimizes/sacrifices) / Recommendation with rationale / Consequences / ADR draft.

---

## Debugger

- **Purpose:** Find and fix root causes with evidence, not pattern-matched patches.
- **Trigger:** Failing test, bug report, unexpected behavior, production incident.
- **Algorithm:** `../core/03_EXECUTION_ENGINE.md` section 2 (reproduce -> read the path -> >=2 hypotheses -> cheapest discriminating test -> isolate -> minimal patch -> verify exact failure + neighbors).
- **Checklist:** reproduction captured (or absence stated) / root cause explained mechanistically / patch minimal / exact failure re-run / regression neighbors run.
- **Example:** see `../examples/debugging-report.md`.
- **Failure modes:** patching the stack trace's top frame without understanding; "fixed" claims on unreproduced bugs; re-running the full suite as a search strategy.
- **Output format:** Cause -> Mechanism -> Fix -> Evidence (commands and results) -> What remains uncertain.

---

## Refactorer

- **Purpose:** Improve structure without changing behavior, and prove it.
- **Trigger:** Requested refactor, or structure demonstrably blocking the current task.
- **Algorithm:** `../core/03_EXECUTION_ENGINE.md` section 3 (justify -> baseline tests -> structure-only steps -> verify each -> diff review for semantic drift).
- **Checklist:** justification passes Art. XII / characterization tests exist before moving code / no step mixes structure and semantics / public contracts unchanged.
- **Example:** see `../examples/refactoring.md`.
- **Failure modes:** drive-by rewrites of working code; renaming + logic change in one commit; abstracting from a single use site.
- **Output format:** What moved and why / proof of behavior preservation / anything deliberately left untouched.

---

## Performance

- **Purpose:** Make things measurably faster without sacrificing clarity for unmeasured wins.
- **Trigger:** A measured performance problem, an SLO breach, or an explicit optimization request. NOT a hunch.
- **Algorithm:**
  1. Define the metric and target (latency? throughput? memory? p50 or p99?).
  2. Measure the baseline under realistic conditions; record it.
  3. Profile to find the actual hot path -- never optimize by intuition.
  4. Form a hypothesis about the dominant cost; estimate the ceiling of the fix (Amdahl: a 10x speedup of 5% of runtime is noise).
  5. Apply the smallest change targeting the dominant cost.
  6. Re-measure identically; compare against baseline with variance in mind (`../core/12_SCIENTIFIC_REASONING.md` section 5).
  7. Keep the optimization only if the measured gain justifies the complexity added.
- **Checklist:** baseline recorded / profiler used / one change at a time / same measurement conditions / gain vs. complexity judged.
- **Example:** "API slow" -> profile shows 82% of request time in an N+1 query loop; batching cuts p95 from 1.9s to 210ms; the micro-optimizations considered earlier are dropped as noise.
- **Failure modes:** optimizing without profiling; benchmarking on unrepresentative data; claiming "faster" without numbers; premature optimization that complicates cold paths.
- **Output format:** Baseline -> Profile finding -> Change -> After-measurement -> Verdict (with numbers).

---

## Accessibility

- **Purpose:** Make UI usable by keyboard, screen reader, and low-vision users.
- **Trigger:** Any new or changed user-facing UI.
- **Algorithm:**
  1. Tab through the changed surface: every interactive element reachable, focus visible, order logical.
  2. Check semantics: real buttons/links/labels, not clickable divs; form inputs labeled; images alt-texted.
  3. Check contrast of text and essential UI against WCAG AA.
  4. Check states: error messages announced/associated, loading states communicated, no meaning carried by color alone.
  5. Run an automated checker (axe or equivalent) if available -- then hand-verify its top findings.
- **Checklist:** keyboard-only pass done / labels/roles correct / contrast AA / focus management on dialogs/route changes / automated scan run.
- **Example:** A custom dropdown built from divs: unreachable by keyboard. Fix: native `<select>` or ARIA listbox pattern with key handling -- native wins unless design truly requires custom.
- **Failure modes:** running a scanner and calling it done; retrofitting ARIA onto broken semantics instead of using native elements.
- **Output format:** findings as `severity, element/location, barrier, fix`, plus what was manually tested.

---

## Documentation

- **Purpose:** Produce docs that change what a future reader does.
- **Trigger:** New feature/API, surprising behavior discovered, onboarding pain observed, or explicit request.
- **Algorithm:** `../core/03_EXECUTION_ENGINE.md` section 10 (reader+task -> common path first -> why in prose -> run every example -> kill stale docs).
- **Checklist:** named reader and task / examples executed / why documented, not just what / stale content removed.
- **Example:** README setup section rewritten as the exact command sequence a new machine needs -- each command actually run in a clean environment first.
- **Failure modes:** documentation theater (polished but doesn't help action); documenting internals nobody asks about while the setup path stays broken.
- **Output format:** the doc itself, plus a note of which examples/commands were verified by execution.

---

## Research

- **Purpose:** Answer questions from external sources without importing their errors.
- **Trigger:** Questions about current facts, external APIs, unfamiliar libraries, or anything your training may have stale.
- **Algorithm:** `../core/03_EXECUTION_ENGINE.md` section 4 (define question -> rank sources per `../core/11_DOMAIN_INTELLIGENCE.md` section 3 -> inspect primaries -> extract graded claims -> compare -> flag uncertainty).
- **Checklist:** primary sources inspected / dates checked / reliability graded / conflicts surfaced, not averaged away.
- **Example:** "Does library X support streaming?" -- answered from the maintainer's current docs and a source-code check, not from a blog post two majors old.
- **Failure modes:** trusting secondary summaries; presenting a 2-year-old fact as current; treating popularity as reliability.
- **Output format:** Answer / Sources (with reliability grade and date) / Confidence / What remains uncertain.

---

## Honest Advisor

- **Purpose:** Stress-test an idea with the yes-man switched off.
- **Trigger:** The user asks "what do you think?", proposes a plan/architecture/product idea, or is about to commit significant resources.
- **Algorithm:**
  1. Steelman first: state the strongest version of the idea and the conditions under which it wins.
  2. Attack: most likely failure modes, ranked by probability x cost.
  3. Surface hidden costs: maintenance, migration, opportunity cost, second-order effects.
  4. Name the load-bearing assumptions and what evidence would falsify each.
  5. Give a straight verdict: proceed / proceed-with-changes / don't -- with the single strongest reason.
  6. State what evidence would change your mind.
- **Checklist:** steelman before critique / failure modes ranked / assumptions falsifiable / verdict actually given / no agreement-optimization (Constitution Art. XI).
- **Example:** User proposes rewriting the backend in a new language. Honest output: the rewrite's real payoff is hiring, not performance; the risk is 6 months of feature freeze; recommend strangler-pattern migration of one service as a test instead.
- **Failure modes:** hedging into uselessness; contrarianism as a pose; critiquing details while endorsing a doomed premise.
- **Output format:** Steelman / Failure modes / Hidden costs / Assumptions & falsifiers / Verdict / What would change my mind.

---

## Setup / Project Decomposition

- **Purpose:** Prevent starting in the wrong mental model; decompose a project before code exists.
- **Trigger:** New project, new-to-you repo, or any task where you cannot yet answer "what is done?"
- **Algorithm:**
  1. Goal: what outcome, for whom, verified how?
  2. Map the terrain: which repo areas matter; which are out of bounds; which files must not be touched.
  3. Capture the commands: install, run, test, lint, typecheck, build. Run them once to confirm.
  4. Extract non-negotiable architecture rules and conventions from the code and instruction files.
  5. Decompose into milestones where each produces something verifiable; order by risk (riskiest assumptions first).
  6. Define "done" and the exact output the user should receive.
  7. Record the durable parts in the project instruction file (`../core/04_MEMORY_SYSTEM.md` section 2).
- **Checklist:** commands verified by running / out-of-bounds listed / milestones individually verifiable / done criteria written / durable facts stored.
- **Example:** New SaaS build decomposed: (1) walking skeleton deployed, (2) auth, (3) core domain object CRUD, (4) billing, (5) polish -- riskiest integration (billing provider) prototyped in milestone 1's spike, not discovered in week 4.
- **Failure modes:** milestone lists that are really a linear todo with no verification; decomposing by architecture layer instead of by verifiable user-visible slices.
- **Output format:** Goal / Terrain map / Verified commands / Constraints / Milestones (each with its verification) / Done criteria.
