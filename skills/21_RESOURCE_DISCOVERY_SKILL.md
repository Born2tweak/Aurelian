# 21_RESOURCE_DISCOVERY_SKILL -- Build From Evidence Before Building From Scratch

## Purpose

Discover, evaluate, and decide how to use existing resources before an agent invents a solution. This skill prevents unnecessary custom work, stale-library choices, license surprises, and weak imitations of mature systems.

It supports general Aurelian projects and UI/editor-heavy work such as design systems, component registries, animation systems, canvas tools, code editors, iframe previews, schema-driven UI, and AI-native interfaces.

## Trigger

Use this skill when:

1. Starting a new feature, product surface, tool, library choice, integration, design system, editor, canvas, or AI UI workflow.
2. The work touches an unfamiliar API, framework, domain, or external dependency.
3. The user asks whether to build, wrap, buy, adapt, replace, or avoid a resource.
4. A proposal duplicates known infrastructure such as authentication, editor engines, component primitives, animation orchestration, visual regression, accessibility checks, or preview sandboxes.
5. The project has `.aurelian/resource-index.md` or `docs/08_RESOURCE_ATLAS.md` that should be updated with verified resources.

## Algorithm

1. **Define the decision.** State what resource choice is being made and what outcome it must support.
2. **Inspect local context first.** Search the repo for existing packages, wrappers, components, design tokens, docs, ADRs, resource indexes, and prior experiments.
3. **Build a source ladder.** Prefer official docs, specs, maintainers, canonical repos, package registry metadata, design system docs, examples, and credible production references over blog summaries.
4. **Search resource classes.** Check official docs, GitHub repos, package registries, design systems, component libraries, animation libraries, editor/canvas libraries, AI UI tools, examples, competitors, standards, accessibility tooling, and visual regression tooling.
5. **Evaluate fit.** Score each candidate on capability, maturity, maintenance, license, integration difficulty, extensibility, performance, accessibility, security surface, bundle/runtime cost, community health, and reversibility.
6. **Prototype only when needed.** If docs and examples cannot answer a critical integration question, run the smallest spike that tests the uncertainty.
7. **Make a decision.** Choose build, wrap, buy, adapt, or avoid. Name the strongest reason and the cost of being wrong.
8. **Record durable resources.** Update `.aurelian/resource-index.md` or `docs/08_RESOURCE_ATLAS.md` only with verified resources that will guide future work. Include freshness, reliability, access notes, and use cases.
9. **Preserve uncertainty.** Mark stale, inaccessible, unverified, or conflicting resources as such. Do not promote popularity into truth.

## Resource Classes To Check

- Official docs and specifications.
- GitHub repositories, examples, issues, releases, and discussions.
- Package registries: npm, PyPI, crates, Maven, NuGet, RubyGems, or the project's ecosystem.
- Internal packages, shared modules, design tokens, component registries, and previous prototypes.
- Design systems and component libraries.
- Animation libraries and interaction examples.
- Editor, canvas, rendering, sandbox, and preview libraries.
- AI UI tools, SDKs, model interaction patterns, evaluation tools, and prompt/interface examples.
- Competitors, adjacent products, and high-quality public references.
- Licenses, commercial terms, governance, and attribution requirements.
- Maintenance status, release cadence, issue response, bus factor, security posture, and maturity.

## UI / Editor Research Areas

For React, Next.js, TypeScript, Tailwind, shadcn/ui, Radix, Framer Motion, GSAP, Three.js, React Three Fiber, Monaco, Sandpack, iframe previews, schema-driven UI, component registries, visual regression tools, and accessibility tools, evaluate:

