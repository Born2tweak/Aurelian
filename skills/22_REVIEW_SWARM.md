# 22_REVIEW_SWARM -- Specialist Reviewers For High-Stakes Work

## Purpose

Coordinate specialist reviewers without turning review into noise. A review swarm splits independent concerns across reviewers, requires evidence for every finding, deduplicates the results, and routes fixes back through the current verification ladder.

Use this for high-risk diffs, major milestones, architecture changes, security/data/money surfaces, public contracts, UI systems, AI-generated interfaces, editors, animation systems, and product work where one reviewer perspective is too narrow.

## Trigger

Use this skill when:

1. The work has meaningful risk across multiple dimensions: correctness, security, performance, UX, accessibility, testing, docs, product, motion, or frontend systems.
2. A milestone is ready for pre-merge or pre-release review.
3. The user asks for a review swarm, specialist reviewers, multi-agent review, or independent perspectives.
4. AI-generated UI, editor systems, component generators, or interface automation must be assessed before acceptance.
5. A single reviewer is likely to miss domain-specific risks.

## Rules

1. Split by concern, not by ego. Each reviewer gets a focused mandate.
2. Give every reviewer the same objective, scope, artifacts, constraints, and intended behavior.
3. Require evidence: file, path, line, screenshot, recording, source, command output, or reproducible steps.
4. Findings without evidence are discarded or downgraded to questions.
5. Merge findings yourself: deduplicate, rank severity, resolve conflicts, and separate must-fix from optional.
6. Do not forward reviewer claims as verified until current-session evidence supports closure.
7. Verify fixes in the repo-native environment using `../core/08_VERIFICATION_ENGINE.md`.

## Reviewer Roster

### Architect Reviewer

- Checks boundaries, module shape, abstraction depth, public contracts, reversibility, migration path, and long-term maintainability.
- Looks for over-abstraction, shallow wrappers, hidden coupling, irreversible commitments, and structure that fights the product workflow.

### Security Reviewer

- Checks trust boundaries, auth/authz, input validation, output encoding, secrets, dependency risk, sandboxing, file/network/shell operations, privacy, and abuse paths.
- For UI/editor systems, checks iframe isolation, preview execution, generated code handling, model/tool inputs, and data exfiltration surfaces.

### Performance Reviewer

- Checks hot paths, rendering cost, bundle size, network waterfalls, caching, database queries, memory, animation frame budget, and large-data behavior.
- Requires measurements or a clear path to measurement before claiming performance improvement.

### UX Reviewer

- Checks user goals, workflows, information architecture, labeling, errors, empty/loading states, affordances, onboarding, and recovery paths.
- Judges whether the system helps users decide and act.

### Taste Reviewer

- Uses `20_TASTE_REVIEW_SKILL.md` to assess hierarchy, spacing, typography, layout balance, density, color, contrast, visual coherence, premium feel, cheap-looking elements, futuristic polish, and screenshot evidence.

### Accessibility Reviewer

- Checks keyboard access, focus management, semantics, screen reader behavior, contrast, touch targets, text resizing, reduced motion, form labeling, and error announcements.
- Pairs automated scan output with manual inspection.

### Testing Reviewer

- Checks whether tests cover the changed behavior, edge cases, regressions, failure states, public contracts, visual states, accessibility, and integration seams.
- Flags tests that pass without proving the change.

### Documentation Reviewer

- Checks setup, usage, examples, comments, public API docs, ADRs, user-facing copy, and durable project memory.
- Verifies that docs are actionable and do not contain unsupported claims.

### Product Reviewer

- Checks whether the work serves the intended user, differentiates the product, avoids fake capability, handles primary workflows, and makes tradeoffs explicit.
- Flags features that look impressive but do not change user outcomes.

### Motion / Interaction Reviewer

- Checks animation purpose, timing, easing, continuity, interruption, reduced-motion support, gesture feedback, hover/focus/active states, drag/drop, undo, and state transitions.
- Rejects motion that is decorative, disorienting, slow, or inaccessible.

### Frontend / UI Systems Reviewer

- Checks component reuse, design tokens, state management, responsiveness, composition APIs, SSR/client boundaries, browser compatibility, styling architecture, visual regression strategy, and design-system consistency.
- For editors, checks selection model, toolbars, panels, canvas/preview boundaries, serialization, undo/redo, and generated-code round trips.

## Required Finding Format

Every reviewer must return findings in this exact shape:

