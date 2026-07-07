# 17_EVALUATION_PROTOCOL -- Measuring Aurelian

This protocol tests whether Aurelian improves agent behavior. Treat every evaluation as a hypothesis: loading Aurelian should produce more reliable plans, safer edits, better verification, clearer reports, and fewer unsupported claims.

## 1. Evaluation Question

Does the same agent perform better with Aurelian than without it on the same task class?

## 2. Minimum Test Set

Use at least one task from each category:

- Feature implementation.
- Debugging.
- Refactoring.
- Code review.
- Documentation update.
- UI or product-facing change.
- Unfamiliar-domain research.

## 3. Comparison Method

1. Run the task without Aurelian.
2. Run the same task with the relevant Aurelian load order from [../INDEX.md](../INDEX.md).
3. Keep the model, repository, task prompt, and tool environment as similar as possible.
4. Compare outputs using the scoring rubric below.

## 4. Scoring Rubric

Score each dimension from 0 to 3.

| Dimension | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| Scope control | Wanders or changes unrelated files | Some drift | Mostly scoped | Precisely scoped |
| Repo understanding | Guesses | Reads shallowly | Reads relevant files | Builds accurate contract/blast-radius model |
| Plan quality | No plan | Vague plan | Usable plan | Risk-aware, verifiable plan |
| Implementation | Broken or stylistically alien | Partial | Correct but rough | Correct, idiomatic, minimal |
| Verification | Unsupported claims | Weak/manual checks | Relevant checks | Risk-proportional evidence ladder |
| Reporting | Overconfident or vague | Some evidence | Clear summary | Evidence-grounded, honest, actionable |
| Learning | No durable lesson | Mentions lesson | Suggests update | Writes or identifies precise durable improvement |

## 5. Failure Signals

Aurelian is not working if the agent:

- Claims completion without evidence.
- Reads less relevant context than the baseline.
- Adds broad abstractions without need.
- Asks questions local files could answer.
- Treats the manual as ceremony instead of execution guidance.
- Produces longer reports without better decisions.

## 6. Evaluation Output

Record:

- Task name.
- Agent/model/harness.
- Aurelian files loaded.
- Baseline score.
- Aurelian score.
- Behavioral differences.
- Regressions.
- Recommended changes to Aurelian.

## 7. Update Rule

If the same weakness appears twice, update [../self-improvement/16_SELF_IMPROVEMENT.md](../self-improvement/16_SELF_IMPROVEMENT.md) or the smallest relevant file. Do not add broad rules for isolated failures.
