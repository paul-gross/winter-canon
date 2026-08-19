# Principles for agent-facing markdown

Cross-cutting principles that apply to every agent-facing markdown file in any agentic harness — READMEs, extension
`index.md`, skills, agents, `CLAUDE.md`, `context/` convention docs. Principles that apply to one specific file shape
live in a per-shape convention file in the consuming harness (e.g. a `writing-readme.md` or `writing-skill.md`) and are
not duplicated here.

Each rule follows the slot skeleton owned by [`./rule-shape.md`](./rule-shape.md) (`canon:rule-shape`).

## No retrospective framing (`canon:no-retro`)

**Rule.** Don't anchor current-state explanations to prior versions of the same doc, the prior shape of the code it
describes, or the change history that produced today's state. State the current rule and the forward-looking reason
behind it.

Superseded behavior, before/after examples, upgrade steps, and breaking-change narratives are not rewritten in place —
they move to a changelog or an explicitly named migration document, linked from the current page only while an active
migration still needs the reader to find it. When no active migration needs it, the dead history is deleted outright: a
reference page carries the present, and the commit history already carries the past.

**Why.** A historical clause is loaded into every future agent context to describe a version of the doc no reader will
ever see. Change history belongs in commit messages and PR descriptions — different audience, different lifetime.

**Exception.** History-by-design files keep their framing — `CHANGELOG.md`, `retrospective.md`, migration notes,
post-mortem reports. There the change history *is* the content.

**Detect.** Grep for the phrases the pattern wears: *"earlier drafts"*, *"previously"*, *"we used to"*, *"the old
approach"*, *"this used to be"*, *"no longer"*. The fix is always the same: delete the historical clause and keep the
forward-looking reason underneath.

**Do.**

- *"Each prompt is inlined to keep step 4 self-contained — no cross-file step-number references."*
- *"Synthesis sections use `## must-fix` / `## consider` / `## clean` to match reviewer output vocabulary."*
- *"`SKILL.md` holds the workflow directly — no sibling doc indirection."*

State the rule, then the forward-looking reason.

**Don't.**

- *"Earlier drafts delegated to `X/SKILL.md` step 4 by step number, which silently broke when those skills renumbered,
  so the prompts are inlined here."*
- *"Previously the synthesis section was called `## Blocking`, but that collided with the `blocking` mode arg, so we
  renamed it."*
- *"This used to be a thick `SKILL.md` that delegated to a sibling doc, but we collapsed it."*

Each frames the current state as a correction to an invisible prior version. Strip the historical clause; what remains
is the convention.

## No process references (`canon:no-process-refs`)

**Rule.** Don't cite the process that produced the content — issue, ticket, and PR numbers, tracker URLs, review-finding
ids (`M1`, `C4`), or review-round vocabulary. State the convention; a reader needs what it is, never which ticket asked
for it or which finding it answers.

**Why.** A process id resolves only inside the system that issued it, and only for as long as that system keeps it — a
finding id is scoped to one review round and dead the moment the round closes, and a tracker number is a lookup no
future agent will perform mid-task. The token is loaded on every read and returns nothing.

**Exception.** Documents whose subject *is* the process keep their references — a changelog, a migration note, an
issue-writing convention showing the reference notation, a review procedure defining its own finding-id vocabulary.

**Detect.** Grep for `#<digits>`, `GH-`, `closes`/`fixes #`, tracker hostnames, bare `M<digits>` / `C<digits>` tokens,
and the phrases *"per the review"*, *"as requested in"*, *"addresses finding"*, *"round 2"*. The fix is deletion, not
rephrasing: strip the citation and check whether the sentence still states a convention — if it doesn't, the sentence
was provenance and goes with it.

**Do.**

- *"Each prompt is inlined so a renumbered sibling skill can't silently break it."*

**Don't.**

- *"Inlined per #218 (review finding M2) so a renumbered sibling skill can't break it."*

The citation names a review round the reader cannot open and a ticket they will not fetch; the convention underneath it
stands on its own.

**See also.**

- `canon:no-retro` above — the same delete-the-history fix, applied to the doc's own change history rather than the
  tracker's.

## One canonical owner per fact (`canon:one-owner`)

**Rule.** Every behavioral rule, schema field, default, protocol requirement, or operational invariant has exactly one
authoritative document — its canonical owner. Any other document that needs the fact links to the owner and may state
*why* the reader should follow the link, but never restates the detail. When two files describe the same fact, exactly
one is canonical and the rest are pointers; "for convenience" is not a second owner.

**Why.** A fact written in two places is a fact that will be edited in one — the stale copy keeps asserting the
superseded value until a reader acts on it. Which document *is* the owner follows the reader's task — see
`canon:by-reader-task` in [`./organization.md`](./organization.md).

**Detect.** The same table, option list, default set, or contract clause appearing in two files with neither reduced to
a pointer — searching a distinctive literal (a field name, a default value, a flag) turns up two prose owners. The fix
names one file canonical and reduces the rest to pointers.

**Do.**

- Pick the owner, name it, and point every other mention at it: *"Binding a provider is a configuration concern — see
  `capabilities.md`."* The pointer carries the stake, not the option list.
- When you find the same fact in two files, make one canonical and reduce the other to a pointer in the same change.

**Don't.**

- Repeat a table, option list, default set, or contract clause in a second file so a reader "doesn't have to follow the
  link" — the convenience lasts until the first edit, then the copy lies.
