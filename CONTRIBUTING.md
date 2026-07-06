# Contributing

`winter-canon` is a docs repo — universal harness conventions that the rest of an agentic ecosystem reads. Changes target a convention file directly.

## The admission bar

A convention earns a place in the canon only if it is true of *every* harness, independent of language, project, or workflow. If a rule only holds for one language's code, one project's architecture, or one team's workflow, it belongs in the consuming harness, not here. When in doubt, keep it out — the canon's value is that a reader can trust every rule in it applies to them.

## Voice and shape

Each convention follows the slot skeleton, stable-id scheme, and file-kind exemptions owned by [`rule-shape.md`](./rule-shape.md) (`canon:rule-shape`), in a terse, code-first voice. Read it and [`principles.md`](./principles.md) — the authoring rules this repo holds itself to — before editing any convention here. Match the shape of the closest existing sibling.

The index (`index.md`) is a router: every row states *when to read* the target, never *what is inside* it. Adding, moving, or removing a convention file updates the index row in the same change.

## Commit messages

[Conventional Commits](https://www.conventionalcommits.org/) with a scope:

    <type>(<scope>): <description>

- Types: `docs` is the common case; also `feat`, `fix`, `chore`, `refactor`.
- Scope: `canon` (or a specific convention like `principles`).

## Delivery

- Default branch: `master`.
- Primary contributors push directly to `master` — rebase onto the latest `origin/master` first so history stays linear.
- Outside contributors: open a PR against `master`.

Co-author agent-assisted commits per your harness's conventions.
