# The gardening axes (`canon:gardening-axes`)

The **gardening axes** registry is a harness doc that declares what standing tending means for its project — the named axes along which the target is recurringly evaluated for weight, truth, and drift.
Canon governs its shape and requires its presence; the axes themselves belong to the project's own harness, because what counts as a weed is a fact about the target.

## Rule

Every harness declares a gardening-axes registry.
Its absence is a gap: a target grows by default — guidance accretes, code drifts, references rot — and without a registry a tending process either does not run or judges by its own taste, which is methodology carrying facts it should not own.

## Shape

The registry lists the axes, one entry per axis. An entry declares four things:

| Declares | Content |
|----------|---------|
| Evaluates | What this axis looks for — the weeds, stated concretely for this target |
| Scope | Which body of the target the axis covers (a codebase, a docs tree, a harness, a test suite) |
| Criteria | The standards or rules the axis judges against — a pointer to their one home, never a restatement. Where no standard exists yet, the entry says so and names authoring it as the axis's first act |
| Measurement | The number every run records, findings or none — the trend is a run's product even when the findings are zero |

### Axis ids

Every axis carries a stable name — the handle an evaluation pass is invoked with and its findings are attributed to. Ids are stable: pass definitions and finding lineages cite them, so a rename is a breaking change made only deliberately.

### Resolution

An evaluation pass names an axis and resolves it from the registry — the pass brings methodology, the registry brings what to look for and what to judge it by. A pass invoked with an axis the registry does not declare fails loudly rather than improvising, and that failure is itself a finding: the harness has a gap.

## Why

Everything a fleet produces is read by agents far more often than by humans, so every artifact carries a token cost per read and either earns it or doesn't — the registry is where a project states what earning it means, and the mandatory measurement is what makes the answer a trend rather than an impression.
Homing the axes in the harness keeps tending passes reusable across projects: the same pass pointed at a different harness tends a different garden.

## Detect

- A harness index with no gardening-axes row.
- A tending or evaluation pass whose prompt embeds its criteria — a taste engine — rather than resolving an axis from the registry.
- An axis entry restating the standards it judges by instead of pointing at their home.
- An axis with no declared measurement.

## Do

- Declare the registry in the harness and link it from the harness index.
- Write axes for what the project actually needs tended, each with its four declarations; point Criteria at the standard's one home.
- Where the standard is missing, declare the axis anyway with authoring the standard as its first act — a declared gap beats an undeclared one.

## Don't

- Run a standing evaluation whose definition of a weed lives in its own prompt — swap the pass and the project's tending criteria disappear with it.
- Copy standards prose into the registry — the entry is a router to criteria, not their second home.
- Declare an axis with no measurement — an axis that only files findings can never show the garden getting healthier.

## See also

- [`./verifiability-matrix.md`](./verifiability-matrix.md) and [`./architecture-guidance.md`](./architecture-guidance.md) — the sibling required-component expectations: verify, guide, and tend.
- [`./facts-vs-methodology.md`](./facts-vs-methodology.md) — the governing principle: axes are facts about the target; how a pass evaluates them is methodology.
- [`./enforcement-channels.md`](./enforcement-channels.md) — axes are the judgment channel where prose standards get their judge.
- [`./organization.md`](./organization.md) — `canon:auto-load-tax`: the acute case of the same per-read economics.