```text
Reviewer:
Finding:
Severity: blocker | high | medium | low | nit
Evidence:
File/path/screenshot:
Recommendation:
Must-fix vs optional:
Verification required:
```

Severity guidance:

- **blocker:** Cannot ship; serious correctness, security, data loss, legal, trust, or unusable workflow risk.
- **high:** Likely user harm, production breakage, accessibility barrier, major regression, or severe maintainability trap.
- **medium:** Meaningful risk or quality issue that should be fixed before broad release.
- **low:** Real issue with limited blast radius or acceptable temporary workaround.
- **nit:** Small polish issue; never allowed to bury higher-severity findings.

## Review Algorithm

1. **State intent.** Summarize objective, changed artifacts, user impact, constraints, and out-of-scope areas.
2. **Select reviewers.** Choose only specialists whose concern is relevant. Do not create ceremonial reviewers.
3. **Prepare packet.** Include diff, files, screenshots, recordings, commands run, test output, designs, specs, and open questions.
4. **Run independent review.** Keep reviewers focused on their mandate and require the finding format.
5. **Normalize evidence.** Remove duplicates, unsupported claims, and findings outside scope. Ask for more evidence only when it would change the decision.
6. **Rank findings.** Order by severity and user/system risk.
7. **Decide action.** Mark each finding must-fix or optional. Must-fix items require verification before closure.
8. **Verify fixes.** Run targeted checks, visual checks, accessibility checks, security checks, or tests appropriate to the finding.
9. **Close with residual risk.** State what was fixed, what was verified, what remains optional, and what was not reviewed.

## AI-Generated UI / Editor Systems Review

When reviewing AI-native interfaces, UI generators, editors, canvases, component builders, prompt-to-UI flows, or design automation, apply these additional gates:

1. Generated UI must be editable through normal product controls.
2. Generated UI must produce reusable components or inspectable structure, not only screenshots or dead markup.
3. Pages and components must be responsive across realistic viewports.
4. Animations must be purposeful: explain state, continuity, progress, or feedback.
5. Design decisions must be explainable to the user or maintainer.
6. No fake AI capabilities: do not imply the system can reason, score, optimize, deploy, or edit beyond implemented behavior.
7. No fake design scoring: subjective or model-generated scores must not masquerade as objective quality.
8. No hallucinated APIs, components, files, integrations, or design tokens.
9. No low-taste default UI: generic gradients, vague cards, fake dashboards, ornamental telemetry, or inaccessible controls are findings.
10. Generated output must preserve accessibility, keyboard access, text wrapping, focus behavior, and contrast.
11. Editor actions must be reversible: undo, reset, diff, preview, or safe discard as appropriate.
12. Preview and execution environments must be isolated when generated code can run.

## Checklist

- Objective, scope, and artifacts provided to all reviewers.
- Relevant specialist reviewers selected; irrelevant ones skipped.
- Every finding includes evidence, path/screenshot/source, recommendation, must-fix vs optional, and verification required.
- Unsupported findings removed or downgraded.
- Findings deduplicated and severity-ranked.
- Must-fix findings verified after changes.
- Residual risks and skipped review areas reported.

## Example

A milestone adds an AI-assisted UI editor. The architect reviewer flags unclear editor serialization boundaries. The security reviewer flags untrusted preview code running in the main app context. The taste reviewer flags generic generated layouts with weak hierarchy. The accessibility reviewer flags missing keyboard paths for canvas controls. The product reviewer flags fake "design score" language. The swarm result is not eleven separate reports; it is one ranked list of must-fix findings with screenshots, file paths, recommendations, and verification required before the milestone can close.

## Failure Modes

- Asking many reviewers for the same generic review.
- Accepting findings without evidence because they sound plausible.
- Letting style nits bury correctness, security, accessibility, or product risks.
- Treating reviewer output as verification.
- Reviewing AI-generated UI only for appearance, not editability, responsiveness, accessibility, and truthfulness.
- Creating a swarm when one focused reviewer would be enough.

## Output Format

```text
Review Swarm Report

Objective:
Artifacts reviewed:
Reviewers used:
Reviewers skipped and why:

Findings:
- Reviewer:
  Finding:
  Severity:
  Evidence:
  File/path/screenshot:
  Recommendation:
  Must-fix vs optional:
  Verification required:

Merged decision:
- Must-fix before ship:
- Optional / follow-up:
- Rejected findings and reason:

Verification:
- Commands, screenshots, scans, or checks already run:
- Checks still required:

Residual risk:
Final recommendation:
```
