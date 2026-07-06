# Principles for agent-facing markdown

Cross-cutting principles that apply to every agent-facing markdown file in any agentic harness — READMEs, extension `index.md`, skills, agents, `CLAUDE.md`, `context/` convention docs. Principles that apply to one specific file shape live in a per-shape convention file in the consuming harness (e.g. a `writing-readme.md` or `writing-skill.md`) and are not duplicated here.

Each rule follows the slot skeleton owned by [`./rule-shape.md`](./rule-shape.md) (`canon:rule-shape`).

## No retrospective framing (`canon:no-retro`)

**Rule.** Don't anchor current-state explanations to prior versions of the same doc, the prior shape of the code it describes, or the change history that produced today's state. State the current rule and the forward-looking reason behind it.

Superseded behavior, before/after examples, upgrade steps, and breaking-change narratives are not rewritten in place — they move to a changelog or an explicitly named migration document, linked from the current page only while an active migration still needs the reader to find it. When no active migration needs it, the dead history is deleted outright: a reference page carries the present, and the commit history already carries the past.

**Why.** A historical clause is loaded into every future agent context to describe a version of the doc no reader will ever see. Change history belongs in commit messages and PR descriptions — different audience, different lifetime.

**Exception.** History-by-design files keep their framing — `CHANGELOG.md`, `retrospective.md`, migration notes, post-mortem reports. There the change history *is* the content.

**Detect.** Grep for the phrases the pattern wears: *"earlier drafts"*, *"previously"*, *"we used to"*, *"the old approach"*, *"this used to be"*, *"no longer"*. The fix is always the same: delete the historical clause and keep the forward-looking reason underneath.

**Do.**

- *"Each prompt is inlined to keep step 4 self-contained — no cross-file step-number references."*
- *"Synthesis sections use `## must-fix` / `## consider` / `## clean` to match reviewer output vocabulary."*
- *"`SKILL.md` holds the workflow directly — no sibling doc indirection."*

State the rule, then the forward-looking reason.

**Don't.**

- *"Earlier drafts delegated to `X/SKILL.md` step 4 by step number, which silently broke when those skills renumbered, so the prompts are inlined here."*
- *"Previously the synthesis section was called `## Blocking`, but that collided with the `blocking` mode arg, so we renamed it."*
- *"This used to be a thick `SKILL.md` that delegated to a sibling doc, but we collapsed it."*

Each frames the current state as a correction to an invisible prior version. Strip the historical clause; what remains is the convention.

## No manual line wrapping (`canon:no-hard-wrap`)

**Rule.** Don't hard-wrap prose. Put one sentence or one paragraph per physical line and let the editor and renderer soft-wrap it; never reflow prose to a fixed column. Scope is prose only — code fences, tables, and YAML metadata blocks keep their own formatting and are exempt.

**Why.** Hard-wrapping makes a one-word edit reflow every line below it, burying the real change in reflow churn. One sentence per line keeps each edit localized to the line it touches.

**Detect.** Prose paragraphs whose physical lines break mid-sentence at a consistent column — lines ending on an unpunctuated word with the sentence continuing on the next line.

**Do.**

```
The reviewer reads the harness conventions before reviewing any agent-facing markdown, so a new rule reaches it through the same discovery chain a future author will traverse.
Each sentence sits on its own physical line; the editor soft-wraps it to the viewport.
```

One sentence per physical line — editing a word touches only that line.

**Don't.**

```
The reviewer reads the harness conventions before reviewing any
agent-facing markdown, so a new rule reaches it through the same
discovery chain a future author will traverse. Each sentence is
hard-wrapped at a fixed column, so editing one word reflows every
line beneath it.
```

Prose reflowed to a fixed column — a one-word edit churns every wrapped line below it.

## One canonical owner per fact (`canon:one-owner`)

**Rule.** Every behavioral rule, schema field, default, protocol requirement, or operational invariant has exactly one authoritative document — its canonical owner. Any other document that needs the fact links to the owner and may state *why* the reader should follow the link, but never restates the detail. When two files describe the same fact, exactly one is canonical and the rest are pointers; "for convenience" is not a second owner.

