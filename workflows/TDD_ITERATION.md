# Test-Driven Iteration Protocol

## Goal

Improve the product's intended behavior through small, evidence-backed changes. Tests and benchmarks
are diagnostic tools, not the objective; do not improve a metric by making the real system worse.

## Before Starting

- State the desired outcome, constraints, non-goals, and observable acceptance criteria.
- Read the repository guidance and identify the relevant test, lint, type-check, and evaluation commands.
- Record the current git state and preserve unrelated work.
- Establish a baseline for the behavior and metrics that may change.

## Iteration Loop

1. Reproduce one failure or weakness with the smallest representative case.
2. Trace it through the system and identify the earliest incorrect stage, not merely the visible symptom.
3. State one falsifiable hypothesis: cause, proposed change, and expected observable effect.
4. Add or refine a focused test that expresses intended behavior. For nondeterministic systems, use
   repeated trials or invariant checks rather than one lucky output.
5. Make the smallest general change that tests the hypothesis. Fix the intended mechanism instead of
   adding a fallback or special case.
6. Run focused tests, then the relevant regression, integration, lint, and type checks.
7. Evaluate real output as well as automated results. Check correctness, usability, performance,
   regressions, and edge cases that the metric may miss.
8. Keep the change only when evidence supports the hypothesis. Otherwise revert it and record what was
   learned; do not stack another speculative change on top.
9. Repeat on varied inputs. Promote a change only after it generalizes beyond the original example.

## Evaluation Rules

- Hold unrelated variables fixed when comparing results.
- Separate genuine failures from test, scorer, or measurement errors.
- Prefer invariant and contract tests over assertions tied to incidental implementation details.
- Add a regression test for every fixed bug when practical.
- Treat a larger test suite or higher score as insufficient without reviewing representative outputs.
- For expensive evaluations, use a small development set first and a broader holdout only after the
  mechanism is stable.
- Never encode fixtures, answers, benchmark wording, or scorer quirks into production logic.

## Devlog and Git

Append each meaningful experiment to the project's devlog: date, hypothesis, change, evidence,
conclusion, and whether it was kept or reverted. Record failed experiments when they prevent repeated
work or reveal a structural constraint.

After a major change is validated, make one focused commit:

- review the diff and stage only files belonging to the change;
- include its tests and documentation;
- describe the mechanism or behavior in the commit message, not merely a metric delta;
- do not commit generated outputs unless they are intentional project artifacts.

Small exploratory edits may remain uncommitted until they form one coherent, validated change. Do not
combine multiple unverified hypotheses in one commit.

## Stop and Report

Stop when the acceptance criteria are met, no coherent failure pattern remains, several hypotheses
produce no meaningful improvement, or progress requires a product decision. Report the baseline and
final evidence, changes retained or rejected, validation performed, known limitations, and decisions
still needed.
