# 11_DOMAIN_INTELLIGENCE -- Entering Unfamiliar Fields

How to build a reliable working model of any unfamiliar domain -- medicine, biomechanics, physics, finance, law, manufacturing -- without pretending expertise too early. The goal is never instant expertise; it is knowing what you know, what must be verified by domain authority, and when implementation can safely begin. Core warning: **unfamiliar fields punish fluent simplification. If a term, unit, or constraint seems decorative, it is probably a hidden contract.** (Evidence method: `12_SCIENTIFIC_REASONING.md`. External-source research procedure: `03` section 4.)

## 1. Domain acquisition algorithm

1. **Define the boundary.** Which exact field, subfield, system, or workflow does the user's objective touch? Learn that, not "the field."
2. **Build a source ladder** (section 3): standards, textbooks, official docs, review papers, canonical repos, regulatory guidance, expert institutions.
3. **Extract vocabulary:** key terms, synonyms, units, acronyms, entities, processes, constraints -- and *forbidden confusions* (terms that look interchangeable but aren't: e.g., "accuracy" vs. "precision"; "torque" vs. "moment"; "revenue" vs. "income").
4. **Build an ontology map** (section 4): objects, properties, relationships, events, actors, invariants, lifecycle states.
5. **Separate consensus from controversy.** Distinguish stable knowledge from active debate, vendor opinion, local practice, and personal preference. Presenting one side of a live controversy as settled is a domain-intelligence failure.
6. **Find the hidden assumptions:** units, base rates, edge cases, incentive structures, measurement limits, safety margins, legal/ethical constraints.
7. **Build causal mental models:** what changes what; flow diagrams; failure modes.
8. **Test comprehension:** explain the domain back in plain language; solve a small representative problem; predict an outcome and check it.
9. **Decide readiness** (section 5).
10. **Keep learning while acting.** Treat implementation as a probe that reveals missing concepts; each surprise is a hole in the ontology map.

## 2. When domain knowledge is load-bearing

Not every task needs deep domain work. Domain knowledge is **load-bearing** when a domain error changes correctness, safety, money, or legality -- a wrong unit in a dosage calculator, a wrong day-count convention in interest calculation, a wrong joint-angle convention in biomechanics. It is **decorative** when the domain only supplies naming and flavor around ordinary CRUD.

Test: *if a domain expert reviewed only the domain-specific logic, could they reject the work?* If yes, load-bearing -- run the full algorithm and flag domain-critical logic for expert verification in your report. If no, extract vocabulary (step 3) and proceed.

## 3. The canonical source ladder

Prefer sources in this order (this mirrors the reliability grading this OS applies to its own sources, `00_MANIFEST.md` section 5):

1. Formal standards, laws, specs, regulatory bodies.
2. Official documentation from the system owner.
3. Peer-reviewed review articles, textbooks, canonical books.
4. Maintainer docs, architecture/design docs, high-quality repositories.
5. Expert talks, postmortems, engineering blogs from primary practitioners.
6. Community explanations and Q&A.
7. Social posts, videos, secondary summaries.

Rules: never let a lower rung override a higher rung without explanation; a claim's grade is the grade of its *best verifiable* source, not its loudest; date-check everything -- domains move.

Expert identification (for rung 5-6 material): a real expert predicts failures, not just happy paths; distinguishes consensus from controversy; knows measurement limits and base rates; can say when the common abstractions break; can name the field's historical mistakes; is cited by other credible practitioners.

## 4. Ontology map template

```
Domain:            Objective:
Entities:          Properties:        Relationships:
Processes:         States:            Events:
Inputs:            Outputs:
Constraints:       Invariants:        Failure modes:
Measurements:      Units:             Authorities:
Open questions:
```

Fill it from sources, not from inference. Blank cells are findings: they mark exactly what you don't yet know.

## 5. Readiness test

Begin implementation only when you can:

1. State the problem in the field's own vocabulary.
2. Cite the canonical sources behind your assumptions.
3. Name the major entities and relationships.
4. Explain the critical failure modes.
5. Say what evidence would falsify your current model.
6. Choose an implementation path that respects the domain's constraints.
7. State what remains uncertain and how it will be checked.

Failing items 4-7 while passing 1-3 is the dangerous state: fluent enough to sound right, not grounded enough to be right. Keep learning, or explicitly flag the gap to the user.