1. Official documentation quality and current version behavior.
2. Compatibility with the project's framework, bundler, rendering mode, styling system, and deployment target.
3. TypeScript support, API stability, tree-shaking, SSR/client boundaries, and testing story.
4. Accessibility defaults and escape hatches.
5. Theming and design-token compatibility.
6. Composition model: primitives, headless components, slots, controlled state, plugin APIs, and imperative handles.
7. Editor-specific constraints: undo/redo, selection, drag/resize, keyboard shortcuts, iframe isolation, preview security, persistence, serialization, collaboration, and generated-code round trips.
8. Animation-specific constraints: sequencing, interruption, layout transitions, scroll/timeline control, performance, and reduced motion.
9. Visual QA support: screenshots, snapshots, Storybook, Playwright, Chromatic, Loki, Percy, axe, Lighthouse, and contrast tooling.
10. Whether generated UI remains editable, reusable, responsive, accessible, and explainable.

## Evaluation Matrix

Use this table for each serious candidate.

```text
Resource:
Type:
Location:
Version/date checked:
Source reliability: official | maintainer | canonical repo | community | unknown
License/commercial terms:
Maintenance status:
Maturity:
Capability fit:
Integration difficulty:
Accessibility posture:
Performance/runtime cost:
Security/privacy surface:
Extensibility:
Reversibility:
Known risks:
Evidence inspected:
Decision: build | wrap | buy | adapt | avoid
Reason:
Verification required:
```

## Decision Guide

### Build

Choose build when the requirement is core IP, existing options fail a load-bearing constraint, the scope is small and stable, or customization cost exceeds implementation cost. Building requires tests, docs, and a maintenance owner.

### Wrap

Choose wrap when a mature resource solves the hard problem but the project needs a stable local API, design-system integration, observability, accessibility fixes, or migration insulation.

### Buy

Choose buy when the capability is non-core, operationally expensive, legally sensitive, security-sensitive, or better handled by a maintained service with clear support and acceptable lock-in.

### Adapt

Choose adapt when an existing open resource, example, or internal pattern can be modified with clear license permission and manageable divergence. Record what changed and what future upgrades will cost.

### Avoid

Choose avoid when the resource is stale, poorly maintained, incompatible, overpowered, inaccessible, license-problematic, security-risky, fake, untestable, or likely to trap the product in the wrong abstraction.

## Checklist

- Local resources inspected before external search.
- Official docs or maintainer sources checked for important claims.
- GitHub and package registry health checked when choosing dependencies.
- License and commercial terms checked before reuse.
- Maintenance, maturity, integration difficulty, and reversibility assessed.
- Competitors and examples considered when product or UI taste is at stake.
- Build/wrap/buy/adapt/avoid decision recorded with evidence.
- Resource index or atlas updated only for verified durable resources.
- Unknowns and required verification are explicit.

## Example

A team wants to build a browser-based UI editor from scratch. Resource discovery finds mature candidates for code editing, previews, drag interactions, animation, accessibility checks, and visual regression. The decision is not "use everything." It is: wrap Monaco for code editing, evaluate Sandpack for isolated preview, use existing design-system primitives for controls, spike iframe preview security, avoid fake design scoring libraries, and record the resource evidence in `docs/08_RESOURCE_ATLAS.md`.

## Failure Modes

- Building from scratch because searching feels slower than coding.
- Choosing a dependency from popularity without checking maintenance, license, accessibility, or integration fit.
- Trusting secondary tutorials over current official docs.
- Importing a component library that fights the project's design system.
- Adopting an editor/canvas library before testing undo, selection, serialization, and responsive preview behavior.
- Accepting AI UI tools that produce uneditable, inaccessible, or hallucinated interfaces.
- Failing to record durable resource decisions, causing future agents to repeat the same search.

## Output Format

```text
Resource Discovery Report

Decision needed:
Local resources inspected:
External resources inspected:
Candidates:
- name, type, source, date/version, reliability, license, maintenance, fit, risks

Comparison:
- capability fit
- maturity and maintenance
- integration difficulty
- accessibility/security/performance considerations
- reversibility

Recommendation:
- build | wrap | buy | adapt | avoid
- rationale
- cost of being wrong

Verification required:
- docs to confirm
- spikes to run
- tests or visual checks needed

Durable updates:
- resource-index or resource-atlas entries added/changed
- unresolved unknowns
```
