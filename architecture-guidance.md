# Architecture guidance (`canon:architecture-guidance`)

**Architecture guidance** is a harness doc that describes an application's structural invariants, design decisions, and the constraints a change must honor.
A harness is expected to carry it.
Canon governs the expectation; the content belongs to the application's harness.

## Rule

Every harness carries architecture guidance.
Its absence is a gap: a planner without it must infer structure from code, and a plan reviewer cannot check whether a proposed design respects the invariants the application owns.

## Why

Without a documented invariant, every planner infers the architecture independently and no reviewer can flag a contradiction, because there is nothing to contradict.
With one, the constraints live in a single maintained place and every future plan and review picks them up.

## Detect

A harness index with no architecture-guidance row; structural constraints embedded in a planner or reviewer prompt instead of the guidance doc.

## Do

- Carry architecture guidance in the application's harness and link it from the harness index.
- State invariants as facts: what must be true of the application's structure, not how a workflow uses it.
- Update guidance when an invariant changes; the guidance is the single source of truth for the application's structural constraints.

## Don't

- Embed architectural constraints in a planner or reviewer prompt — those are facts about the application and belong in the guidance doc.
- Leave guidance absent and rely on planners to infer structure from code — inference diverges across runs and leaves no shared reference for contradiction checks.

## See also

- [`./facts-vs-methodology.md`](./facts-vs-methodology.md) — the governing principle: architectural invariants are facts and live in the harness; how a planner drafts or a reviewer sequences is methodology and lives with the skill.
- [`./verifiability-matrix.md`](./verifiability-matrix.md) — the paired expectation: a harness also declares a verifiability matrix.
