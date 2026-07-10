# 20_TASTE_REVIEW_SKILL -- Operational UI Taste Review

## Purpose

Review visual and interactive work with practical taste, not decoration talk. The skill turns subjective UI judgment into evidence-grounded findings that improve hierarchy, spacing rhythm, typography, layout balance, information density, color and contrast, motion quality, micro-interactions, visual coherence, premium feel, futuristic/interface polish, accessibility, and responsiveness.

Use this for pages, dashboards, landing pages, components, design systems, editors, animation systems, AI-generated UI, and any surface where users must understand, decide, or act.

## Trigger

Use this skill when:

1. A user asks for UI, UX, product, visual, interaction, design system, editor, canvas, landing page, dashboard, component, or animation review.
2. A diff changes user-facing UI or visual system primitives.
3. AI-generated UI must be accepted, rejected, or improved.
4. A product surface feels cheap, generic, confusing, noisy, low-trust, or unfinished.
5. A future product needs a taste gate before implementation, merge, release, or design handoff.

## Required Evidence

Taste review requires rendered evidence. Code inspection can identify likely problems, but final UI claims require screenshots or recordings.

Minimum evidence:

1. Desktop screenshot of the reviewed state.
2. Mobile or narrow-width screenshot when the surface is responsive or public-facing.
3. Screenshots for important states in scope: default, empty, loading, error, long-content, disabled, focused, hover/active, modal/open panel, and selected states.
4. Motion evidence when animation is reviewed: screen recording, frame sequence, or live browser observation.
5. Accessibility evidence when possible: keyboard traversal notes, focus screenshot, contrast check, and automated scan output if the project has tooling.

If screenshots are unavailable, mark the review as provisional and say exactly what cannot be verified.

## Algorithm

1. **Name the user objective.** What is the user's next decision or action on this surface?
2. **Gather artifacts.** Inspect screenshots, recordings, live pages, design files, component states, relevant code, and the product's `.aurelian/taste-reference.md` or `docs/03_PRODUCT_EXPERIENCE_BIBLE.md` when available.
3. **Establish context.** Identify surface type: page, dashboard, landing page, component, design system, editor, animation system, or AI-generated UI. Judge against the domain's real user, not a generic portfolio aesthetic.
4. **Trace hierarchy.** Rank what the eye sees first, second, and third. Compare that order to the user's objective.
5. **Evaluate layout and spacing.** Check alignment, grouping, rhythm, density, edge relationships, gutters, scroll behavior, and whether whitespace communicates structure.
6. **Evaluate typography.** Check type roles, scale, weight, line height, measure, casing, truncation, labels, hierarchy, and whether content is readable in real data states.
7. **Evaluate color and contrast.** Check semantic color roles, contrast, disabled and focus states, color-only meaning, palette restraint, and whether the palette feels coherent with the product's domain.
8. **Evaluate interaction and motion.** Check affordances, feedback, continuity, timing, easing, interruption behavior, reduced-motion behavior, and whether motion explains change instead of showing off.
9. **Evaluate premium feel.** Look for polish in alignment, rhythm, icon consistency, empty states, microcopy, focus states, loading behavior, shadows/borders, and transitions.
10. **Detect cheap-looking UI.** Flag generic gradients, random glass effects, inconsistent radii, muddy shadows, cramped hero copy, stock-card composition, low-contrast gray text, mismatched icons, one-note palettes, decorative motion, and components that look pasted from unrelated systems.
11. **Check accessibility and responsiveness.** Verify keyboard reachability, focus visibility, semantics, contrast, touch target size, text wrapping, zoom behavior, breakpoints, and content overflow.
12. **Produce improvements.** Each recommendation must be specific enough to implement: what to change, where, and why it improves the user's objective.
13. **Update durable taste memory only when stable.** If a review produces a repeated or accepted project taste rule, add it to `.aurelian/taste-reference.md` or `docs/03_PRODUCT_EXPERIENCE_BIBLE.md` with evidence. Do not store one-off opinions.

## Review Criteria

### UI Hierarchy

- The primary action, primary information, and current state are unmistakable.
- Competing elements do not fight for equal attention.
- Headings, size, contrast, position, and grouping express real priority.
- Empty and error states preserve the same hierarchy instead of becoming afterthoughts.

### Spacing Rhythm

- Spacing uses consistent roles: component padding, group gaps, section gaps, and page margins.
- Related items sit closer than unrelated items.
- Vertical rhythm supports scanning.
- Crowding and excessive air are both treated as hierarchy failures.

### Typography

- Type scale has clear roles, not arbitrary sizes.
- Body copy is readable at realistic line lengths.
- Labels, captions, metadata, and helper text are distinct without becoming faint.
- Long words, dynamic data, and localization do not break containers.

### Layout Balance

- Alignment is intentional across columns, controls, cards, panels, and toolbars.
- Dense interfaces remain scannable.
- Landing and editorial surfaces avoid dead zones and awkward first-viewport composition.
- Editors and dashboards prioritize work area, controls, feedback, and status in that order unless the product's workflow requires otherwise.

### Information Density

- Density matches the user's frequency and expertise.
- Expert workflows expose enough data and controls without decorative padding.
- Onboarding or rare workflows use lower density to reduce decision load.
- The interface does not hide essential status, validation, or next actions for aesthetic minimalism.

### Color And Contrast

