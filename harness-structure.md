# The shape of a harness

The standard domains a harness organizes its conventions into, and the lifecycle phase that reaches for each.
A harness carries these domains so an agent can predict where a fact lives from the task it is doing.
Canon governs the expectation that the set exists and what each domain owns; the content of each domain belongs to the consuming harness.

Each domain is a top-level directory named for the subject it governs, fronted by an index that routes. The canonical set:

| Domain | Governs | Reached when |
|--------|---------|--------------|
| `domain/` | The business/domain model — what the concepts are, how they behave, and how they intertwine, with **no technical detail**. The source of truth for how things actually work. | Establishing or asserting **correctness** — planning against intent, and reviewing or verifying behavior against the model |
| `architecture/` | The application's technical structure — the invariants and design decisions that govern *where and how* to build. | **Planning** a change and **reviewing a plan** |
| `standards/` | The patterns and conventions a finished change is held to — code-level, and other non-code standards. | **Reviewing** finished work — code review and post-work review |
| `verification/` | The verifiability matrix — the concrete methods that prove a change works. | **Verifying** a change, and **planning** the steps that will verify it |
| `workflows/` | Processes and workflows that achieve agentic goals — e.g. delivering a feature (`feature-delivery.md`). | Carrying out a **known, deterministic operation** toward a goal rather than improvising one |
| `exemplars/` | Reference implementations to pattern new work off. | **Building** — writing against a known-good pattern |
| `tooling/` | Additional tools and external systems the harness can use. | **Performing an operation** through one of those tools |

## Rule

A harness organizes its conventions into this standard set of domains, each a directory named for its subject and reached by a specific reader task and lifecycle phase.
A harness may carry more domains than these, but a missing one from the set is a gap to name, the same as an absent verifiability matrix or architecture guidance — not a silent omission.

## Why

An agent reaches for a fact by the phase it is in: a planner needs intent and structure, a reviewer needs conformance and correctness, a verifier needs proof.
A stable domain map means every planner reads `domain/` and `architecture/`, every reviewer reads `standards/` and `domain/`, every verifier reads `verification/` — without inspecting the tree to learn where each harness put things.
Without the shared shape, each harness invents its own layout, conventions scatter or duplicate across ad-hoc directories, and an agent cannot predict from its task where the fact it needs lives.

## Do

- Give each domain its own top-level directory named for its subject, fronted by an index that routes — the same truthful-directory rule every taxonomy in the harness follows.
- Keep the three planning-and-review domains distinct: **`domain/`** is the business model with no technical detail, **`architecture/`** is technical design, **`standards/`** is code-and-convention conformance. They serve three different readers at three different phases.
- Point an agent at the domain its current phase reaches for: `domain/` and `architecture/` when planning — with `verification/` to plan how the change will be proven; `exemplars/` when building; `standards/` and `domain/` when reviewing; `verification/` again when verifying; `workflows/` when carrying out a known, deterministic process toward a goal.
- Name a missing expected domain as a gap, so the harness's shape is legible by its absence as well as its presence.

## Don't

- Fold the business/domain model into `architecture/`. Mixing *how the concepts behave* with *how the code is structured* removes the technical-free reference an agent reaches for precisely to assert correctness, and forces a planner to wade through code structure to find intent.
- File code-level standards where a planner reads `architecture/`, or design invariants under `standards/`. The planner then loads review-time conformance it does not need, and the reviewer hunts for standards under design.
- Treat the domain names as decoration. A directory that has drifted from the subject it is named for has stopped predicting its contents — reorganize or rename it, do not widen its description.

## See also

- [`./architecture-guidance.md`](./architecture-guidance.md) — the deeper expectation for the `architecture/` domain: the guidance doc a harness carries and that its absence is a gap.
- [`./verifiability-matrix.md`](./verifiability-matrix.md) — the deeper expectation for the `verification/` domain: the matrix's shape and what each row declares.
- [`./organization.md`](./organization.md) §"Make directory names and layer descriptions truthful" — the placement rule each domain directory is held to.
- [`./facts-vs-methodology.md`](./facts-vs-methodology.md) — why the content of these domains is *facts* that live in the harness, while the workflow that reads them across phases is *methodology* that lives with the skill.
