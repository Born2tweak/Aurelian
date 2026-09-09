# Using Aurelian in an agent workflow

[Back to the overview](../README.md)

These examples use the published instructions and templates. They require an agent environment with the appropriate tools and observable acceptance criteria.

## Engineering task

Start with a concrete change and a condition that can be checked. For example, adapting a camera source should specify the frame representation and accepted source labels before implementation begins.

1. Read project instructions, current state, and affected interfaces.
2. Identify the requirement and the narrowest check that would expose a violation.
3. Plan the scoped change, including downstream consumers.
4. Implement, run the checks, and inspect the actual results.
5. Review the diff against the original requirement.
6. Record the result, candidate commit where available, and remaining uncertainty.

Use the [task procedures](../core/03_EXECUTION_ENGINE.md), [verification rules](../core/08_VERIFICATION_ENGINE.md), and [milestone report template](../templates/aurelian-project/reports/milestones/README.md).

If a command reports success after evaluating no eligible examples, the acceptance check must expose that empty result.

## Independent review

Give the reviewer the objective, requirements, diff, relevant source, and verification output. Ask for specific failure conditions backed by artifacts or reproducible checks. Treat the implementation agent's explanation as context, not proof.

One focused reviewer may be enough for a small change. The [specialist review protocol](../skills/22_REVIEW_SWARM.md) explains how to divide broader concerns and reconcile findings. Avoid concurrent edits to shared files. Verify accepted corrections before closure.

## Bounded research

Define the decision before searching. Specify what would directly support it, which sources offer only background, what details must be extracted, and when uncertainty is the appropriate outcome.

A KinematicIQ task used this structure to ask whether studies directly validated MediaPipe or BlazePose for a particular dynamic lunge and single-camera setup. The prompt required study-level details, distinguished direct from related evidence, and allowed a conclusion that no direct evidence was found. This illustrates task design, not a current claim about the scientific literature.

```text
Decision: [what the research will determine]
Direct evidence criteria: [system, setting, measurement, comparison]
Related evidence: [what informs design but cannot establish the claim]
Extraction: [source, date, method, results, limitations]
Allowed conclusions: [supported, insufficient, or not found]
Deliverable: [report with evidence references and search limits]
```

Use the [research-to-execution playbook](../playbooks/18_RESEARCH_TO_EXECUTION_OS.md) and [scientific reasoning rules](../core/12_SCIENTIFIC_REASONING.md). Preserve the scope and limits of a negative search result.

## Continuing across sessions

Use the [project-state template](../templates/aurelian-project/.aurelian/project-state.md) to record the objective, current position, blockers, and next action. Store durable decisions separately from raw logs. Link evidence to the requirement and artifact it describes.

At the next session, compare those records with current files and Git state. Investigate discrepancies before resuming. A prior completion statement is a lead to inspect.

## Responsibilities

| Participant | Responsibility |
|---|---|
| Human | Set objectives, constraints, permissions, and acceptance expectations; resolve decisions requiring human judgment |
| Agent | Inspect, plan, use tools, produce changes, investigate failures, and report evidence |
| Host and project tooling | Execute tools, enforce configured boundaries, run checks, and preserve available logs |
| Reviewer or evaluator | Assess results against requirements and expose unsupported claims |

Record contributions explicitly when authorship matters. Submitting a prompt, generating an implementation, and operating an automated check are different contributions.