- Color has semantic roles and does not carry meaning alone.
- Text and essential controls meet WCAG AA unless there is a documented exception.
- Accent colors guide action, state, or brand; they do not decorate every surface.
- Disabled, danger, success, warning, focus, and selection states are distinguishable.

### Motion Quality

- Motion explains continuity, causality, progress, or feedback.
- Timing feels responsive: fast for feedback, slower only when spatial continuity needs it.
- Easing is consistent across related interactions.
- Animation can be interrupted, does not block task flow, and respects reduced motion.

### Micro-Interactions

- Hover, focus, active, drag, drop, resize, undo, save, copy, loading, and error feedback are visible and useful.
- Controls reveal affordance before the user commits.
- State changes are acknowledged without noisy celebration.
- Editors and AI interfaces make generation, selection, application, rejection, and revision states explicit.

### Visual Coherence

- Components look like they belong to one system.
- Icons, radii, borders, shadows, spacing, and type roles repeat intentionally.
- Novel effects are reserved for places where they clarify the product's identity or workflow.
- Local conventions beat imported style.

### Premium Feel

- Precision is visible: crisp alignment, deliberate rhythm, well-tuned contrast, mature copy, and clean states.
- The UI feels trustworthy under real content, not only in ideal mock data.
- Advanced or futuristic surfaces still expose affordances, state, and recovery paths.
- Polish is concentrated around the user's most important moments.

### Futuristic / Interface Polish

- Futuristic styling must improve legibility, control, or product identity.
- Avoid fake complexity: ornamental charts, meaningless glow, decorative telemetry, and unreadable HUD density.
- Editors, canvases, and AI-native tools should feel powerful through direct manipulation, preview quality, explainable controls, and reversible actions.
- AI-generated UI must be editable and inspectable, not just visually impressive.

### Cheap-Looking UI Detection

Common cheapness signals:

- Random gradients, generic glass cards, excessive blur, decorative blobs, or inconsistent shadow depth.
- Poor alignment, off-rhythm spacing, mismatched icon weights, uneven corner radii, and inconsistent border treatment.
- Low-contrast gray text, washed-out controls, vague button labels, and identical visual weight for unrelated actions.
- Hero sections that look like templates rather than the product.
- AI UI that claims intelligence while showing fake scoring, fake capability, or uneditable output.

### Accessibility

- Keyboard path is complete and visible.
- Focus states are not removed or hidden under custom styling.
- Semantic HTML or correct ARIA patterns support assistive technology.
- Contrast, text resizing, reduced motion, touch targets, error messaging, and form labels meet expected standards.

### Responsiveness

- Layouts adapt intentionally across desktop, tablet, and mobile widths.
- Content wraps without overlap or clipping.
- Controls remain reachable and appropriately sized.
- Tables, canvases, editors, sidebars, and toolbars have responsive strategies instead of simple shrinkage.

## Checklist

- User objective named.
- Screenshots or recordings inspected.
- Desktop and responsive states checked or explicitly marked unavailable.
- Hierarchy, layout, spacing, typography, color, motion, interaction, premium feel, accessibility, and responsiveness reviewed.
- Cheap-looking and confusing elements identified.
- Findings tied to visual evidence, file path, design node, screenshot, or URL.
- Recommendations are specific and implementable.
- Final recommendation states ship / ship with fixes / revise before ship / reject.

## Example

A dashboard screenshot shows six equal-weight cards, faint gray labels, a heavy decorative gradient header, and a primary export button below the fold. Taste review finds that the user's likely next decision is "which account needs attention." Recommendation: demote decoration, raise alert summary and primary filters, use denser table rows, strengthen label contrast, and move export into the toolbar as a secondary action. Evidence: desktop and mobile screenshots plus file paths for the affected dashboard components.

## Failure Modes

- Reviewing from code alone while claiming visual confidence.
- Treating personal preference as a product rule.
- Praising novelty while missing hierarchy and usability.
- Applying landing page spaciousness to expert tools.
- Applying dense dashboard patterns to first-run onboarding.
- Accepting AI-generated UI that looks polished but is not editable, responsive, accessible, or explainable.
- Reporting vague taste comments without concrete fixes.

## Taste Review Report Format

```text
Taste Review Report

1. First impression
- What the surface communicates in the first three seconds.
- Confidence level and evidence inspected.

2. Hierarchy assessment
- What appears first, second, third.
- Whether that matches the user's objective.

3. Layout/spacing assessment
- Alignment, grouping, rhythm, density, balance, and responsive structure.

4. Typography assessment
- Type roles, scale, readability, labels, data handling, and truncation.

5. Motion/interaction assessment
- Affordances, feedback, transitions, micro-interactions, timing, and reduced-motion concerns.

6. Premium feel assessment
- What feels refined, trustworthy, mature, powerful, or unfinished.

7. Cheap-looking elements
- Specific elements that feel generic, low-trust, inconsistent, decorative, or template-like.

8. Confusing elements
- Ambiguous labels, unclear state, poor affordance, competing actions, hidden status, or misleading AI behavior.

9. Accessibility/responsiveness issues
- Keyboard, semantics, focus, contrast, touch targets, overflow, breakpoints, text scaling, and motion preferences.

10. Specific improvements
- Ordered recommendations with location, change, rationale, and must-fix vs optional.

11. Required screenshot/evidence
- Screenshots, recordings, URLs, design nodes, file paths, viewport sizes, states reviewed, and missing evidence.

12. Final recommendation
- Ship / ship with fixes / revise before ship / reject.
- Verification required before closing.
```
