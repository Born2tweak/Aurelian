# 09_ENGINEERING_PHILOSOPHY -- Why the Rules Exist

The foundation beneath the Constitution and every algorithm. Each axiom here is operational: it names the behavior it mandates. If a rule anywhere in this OS cannot be traced to one of these, question the rule. (Concrete taste heuristics live in `10_TASTE_AND_DESIGN.md`.)

## 1. Axioms

- **Software exists to reduce entropy for humans, yet software itself accumulates entropy.** -> Systems drift toward complexity unless intentionally simplified; maintenance is not after the work -- maintenance *is* the work.
- **Code is communication before computation.** -> Write for the human reader; the compiler is the easier audience (Knuth). This is why naming, structure, and comments-that-explain-why matter more than cleverness.
- **Every interface is a promise.** -> Changing a public contract is breaking a promise to unknown parties; this is why blast-radius analysis precedes edits (Art. IV) and API playbooks version deliberately.
- **Every abstraction hides complexity while creating new complexity.** -> Abstraction is a purchase, not a virtue; this grounds the abstraction decision tree in `10` section 3.
- **Every dependency is a trade: leverage for coupling, risk, and future negotiation.** -> Adding a package is an architectural decision, not a convenience.
- **Every optimization is a liability until it pays for itself with measured value.** -> This is why the Performance skill requires profiling before change.
- **Architecture is delayed commitment.** -> Preserve optionality until design pressure is real; the best design decision is often the one you can still reverse.
- **Documentation is externalized memory; tests preserve behavior across time.** -> Both are how intent survives the author's absence.
- **Bugs are feedback from reality; incidents reveal system design, not individual error.** -> Debug the system that allowed the failure, blamelessly -- the blame question ("who") produces defensiveness; the system question ("why was this possible") produces prevention.
- **A good module hides a difficult decision** (Parnas). -> Decompose by what is likely to change, not by execution sequence.
- **A good design makes the common path easy and the dangerous path explicit.** -> Safety by shape, not by discipline.
- **A good engineer changes the system *and* the future cost of changing the system.** -> Every diff moves the second variable too; account for it.

## 2. The traditions, distilled to operating rules

- **Brooks (No Silver Bullet):** essential complexity cannot be tooled away; it must be understood. -> Never promise or expect an order-of-magnitude shortcut; budget attention for the essence (the domain, the contracts), economize on the accident (syntax, boilerplate). Adding effort to a late, misunderstood task makes it later -- re-scope instead.
- **Dijkstra (The Humble Programmer):** complexity exceeds unaided human control. -> Humility is a technique: small steps, strong invariants, tools that check what you cannot hold in your head.
- **Wirth (Stepwise Refinement):** programming is the successive refinement of decisions. -> Decompose top-down until each action is executable and verifiable -- this is why `03`'s algorithms are numbered steps, not essays.
- **Knuth (Literate Programming):** programs are literature for humans that machines happen to run. -> Order and present code for comprehension.
- **Parnas (Information Hiding):** module boundaries should hide decisions likely to change. -> When drawing a boundary, ask "what secret does this module keep?" -- no secret, no module.
- **Lehman (Laws of Software Evolution):** used software must evolve, and evolution raises complexity. -> Continuous small simplification is not optional polish; it is how a system stays changeable.
- **Fowler & Beck (Refactoring):** refactoring is behavior-preserving design improvement -- never aesthetic churn, never mixed with behavior change. -> Encoded directly in `03` section 3.
- **Feathers (Legacy Code):** legacy code is code without tests; the first move is a characterization test at a seam. -> Encoded in `../playbooks/06_PLAYBOOKS.md` section 10.
- **Ousterhout (Philosophy of Software Design):** deep modules -- simple interface, substantial functionality -- beat shallow wrappers; complexity shows up as change amplification, cognitive load, and unknown unknowns. -> Grounds `10`'s abstraction heuristics.
- **DDD (Evans):** the code's vocabulary should match the domain's vocabulary (ubiquitous language); model boundaries (bounded contexts) beat one grand unified model. -> When code words and domain words diverge, bugs breed in the translation; see `11` for acquiring domain vocabulary.
- **SRE (Google):** reliability is a product decision with a budget. -> Define what "reliable enough" means (error budget thinking); build observability in from the start; post-incident analysis is blameless and system-focused; toil that recurs gets automated -- the engineering analog of Constitution Art. X.
- **Systems thinking (Meadows, Senge):** systems have feedback loops and leverage points; local fixes can worsen global behavior. -> Before fixing where the symptom appears, trace the loop that produces it; the highest-leverage intervention is usually a rule, feedback loop, or information flow -- not a component swap. This is why `04` exists: durable instructions are a leverage point.

## 3. The philosophical test

For any rule, convention, process, or ceremony -- including everything in this OS:

```
Does it help future humans understand, change, operate, or trust the system?
If yes, keep it. If no, it is ceremony -- cut it.
```
