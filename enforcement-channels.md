# How a standard binds (`canon:enforcement-channels`)

A standard's prose does not govern the agents writing against it — imitation does. Agents write by pattern-matching the code and docs already in their context, which outweigh instructional prose by orders of magnitude; the same prose is applied well at judgment time, when a reviewer holds rule and artifact side by side. This rule names the channels through which a standard actually binds, so harness effort goes to the channels that work.

## Rule

Write standards for judges, and enforce them through the channel that binds at write time: the target itself first, mechanical gates second, judgment last.

- **The target teaches.** Agents imitate what they read, so a conformant target propagates its own standards and every tolerated violation teaches the next agent to repeat it. Keeping the target conformant is enforcement, not cleanup.
- **Exemplars are the bridge.** An exemplar is prose-shaped but pattern-consumed — built to be imitated, it is the deliberate channel from a standard into write-time behavior, the highest-leverage file in a harness and the most damaging when it drifts from the standard it embodies.
- **Mechanical gates bind deterministically.** A standard whose violation has a crisp signature belongs in lint or CI — the one write-time channel an agent cannot rationalize past.
- **Prose binds at judgment.** A written standard's consumers are the reviewer, the standing evaluation pass, and the author of a mechanical check. Author it as a criterion for them — and pair it with at least one such judge, or it binds nowhere.

## Why

An agent handed a page of "how to write" alongside a hundred times as much context that writes otherwise resolves the contradiction in favor of the evidence — instructional prose loses exactly where the target disagrees with it, which is the only place it was needed. At judgment time no competing gradient exists: rule and artifact meet directly, and judging conformance is work agents do reliably.

## Detect

- A standard authored or expanded to change writer behavior, with no judge — review axis, evaluation pass, or gate — that applies it.
- A harness answering recurring violations with more instructional prose instead of fixing the pattern pool (the target, its exemplars) or adding a mechanical check.
- An exemplar that contradicts a stated standard. The pattern is what propagates: resolve the conflict deliberately and fix whichever is wrong, never leave them disagreeing.

The fix to prescribe: pair the standard with its judge, and route write-time intent through the target's own conformance, its exemplars, and mechanical gates.

## Do

One standard, landed across all three channels:

```text
standards/comments.md      → the criterion a review or evaluation pass judges against
exemplars/ (pruned)        → the pattern writing agents actually imitate
lint: banned-comment rules → the crisp categories, gated deterministically in CI
```

## Don't

A harness that answers verbose machine-written comments by adding a "keep comments minimal" paragraph to its style guide — while its exemplar still opens with a thirty-line docstring. The next agent reads both and writes thirty-one.

## See also

- [`./principles.md`](./principles.md) — `canon:one-owner`: a standard graduating between channels moves home, never copies.
- [`./facts-vs-methodology.md`](./facts-vs-methodology.md) — standards are target facts; the judges that apply them live in the workflow product.
- [`./evaluating-harness-changes.md`](./evaluating-harness-changes.md) — the cold eval a new or reshaped rule is owed before push.
