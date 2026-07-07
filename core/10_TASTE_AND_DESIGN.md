# 10_TASTE_AND_DESIGN -- What Good Looks Like

Taste is engineering judgment about shape, proportion, restraint, naming, abstraction, and coherence. It is not personal style, and it is not decoration. Root principle: **optimize for the maintainer's future attention, not the author's present cleverness.** (Why these rules exist: `09_ENGINEERING_PHILOSOPHY.md`. Worked contrasting examples: `../examples/`.)

## 1. Code

- **Clarity over cleverness.** If a reviewer must decode it, it is wrong even when correct.
- **Local consistency over personal style.** In Rome, write Roman. A "better" idiom that fights the codebase is worse.
- **Explicit contracts over implicit coupling.** If caller and callee share an unstated assumption, name it in the signature, type, or doc.
- **Make illegal states hard to represent** where the language allows: sum types over boolean pairs, non-null by construction, parse-don't-validate.
- **Delete dead code.** Version control remembers; the reader's attention doesn't.

Contrast:

```
Bad:  if (u.type == 2 && !u.del && u.exp > now()) { ... }
Good: if (user.isActiveSubscriber(now)) { ... }
```
The good version moves the domain rule to one named home; the bad one makes every reader re-derive it and every change hunt for copies.

## 2. Naming

A name is good when the next reader can **predict behavior without reading the body**.

- Name for what it means in the domain, not how it's implemented (`retryDelay`, not `sleepTime2`).
- A name broader than the behavior is a lie: a `validateUser` that also creates a session must be renamed or split.
- Precision beats brevity; brevity beats ceremony: `userCount` > `numberOfUsersInTheSystem` > `n`.
- One concept, one word, everywhere: don't alternate `fetch`/`get`/`load` for the same operation.

## 3. Abstractions

Deep modules -- simple interface, substantial functionality -- are the goal. Shallow wrappers that rename their contents are negative value.

Decision tree:

```
Should I introduce an abstraction?
1. Duplicated BEHAVIOR, or only duplicated shape?  (shape -> no)
2. Is the concept stable enough to name?
3. Will callers understand it without reading its internals?
4. Does it reduce the facts a future maintainer must hold?
5. Does it preserve local idioms?
6. Can it be tested at its own boundary?
Mostly yes -> abstract.  Mostly no -> keep the code direct.
Uncertain -> duplicate once more, note the pressure, revisit with evidence.
```

Smells: a "generic" type with one call site; a helper that saves two lines but hides a contract; a wrapper that forwards every argument; configurability along an axis that has never varied.

## 4. APIs

- **Boring, predictable, hard to misuse.** Surprise is the cardinal API sin.
- The common path takes one obvious call; the dangerous path is loud (`deleteAll` should not sit next to `delete` in autocomplete with the same shape).
- Never require callers to know your internal call order. If B must follow A, make A return what B needs, or fuse them.
- Consistency across the surface (naming, errors, pagination, units) beats elegance in any single endpoint. Full API workflow: `../playbooks/06_PLAYBOOKS.md` section 8.

## 5. UX and visual design

Design is attention allocation made visible: a coherent interface lets users spend attention on their objective instead of decoding the tool.

- **Hierarchy directs attention.** Decide what the eye sees first, second, third -- then enforce it with size, position, contrast, spacing, grouping.
- **Whitespace is structure**, not emptiness. **Typography gives information a voice** -- consistent roles (heading/body/caption), not ad-hoc sizes.
- **Motion explains change** (continuity, cause-effect, feedback) -- it never merely proves the interface can move.
- **Density matches the user:** low density for onboarding, discovery, rare actions; high density for expert, repeated, monitoring workflows. Spaciousness is not elegance; density is not productivity.
- **Affordances make possible actions legible.** Color encodes meaning or nothing.
- Coherence beats novelty. Remove decisions the user shouldn't have to make.

Visual hierarchy algorithm:

1. Identify the user's next decision on this screen.
2. Rank visible elements by relevance to that decision.
3. Assign visual weight accordingly; demote or remove competitors.
4. Verify scanning order with an actual screenshot (never from the code alone).
5. Check mobile/desktop, empty, loading, error, and long-content states.

Coherence check (before shipping UI): Does layout reflect information priority? Are typography and spacing roles consistent? Does anything look clever but reduce comprehension? Does it feel native to its domain?

## 6. Writing and documentation

- Lead with the outcome; supporting detail after. The reader should get the point from the first sentence.
- One idea per paragraph; concrete nouns and verbs; delete words that don't change meaning.
- Comments explain **why the design exists** -- constraints, tradeoffs, non-obvious intent. A comment restating what the code does is a smell (and a maintenance liability).
- Structure follows the reader's task, not the author's discovery order. (Doc production algorithm: `03` section 10.)

## 7. Architecture

- Boundaries follow what changes together and what must be hidden (Parnas, `09` section 2), never fashion.
- Prefer the design you can still reverse; the strongest architecture claim is "we can change this later cheaply."
- A system's quality is visible in its failure behavior: good architecture degrades legibly, fails loudly at boundaries, and localizes damage.
- If explaining the architecture takes longer than a whiteboard sketch, the architecture -- not the explanation -- is probably wrong.

## 8. Restraint (the taste of not doing)

- No refactor when the requested change is narrow and the design is stable enough.
- No optimization without evidence of a problem and a hot path.
- No famous pattern unless the local forces match it.
- No configurability before the axis of variation is real.
- No test scope so broad that feedback becomes too slow to guide work.
- Fast shipping stops where correctness, security, data, or trust begins -- and perfectionism stops where the task is exploratory or throwaway.

Elite behavior is not the maximum possible work; it is the **right amount of work, at the right level of abstraction, with the right evidence, for the actual risk.**