- Leave two files each describing the schema with neither marked as the owner, so the next editor changes whichever they
  happened to open.

## Point, don't duplicate (`canon:point-dont-duplicate`)

The reference-shape corollary of `canon:one-owner`: that rule says a fact lives in one place; this one says what the
*other* places may say about it.

**Rule.** When one agent-facing doc points at another file or section — an index or "when to read" table row, a
`CLAUDE.md` navigation entry, an extension `index.md` line, a cross-reference — describe the target by what the reader
gets there or when to go, not by enumerating or copying its contents. A pointer that restates its target's contents is a
second copy of them, and the copy drifts the moment the target changes.

**Why.** A pointer written as a read-trigger — "read before authoring an agent-facing file" — stays true across every
edit to the target; a contents description silently drifts the moment the target changes, and reads as complete long
after it isn't.

**Detect.** A pointer whose description enumerates the target's sections, rules, or options — a noun list that must be
re-synced by hand when the target changes — instead of naming when to go or what the reader gets there.

**Do.**

- Index / "when to read" row described by read-trigger:

  ```text
  | ./principles.md | Cross-cutting principles for any agent-facing markdown file — read before authoring or editing one |
  ```

- `CLAUDE.md` navigation row described by destination: `| Worktree git operations | context/worktree-ops.md |` — names
  where to go, not the steps the target lists.

Describe the destination; let the reader follow the link for the contents.

**Don't.**

- Index row enumerating the target's contents:
  `| ./principles.md | The no-retrospective-framing, no-manual-line-wrapping, and point-don't-duplicate rules |` — the
  list must be re-synced by hand every time a principle is added or renamed.
- An extension `index.md` line or `CLAUDE.md` row that restates the contents of the file it points at, instead of naming
  the destination — a second copy that drifts.

The enumerated list reads as complete, so the next author trusts it instead of the target — and it is wrong the first
time the target changes.

## Examples are illustrative, not normative (`canon:minimal-examples`)

**Rule.** An example shows the smallest surface that makes the canonical rule concrete. It never reproduces a whole
schema, template, exhaustive option set, or second specification already owned elsewhere. If an example would have to
change every time the canonical contract changes, it is too big: cut it to the part that illustrates the point and link
to the owner for the rest.

**Why.** A full-schema "example" is a second copy of the schema wearing an example's clothes — the word "example"
disguises the duplication, and it drifts like any other copy (`canon:one-owner`). A minimal example carries no contract
of its own; there is nothing in it to keep in sync.

**Detect.** Ask of each example: would it have to change if the canonical contract changed? An example reproducing every
field of a schema owned elsewhere is a disguised duplicate, not an illustration.

**Do.**

- Show one representative entry, enough to make the shape concrete, and link to the canonical schema for the full field
  set.
- When an example must demonstrate a non-obvious or counter-example form, mark it with a comment marker (e.g.
  `<!-- lint:example -->`) so a lint or reviewer does not mistake it for a live reference; the harness that consumes
  this canon owns the concrete marker token and the lint that honors it.

**Don't.**

- Paste an entire manifest block with every field "as an example" into a file that does not own the schema — the field
  list is now duplicated, and it is wrong the first time the schema changes.

## Parallel items get parallel structure (`canon:parallel-structure`)

**Rule.** Present a series of parallel items as markdown structure — a list or a table, one item per physical line —
never as an enumeration carried inside a single paragraph, sentence, or table cell.

**Why.** Structure makes growth safe and visible: a new item is a new line the diff shows exactly, and a reader needing
one item finds it without parsing its siblings. An inline enumeration ratchets the other way — appending to the line is
always the edit least likely to break its neighbors, so every edit appends and the container degrades with no structural
rule left to fire on it.

**Scope.** The test is the item, not the count: binds any series whose items carry independent detail — their own
clauses, assertions, or references — and any open set that grows edit by edit; a short closed series named in passing
("init, provision, and up") stays prose. A set of parallel *choices* takes the table shape `canon:tables-for-options`
owns, and a routing table's citation-id column (a hub's Rule ids) stays inline — it is scanned as a set, not read item
by item.

**Detect.**

- Inline ordinal markers (`**(1)**`, `(a)`, "first… second…") inside a paragraph or cell.
- A semicolon-chained series whose items each carry independent detail.
- A hand-maintained count naming the enumeration's size ("sixteen scenarios").
- A physical line whose length no single sentence explains.

The fix to prescribe is restructuring into a list or table — never trimming items or wrapping the line.

**Do.**

```markdown
Scenarios:

- `test_happy_path` — build → review → land
- `test_review_cycle` — review fails once, findings thread back, then lands
- `test_escalation` — retries exhaust, the chunk parks for a human
```

One item per line — a new scenario is a new line, and the list needs no count to maintain.

**Don't.**

*"The suite covers three scenarios: **(1)** `test_happy_path` — build → review → land; **(2)** `test_review_cycle` —
review fails once, findings thread back, then lands; **(3)** `test_escalation` — retries exhaust, the chunk parks for a
human."*

Appending **(4)** mutates a line whose length the renderer hides, and the "three" in the prose is wrong the moment it
lands.

**See also.**

- `canon:semantic-load` in [`./progressive-disclosure.md`](./progressive-disclosure.md) — the overload test this rule
  gives a shape answer to.
- `canon:tables-for-options` in [`./progressive-disclosure.md`](./progressive-disclosure.md) — the required shape when
  the parallel items are a set of choices.
