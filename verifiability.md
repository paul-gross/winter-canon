# Verifiability matrix

The verification methods available for the canon itself — how a change to a convention in this repo is verified. Shape
per [`./verifiability-matrix.md`](./verifiability-matrix.md) (`canon:verifiability-matrix`).

## Commands

The canon ships no scripts of its own — mechanical enforcement of its *rules* lives in the consuming harnesses, per
[`./enforcement-channels.md`](./enforcement-channels.md). What runs here is the mechanical markdown style every file in
the repo is held to, declared by the two configs at the repo root. Run both from the repo root.

| Method                | Command                                                                                                                                               |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `canon:format`        | `dprint check` — every markdown file matches the format `dprint.json` declares; `dprint fmt` writes the fix. Needs the `dprint` binary on `PATH`.     |
| `canon:markdown-lint` | `rumdl check .` — the structural markdown lint `.rumdl.toml` declares; `rumdl check . --fix` applies the autofixable subset. Needs `rumdl` on `PATH`. |

## Manual testing

`canon:manual` — the cold-spawn behavioral eval owed by
[`./evaluating-harness-changes.md`](./evaluating-harness-changes.md) (`canon:cold-eval`) for any rule addition, trigger
broadening, or routing change: declare each behavioral expectation as a scenario, spawn a fresh subagent with only the
cue and the production discovery chain, and record `reached` and `behaved` per scenario. A copyedit that changes no
claim owes nothing.

## Tools

`tool:eval-fixture` — a scratch directory of freshly written fixture prose exhibiting the anti-pattern under test, for
enforcement-flavored scenarios; write it from scratch, never from the rule's own `Do`/`Don't` examples.
