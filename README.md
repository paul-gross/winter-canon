# ❄️ winter-canon

The **Canon**: the universal, enforceable substrate true of *every* agentic harness — independent of language, project, or workflow.

These are the rules and governance for agent-facing context. They hold whether the harness governs a Python service, a C# game engine, an Angular frontend, or a docs repo. A harness in any ecosystem can adopt this canon as its bottom layer and build its project- and language-specific conventions on top.

## ✨ What's here

- **Authoring & organization law** — how any agent-facing markdown file is written, placed, and split so a cold agent finds the one fact it needs: cross-cutting authoring principles (`principles.md`), progressive disclosure (`progressive-disclosure.md`), and placement/admission rules (`organization.md`).
- **Harness-design law** — what makes a harness extensible by agents and how its parts divide: the standard domains a harness organizes into and when each is read (`harness-structure.md`), the facts-vs-methodology seam (`facts-vs-methodology.md`), the four levers of agent productivity (`four-levers.md`), the required verifiability matrix (`verifiability-matrix.md`) and architecture guidance (`architecture-guidance.md`), and the cold-spawn behavioral eval for harness changes (`evaluating-harness-changes.md`).

See [`index.md`](./index.md) for the routing table.

## 🚀 Installation

The canon plugs into a [winter](https://github.com/paul-gross/winter) workspace as a standalone extension. Add to the workspace's `.winter/config.toml`:

```toml
[[standalone_repository]]
name = "winter-canon"
url  = "git@github.com:paul-gross/winter-canon.git"
path = ".winter/ext/canon"
```

Then run `winter ws init`. Its conventions are addressed via the `winter-canon:` path notation (e.g. `winter-canon:/principles.md`).

A non-winter consumer can vendor or submodule the repo just as well — the canon depends on nothing and knows nothing about winter.

## 🎯 Scope

The canon owns only what is true of *every* harness. Language-specific code standards, project-specific architecture, and one team's workflow methodology are **not** canon — they live in the consuming harness and build on this substrate.

## License

MIT.
