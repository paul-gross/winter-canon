# Organization and placement

Where a fact or a file belongs in the taxonomy, what earns a place in it, and what an automatically-loaded file may hold. The complement to [`./progressive-disclosure.md`](./progressive-disclosure.md): that governs how one topic splits into hubs and spokes; this governs which file or directory owns a fact at all, and whether a new file should exist.

Each rule follows the slot skeleton owned by [`./rule-shape.md`](./rule-shape.md) (`canon:rule-shape`).

## Classify content by the reader's task (`canon:by-reader-task`)

**Rule.** A fact's home follows what the reader is trying to *do* with it, not which component happens to implement the behavior. Command invocation, flags, examples, and result interpretation belong with usage; workspace and extension schemas belong with configuration; extension-author and provider protocols belong on an explicitly named architecture or contract surface; multi-step operating sequences belong in workflow documents. A page that serves materially different reader tasks is split, or reduced to a router that sends each task to its own page.

**Why.** A reader arrives by task; filing a fact by the component that implements it scatters one task across many files and piles unrelated tasks into one. Filing by reader task is the discrimination that lets a hub route a task to a single destination.

**Detect.** One page serving two reader tasks because one component implements both — operator invocation sharing a file with the provider wire contract, a configuration schema inside a workflow doc.

**Do.** Ask who reads this and what they are doing, then place it with the other facts that same reader reaches for: the operator's invocation with the other commands, the implementer's wire contract with the other contracts.

**Don't.** Keep a provider's protocol contract on the operator's command page because the same subsystem implements both — the operator loads the protocol they never call, and the implementer hunts for it under "usage".

## Make directory names and layer descriptions truthful (`canon:truthful-names`)

**Rule.** Every file satisfies the documented purpose of its containing directory and layer. A directory must not become a miscellaneous bucket by accumulating exceptions. When several files fail the placement test for where they sit, reorganize or rename the taxonomy and update its routers — do not widen the directory's description until it covers the unrelated material.

**Why.** The directory name is the router's promise — *everything here is X* — which is what lets a reader skip or trust it unopened. Widened to "X, and also Y" it predicts nothing, and the reader is back to the per-file inspection the taxonomy existed to spare them.

**Detect.** A directory description containing "and also", "plus", or "miscellaneous"; files that fail the placement test for their directory's stated purpose.

**Do.** When a file does not fit its directory's promise, move it to one whose promise it does fit, or — if several files are misfiling the same way — rename the taxonomy to name the real boundary and repoint the routers.

**Don't.** Append "and X" to a directory's description to legalize a file that does not belong, turning a precise layer into a catch-all that predicts nothing.

## Apply a new-document admission test (`canon:admission-test`)

**Rule.** A new agent-facing document is justified only when it (a) owns a distinct fact or reader task that no existing leaf naturally owns, (b) has a precise read-trigger, (c) is added to its parent router in the same change, and (d) removes or replaces any superseded copy it supplants. A file that merely gives another explanation of material an existing leaf already owns is rejected — improve the owner instead.

**Why.** Every new file is another branch to weigh at the hub and another place the same fact can later drift to; a distinct owned fact repays that cost, a re-explanation only adds it.

**Detect.** A new file whose topic an existing leaf already owns; a new file landing without a router row, or without deleting the copy it supersedes.

**Do.** Before adding a file, name the distinct fact it will own and the trigger that sends a reader to it; if you cannot, the content belongs in an existing leaf. When the new file does supersede an older one, delete the old in the same change.

**Don't.** Add a second file that re-covers an existing leaf's topic from a slightly different angle — two partial owners of one fact, neither canonical.

## Charge auto-loaded entry points a higher context cost (`canon:auto-load-tax`)

**Rule.** A file loaded into every agent context automatically — `CLAUDE.md`, an extension's top-level `index.md`, and the like — contains only universally-required operational rules and navigation. Background explanation, implementation detail, setup walkthroughs, and task-specific reference live behind links. Every non-routing section in an auto-loaded file must justify why *every* session needs it, not merely that it is true or useful.

**Why.** An ordinary leaf is paid for only by the agents that open it; an auto-loaded file taxes every session on every turn. The bar for inline content is not "is this useful" but "does every session need this to operate correctly".

**Detect.** Setup walkthroughs, schemas, or subsystem internals inline in `CLAUDE.md` or a top-level extension `index.md` — any non-routing section that can't answer why every session needs it.

**Do.** Keep an auto-loaded file to the rules every session must respect and a routing table to everything else; push setup steps, internals, and topic reference into linked leaves.

**Don't.** Park a setup walkthrough, a schema, or a subsystem's internals in `CLAUDE.md` or an extension `index.md` because it is convenient to have inline — every session now pays for what few need. A consuming harness applies this rule to its own auto-loaded surfaces — its `CLAUDE.md`, its extension `index.md` files — through whatever writing conventions it maintains for them.

## See also

- `canon:one-owner` in [`./principles.md`](./principles.md) — the ownership rule these placement rules decide the *home* for.
- [`./progressive-disclosure.md`](./progressive-disclosure.md) — once a fact's home is chosen, how that topic is shaped into hubs and spokes for discovery.
