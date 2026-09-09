# Architecture

[Back to the overview](../README.md)

Aurelian separates an agent's operating instructions from the infrastructure that executes and verifies work. This repository publishes the instruction layer. The related Python implementations described below remain separate.

## Instruction framework

The [Constitution](../core/01_CONSTITUTION.md) defines the core rules. The [execution procedures](../core/03_EXECUTION_ENGINE.md) and [decision engine](../core/07_DECISION_ENGINE.md) translate those rules into steps for planning, acting, recovering, and reporting. The [verification engine](../core/08_VERIFICATION_ENGINE.md) defines what evidence supports a completion claim.

The host supplies the model, tools, permissions, and orchestration. Loading a Markdown file does not itself create a scheduler or enforce a permission boundary. Projects can implement enforcement through tests, hooks, CI, or execution infrastructure.

### Context and memory

The agent starts with the kernel and loads task-specific material as needed. The [memory system](../core/04_MEMORY_SYSTEM.md) keeps stable decisions and project facts separate from temporary observations. The [project scaffold](../templates/aurelian-project/) includes state, decision, evidence, and traceability files.

These are records maintained by the workflow, not an automatically synchronized database. Agents must compare them with current repository state.

### Traceability and review

The [traceability contract](../core/14_TRACEABILITY_ENGINE.md) connects objectives and research to decisions, specifications, milestones, source files, tests, evidence, and review. Artifacts can record their owner or tool, parents, children, confidence, and supersession history. This repository does not ship a graph database or a program that validates every link.

The [review protocol](../skills/22_REVIEW_SWARM.md) divides concerns among focused reviewers, requires evidence for findings, and routes accepted corrections back through verification. Review remains a fallible evaluation step.

## Related Runtime and Trust Core

Separate local development contains a Python Runtime (`0.3.0a0`) and Trust Core (`0.2.1rc2`). Copying this repository's templates does not install those packages. Their distribution and public source locations are not established here.

| Component | Responsibility | Observed implementation |
|---|---|---|
| Runtime | Select and execute declared work | Dependency-aware scheduling, persisted planning observations, journals, recovery, typed retries |
| Authority | Decide whether an action is permitted | Policy checks around side-effecting operations |
| Trust Core | Evaluate declared completion requirements | Snapshot and execution binding, evidence records, acceptance predicates, completion records |

The Runtime's milestone pipeline follows this order:

```text
Implement -> Commit -> Capture snapshot -> Begin execution
          -> Produce evidence -> Verify -> Record completion
```

Evidence is evaluated against a committed candidate. Changing that candidate invalidates the verification context. Finishing implementation alone does not produce a completion record.

Recovery reconciles the Runtime journal with authoritative Trust Core completion state. Leases, heartbeats, and fencing address stale workers. Explicit transient failures can receive bounded retries; an evidence failure requires investigation.

### Current boundaries

The inspected integration trials use predefined Python implementation functions that write supplied source content. The planner reconciles declared work with repository observations; it does not establish unrestricted model-generated planning. Cross-repository portfolio scheduling is outside the recorded runtime scope.

The authority mechanism is an application boundary, not a sandbox against someone who can rewrite its implementation. Local hashes and journals do not establish authenticity against an actor controlling the code, data store, and every verification anchor.

Development examples and their evidence limits appear in [Reliability and research](RELIABILITY.md).
