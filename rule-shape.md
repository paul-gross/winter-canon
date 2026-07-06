# The rule shape (`canon:rule-shape`)

The slot skeleton every canon rule is written in — the slots, their semantics, the stable-id scheme, and the file kinds that are exempt.
This file owns the format; the rule files declare conformance by pointing here, never by restating the skeleton.
A consuming harness may adopt the same shape for its own conventions and gets the same scanability and enforceability when it does.

## Rule

Every canon rule is written in the slot skeleton below, carries a stable `canon:<slug>` id in its heading, and uses one of the two granularities.
A file that is not a rule file — a procedure or a taxonomy (see [File kinds](#file-kinds)) — is exempt from the skeleton but still carries a file-level id and an index row.
Any other deviation from the skeleton is drift for a reviewer to flag, not a local style choice.

### The slots

In this order:

| Slot | Presence | Holds |
|------|----------|-------|
| `Rule` | required | An imperative first sentence an agent can act on; qualifications follow it, never precede it. |
| `Why` | required | At most two sentences of generative rationale — enough for a reader to decide an edge case the rule doesn't list. Never the rule restated in negative form. |
| `Exception` | optional | The exhaustive exceptions. Absence is a claim: the rule has none. |
| `Scope` | optional | What the rule binds and what it leaves alone, when the `Rule` sentence can't carry it. |
| `Detect` | required for reviewer-enforced rules | The violation's signature: greppable phrases, structural tells, or the concrete question a reviewer asks — plus the fix to prescribe when it differs from "apply the rule". |
| `Do` / `Don't` | required | Minimal contrastive artifacts — a snippet, a table row, a directory tree. Never the rule restated as advice: a `Do` that paraphrases the `Rule` is duplication, not an example. |
| `See also` | optional | Cross-references to adjacent rules, cited by id. |

A rule whose violation has no expressible `Detect` signature is suspect: a rule no reviewer can recognize breaking is usually too vague to follow, let alone enforce.

### Stable ids

Every rule carries an id of the form `canon:<slug>` in its heading — in the `##` heading at rule-per-section granularity, in the `#` title at file-per-rule granularity.
The id is the citation handle: cross-references and reviewer findings cite the id, and the canon index's id column resolves each id to the file that owns it.
Ids are stable — citations depend on them, so a rename is a breaking change made only deliberately.
Adding, renaming, or removing a rule updates the index's id column in the same change.

### Two granularities

- **Rule-per-section** — a file collects several rules of one theme; each rule is a `##` section and the slots are bold run-ins (`**Rule.**`). For rules whose statement and examples fit a section.
- **File-per-rule** — one rule owns a whole leaf; the slots are `##` headings. For a rule that requires a contract with a body of its own — the file then carries additional sections (a shape spec, a domain table) that define the contract the `Rule` slot requires. Those sections are the owned fact, not skeleton drift.

## File kinds

Not every canon file states a rule. Three kinds, three shapes:

| Kind | Shape | Exempt from |
|------|-------|-------------|
| Rule file | The slot skeleton, at either granularity | — |
| Procedure file | Its own steps, schemas, and decision tables; `Rule` and `Why` open it to state the obligation and its reason, `Don't` closes with the failure modes | `Do` and `Detect` — the worked steps and examples are the positive form |
| Taxonomy file | Names and defines a set, as a definition list or table, with a `Why` for the set's membership | The skeleton — a definition has no imperative to slot |

A procedure or taxonomy file still carries a file-level `canon:<slug>` id in its title and a row in the index.

## Why

A fixed skeleton lets an agent read only the slot its task needs — `Rule` to comply, `Detect` to review, `Why` to judge an edge case — instead of parsing free prose to find the norm.
Declaring the exempt kinds keeps the skeleton's promise honest: a reader who knows a file's kind knows exactly which structure to expect.

## Detect

- A rule section missing a required slot, or carrying unlabeled normative paragraphs between the slots.
- A `Why` running past two sentences, or re-arguing the rule instead of giving rationale that generalizes.
- A `Do` that paraphrases the `Rule` instead of showing an artifact.
- A rule heading without a `canon:<slug>` id; a cross-reference quoting a heading title where an id exists; an id present in a heading but missing from the index's id column.
- The skeleton forced onto a stepwise procedure or a definitional taxonomy — or a single enforceable rule hiding inside a procedure or taxonomy shape where no `Rule` slot names it.

## Do

A complete rule at rule-per-section granularity:

```markdown
## No stale command output (`canon:no-stale-output`)

**Rule.** Don't paste captured command output into reference prose as if current; state what the command reports and let the reader run it.

**Why.** Pasted output asserts values that change on the next release, and nothing flags the staleness.

**Detect.** Fenced blocks of versioned or timestamped output inside reference prose.

**Do.** *"`winter status` lists each env with its port base."*

**Don't.** A fenced block of last month's `winter status` output presented as the current state.
```

## Don't

A rule written as free prose — norm, rationale, and examples interleaved in paragraphs a reader must parse whole to find the imperative, with no id to cite it by.

## See also

- [`./principles.md`](./principles.md) — the authoring rules the slot contents are held to (`canon:one-owner`, `canon:minimal-examples`).
- [`./evaluating-harness-changes.md`](./evaluating-harness-changes.md) — a new or reshaped rule is a harness change; the cold eval it is owed before push.