**Why.** A fact written in two places is a fact that will be edited in one — the stale copy keeps asserting the superseded value until a reader acts on it. Which document *is* the owner follows the reader's task — see `canon:by-reader-task` in [`./organization.md`](./organization.md).

**Detect.** The same table, option list, default set, or contract clause appearing in two files with neither reduced to a pointer — searching a distinctive literal (a field name, a default value, a flag) turns up two prose owners. The fix names one file canonical and reduces the rest to pointers.

**Do.**

- Pick the owner, name it, and point every other mention at it: *"Binding a provider is a configuration concern — see `capabilities.md`."* The pointer carries the stake, not the option list.
- When you find the same fact in two files, make one canonical and reduce the other to a pointer in the same change.

**Don't.**

- Repeat a table, option list, default set, or contract clause in a second file so a reader "doesn't have to follow the link" — the convenience lasts until the first edit, then the copy lies.
- Leave two files each describing the schema with neither marked as the owner, so the next editor changes whichever they happened to open.

## Point, don't duplicate (`canon:point-dont-duplicate`)

The reference-shape corollary of `canon:one-owner`: that rule says a fact lives in one place; this one says what the *other* places may say about it.

**Rule.** When one agent-facing doc points at another file or section — an index or "when to read" table row, a `CLAUDE.md` navigation entry, an extension `index.md` line, a cross-reference — describe the target by what the reader gets there or when to go, not by enumerating or copying its contents. A pointer that restates its target's contents is a second copy of them, and the copy drifts the moment the target changes.

**Why.** A pointer written as a read-trigger — "read before authoring an agent-facing file" — stays true across every edit to the target; a contents description silently drifts the moment the target changes, and reads as complete long after it isn't.

**Detect.** A pointer whose description enumerates the target's sections, rules, or options — a noun list that must be re-synced by hand when the target changes — instead of naming when to go or what the reader gets there.

**Do.**

- Index / "when to read" row described by read-trigger: `| ./principles.md | Cross-cutting principles for any agent-facing markdown file — read before authoring or editing one |`
- `CLAUDE.md` navigation row described by destination: `| Worktree git operations | context/worktree-ops.md |` — names where to go, not the steps the target lists.

Describe the destination; let the reader follow the link for the contents.

**Don't.**

- Index row enumerating the target's contents: `| ./principles.md | The no-retrospective-framing, no-manual-line-wrapping, and point-don't-duplicate rules |` — the list must be re-synced by hand every time a principle is added or renamed.
- An extension `index.md` line or `CLAUDE.md` row that restates the contents of the file it points at, instead of naming the destination — a second copy that drifts.

The enumerated list reads as complete, so the next author trusts it instead of the target — and it is wrong the first time the target changes.

## Examples are illustrative, not normative (`canon:minimal-examples`)

**Rule.** An example shows the smallest surface that makes the canonical rule concrete. It never reproduces a whole schema, template, exhaustive option set, or second specification already owned elsewhere. If an example would have to change every time the canonical contract changes, it is too big: cut it to the part that illustrates the point and link to the owner for the rest.

**Why.** A full-schema "example" is a second copy of the schema wearing an example's clothes — the word "example" disguises the duplication, and it drifts like any other copy (`canon:one-owner`). A minimal example carries no contract of its own; there is nothing in it to keep in sync.

**Detect.** Ask of each example: would it have to change if the canonical contract changed? An example reproducing every field of a schema owned elsewhere is a disguised duplicate, not an illustration.

**Do.**

- Show one representative entry, enough to make the shape concrete, and link to the canonical schema for the full field set.
- When an example must demonstrate a non-obvious or counter-example form, mark it with a comment marker (e.g. `<!-- lint:example -->`) so a lint or reviewer does not mistake it for a live reference; the harness that consumes this canon owns the concrete marker token and the lint that honors it.

**Don't.**

- Paste an entire manifest block with every field "as an example" into a file that does not own the schema — the field list is now duplicated, and it is wrong the first time the schema changes.
