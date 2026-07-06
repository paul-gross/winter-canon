# The Canon

The **Canon**: the universal, enforceable substrate true of *every* harness, independent of language, project, or workflow. These conventions hold for any harness — start here, then follow the one row that matches your task.

Every rule carries a stable `canon:<slug>` id ([`./rule-shape.md`](./rule-shape.md)); the Rule ids column below resolves a cited id to the file that owns it.

| File | When to read | Rule ids |
|------|--------------|----------|
| [`./principles.md`](./principles.md) | Cross-cutting principles for any agent-facing markdown file — read before authoring or editing one | `canon:no-retro` · `canon:no-hard-wrap` · `canon:one-owner` · `canon:point-dont-duplicate` · `canon:minimal-examples` |
| [`./rule-shape.md`](./rule-shape.md) | Adding, reshaping, or reviewing a convention rule — the slot skeleton, the stable-id scheme, and which file kinds are exempt | `canon:rule-shape` |
| [`./progressive-disclosure.md`](./progressive-disclosure.md) | Deciding how a topic is split across files and how its hubs route — read when shaping or restructuring a multi-file topic | `canon:hub-and-spoke` · `canon:semantic-load` · `canon:one-question` · `canon:row-is-router` · `canon:pure-hubs` · `canon:hub-vs-deep-link` · `canon:tables-for-options` · `canon:index-scrutiny` |
| [`./organization.md`](./organization.md) | Deciding where a fact or file belongs and whether a new document is warranted — read when placing, naming, or admitting an agent-facing file, or auditing a directory's contents against its purpose | `canon:by-reader-task` · `canon:truthful-names` · `canon:admission-test` · `canon:auto-load-tax` |
| [`./facts-vs-methodology.md`](./facts-vs-methodology.md) | Building any agentic feature (reviewer, skill, context doc) — deciding where the facts it acts on live (the harness, or the review target's own harness) vs. where the methodology it applies lives (the workflow) | `canon:facts-vs-methodology` |
| [`./evaluating-harness-changes.md`](./evaluating-harness-changes.md) | Shipping a change that adds context an agent should act on (new skill, agent, rule, feedforward doc, or routing) — the cold-spawn behavioral-expectation eval to run before push | `canon:cold-eval` |
| [`./four-levers.md`](./four-levers.md) | Reasoning about what makes a harness extensible by agents — the named levers a harness pulls to raise agent autonomy | `canon:four-levers` |
| [`./harness-structure.md`](./harness-structure.md) | The standard domains a harness organizes its conventions into and the lifecycle phase each is read in — read when structuring a harness, or deciding which domain a convention belongs to | `canon:harness-structure` |
| [`./verifiability-matrix.md`](./verifiability-matrix.md) | Authoring or reviewing a harness — the required verifiability matrix: its shape, what each row must declare, and naming its absence as a gap | `canon:verifiability-matrix` |
| [`./architecture-guidance.md`](./architecture-guidance.md) | Authoring architectural guidance within a harness — the expected guidance doc and that its absence is a gap | `canon:architecture-guidance` |
