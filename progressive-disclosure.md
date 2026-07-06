# Progressive disclosure

How agent-facing docs are structured so an agent finds the one fact it needs without loading the rest. The structural complement to `canon:point-dont-duplicate` in [`./principles.md`](./principles.md): that rule governs how one doc references another; this one governs how a topic is split across files so those references have well-shaped targets to point at.

Each rule follows the slot skeleton owned by [`./rule-shape.md`](./rule-shape.md) (`canon:rule-shape`).

## Hub-and-spoke split (`canon:hub-and-spoke`)

**Rule.** When a reader seeking one fact in a topic would have to load substantial unrelated material to reach it, or the topic spans distinct sub-topics, split it into a hub `index.md` that carries a routing table plus one file per sub-topic — the threshold is semantic load, not length (`canon:semantic-load`). The hub holds only what every reader of the topic needs — the one-line framing and the router; each spoke holds one sub-topic's detail. General navigation into the topic enters at the hub, so the reader sees the sibling branches and descends only the one they need; a reference straight to a deep leaf is reserved for when the referring sentence needs one already-known fact and discovery is not the reader's task (`canon:hub-vs-deep-link`). When a single spoke itself grows into distinct sub-topics, it becomes a hub in turn (a sub-directory with its own `index.md`), and the chain deepens by one.

**Why.** A monolith taxes every reader with the whole topic for one fact; a flat pile of siblings with no hub makes them guess; a straight-to-leaf discovery reference hides the sibling branches. The hub keeps discovery cost bounded as the topic grows: read one short router, descend exactly one branch.

**Detect.** A directory of sibling leaves with no `index.md`; a doc whose sections a reader could enter independently but must load together; a *discovery* reference pointing past an existing hub straight at a leaf.

**Do.**

- A command reference where each command has its own file: a hub `index.md` with a routing row per command, and `init.md`, `destroy.md`, `status.md` beside it. A command group with many sub-commands earns its own sub-directory with its own hub.
- A convention area: a hub `index.md` whose rows route to one convention file each, and which itself names its parent domain for the reader climbing back up.

**Don't.**

- A single file that grows section after section until an agent must load all of it to answer one question — split it once a reader seeking one fact must wade through unrelated material, or it starts spanning sub-topics.
- A *discovery* reference that points past the hub straight at a leaf, so the reader never sees the router and the sibling branches stay invisible. (A reference that already knows its exact target is a different case — `canon:hub-vs-deep-link`.)

## Split by semantic load, not word count (`canon:semantic-load`)

**Rule.** No numeric length threshold decides structure — not a line count, not a "screenful." A document becomes a hub with routed spokes when a reader after one fact must load substantial unrelated material to reach it, when its routing description needs several independent clauses to cover what it holds, or when its sections can be entered independently without reading the rest. The converse holds too: a long but cohesive contract a reader consumes as a whole stays one file, and a short file mixing unrelated purposes still splits. Size is a symptom, not the test.

**Why.** Length proxies for load but does not equal it: an arbitrary cut severs a thread the reader follows end to end, and a short mixed-purpose file still taxes its reader. Measuring load directly splits exactly the files that tax a reader and leaves the rest alone.

**Detect.** A split — or a refusal to split — justified by a number ("over N lines", "a screenful") rather than by what a reader seeking one fact must load to reach it.

**Do.** Ask what a reader seeking one fact must load to reach it. If the answer is "much they don't need," split; if "only the surrounding thread of the same idea," leave it whole.

**Don't.** Split, or refuse to split, on a line count. "Over N lines" is not a reason to break a file, and "under N lines" is not a reason to keep a mixed-purpose one whole.

## One leaf, one coherent question (`canon:one-question`)

**Rule.** A leaf document answers one coherent question: it has one expressible read-trigger, serves one audience, and sits at one level of abstraction. When a leaf's major sections require different read-triggers, switch between audiences (operator vs. implementer), or combine reference, tutorial, migration, and design rationale that a reader could enter independently, it is serving several questions — split it, sending each part to the file that owns its question, or turn the leaf into a hub routing to them.

**Why.** A leaf answering several questions makes each reader carry the other answers to reach theirs, and forces the hub's single routing row to promise them all at once — the row either misleads or swells into a paragraph.

**Detect.** A leaf whose major sections address different audiences or read-triggers — usage pivoting to wire protocol, reference mixed with migration narrative — or a routing row that needs several independent clauses to cover its target.

**Do.** A command-usage page for the operator running the command; the wire contract for the implementer building against it; the schema for the author configuring it — three triggers, three audiences, three files, each routed from the hub.

**Don't.** One page that opens with operator invocation, pivots to the provider wire protocol, and closes with a migration narrative — three readers, three triggers, bundled so each loads the other two.

## An index row is a router, not a contents list (`canon:row-is-router`)

**Rule.** Every row of a hub `index.md` states **when to read** the target — the trigger or condition that sends the reader there — and links to it. A row never describes **what is inside** the target. The "when to read" framing is a router that survives every edit to the target; a contents description is a second copy of the target that drifts the moment the target changes (`canon:point-dont-duplicate`, applied to the row shape).

**Why.** An agent traversing a hub is deciding *which branch to descend*, and a read-trigger row answers exactly that no matter how the target's contents shift. A contents-summary row is a second copy that reads as complete — the next author trusts the stale summary instead of the target.

**Detect.** A row that inventories — nouns from the target's headings, a list of its rules, "the X, Y, and Z rules" — instead of stating the condition that sends the reader there.

**Do.**

```
| ./principles.md | Cross-cutting principles for any agent-facing markdown file — read before authoring or editing one |
```

The row names the condition under which the reader descends — a trigger, not an inventory.

**Don't.**

```
| ./principles.md | The no-retrospective-framing, no-line-wrapping, and point-don't-duplicate rules |
```

The row inventories the target's contents; it must be re-synced by hand every time a principle is added or renamed, and it is wrong the first time the target changes.

## Keep hubs pure (`canon:pure-hubs`)

**Rule.** A hub `index.md` contains only what every downstream reader needs — the framing required to enter the topic, the navigation back to its parent, and the routing table. It does not carry schemas, procedures, examples, abbreviated reference material, or inventories copied from its children. When a hub starts to hold such detail, that detail belongs in a leaf and the hub points to it. (The routing rows themselves obey `canon:row-is-router`; this rule governs everything *between* the rows.)

**Why.** Every reader downstream of a hub loads it first, so detail parked there is paid for by all of them whether or not their branch needs it — and drifts from the leaf that owns it.

**Detect.** Schemas, procedures, examples, or option tables sitting between a hub's routing rows — anything a reader could reach one click down.

**Do.** A hub whose body is a one-line framing, a parent pointer, and a routing table — every fact one click down.

**Don't.** A hub that reproduces a child's schema table or option list "so the reader doesn't have to click" — the schema now lives in two places and every traverser loads it.

## Intermediate hubs for discovery, deep links for exact facts (`canon:hub-vs-deep-link`)

**Rule.** When the reader's task is *discovery* — finding which file covers a topic — route them through the nearest relevant hub so the sibling branches stay visible and they pick the right one. When the referring sentence instead needs *one already-known fact* — a specific heading, a single field, a named rule — link straight to that leaf or anchor; discovery is not the reader's task and a forced hop through the hub only adds a click. Neither is the universal default: match the link to what the reader is doing.

**Why.** The failure modes are opposite: a deep link during discovery hides the siblings the reader may have needed, while a hub hop on an exact citation spends a step showing choices already made. Ask whether the reader is still choosing.

**Detect.** A discovery-phrased reference ("for the command surface, see…") landing on a deep leaf while a hub exists; an exact single-fact citation routed through a hub it doesn't need. Flag the bypass during discovery — but don't force the exact reference through the extra hop.

**Do.**

- Discovery: *"For the command surface, see the usage hub"* linking to `usage/index.md` — the reader still chooses which command from the router.
- Exact fact: *"…the probe output contract"* linking straight to `configuration/doctor.md#probe-output-contract` — the reader already knows the one fact the sentence needs.

**Don't.**

- Send a reader who is still deciding which sub-topic they need straight to one leaf, bypassing the hub that shows the alternatives.
- Force a sentence that names one exact fact through a hub it does not need, just to honor "always enter at the hub".

## Tables for a set of options (`canon:tables-for-options`)

**Rule.** Present a set of parallel choices — files to route to, commands to pick among, modes to compare — as a table, not as sequential prose, and put the **choice column first**. The leftmost column carries the thing the reader is selecting (the link/destination, the command, the option); the column(s) to its right carry the discriminator that tells the reader which row is theirs. When the choice is a file reference — a routing table — those links form a single scannable left edge the eye runs straight down.

**Why.** A table lets an agent scan one column for its row and stop; sequential prose forces a linear read of every option. Leading with the choice column is what makes the scan fast — the destinations line up on one edge instead of scattering ragged on the right.

**Scope.** This binds tables that exist **to route** — a choice per row, the row's point being "pick this / go here." It does not bind a table that merely *contains* a link incidentally — a feature matrix, a comparison, a schema table — where the link is one attribute among several and no column is "the choice." When unsure, ask what the table is *for*: if a reader consults it to decide which row to act on or which file to open next, lead with that choice.

**Detect.** An option set written as sequential prose ("For X, read A. For Y, read B."); a routing table whose link column is not leftmost.

**Do.** A routing table whose rows are `| destination | when to read |` (the file link first), or a command table whose rows are `| command | usage | purpose |` — the choice on the left, the reader scanning the discriminator column to its right and descending one row.

**Don't.** Invert the columns — `| when to read | destination |` — stranding the links on the right where they no longer line up. And don't fall back to a paragraph that names each option in turn ("For X, read A. For Y, read B. For Z, read C."), which the reader must consume whole to find their case.

## Indexes warrant more scrutiny than leaves (`canon:index-scrutiny`)

**Rule.** Hold a hub `index.md` to a higher bar than the files it routes to, and review each row for whether its read-trigger is precise enough that the right agent descends and the wrong one does not. The invariant is **complete, precise routing**: every agent-facing leaf is reachable from its nearest hub, each routing row links its destination and states the condition under which the reader opens it, and any change to the set of leaves keeps the hub in step.

**Why.** A leaf mistake costs the readers who chose to descend to it; a hub mistake silently blocks discovery of the entire sub-tree it gates, and the blocked agent gets no signal that the missing branch exists at all.

**Detect.** A file under a hub with no routing row (grep the hub for each sibling's filename); a row linking a moved or deleted target; a trigger vague enough that a reader whose need is a sibling would descend it.

**Do.** Adding, moving, or removing a leaf updates its hub's routing in the **same change** — a new spoke gets a row, a moved spoke's row is repointed, a removed spoke's row is deleted. Check that each trigger is specific enough to be matched by the agent who needs that branch and *not* matched by one whose need is a sibling.

**Don't.** Add a file under a hub without a routing row — an unrouted file is undiscoverable; the hub is the only path to it. Leave a row pointing at a leaf that has moved or no longer exists — a dead route is worse than none, because the reader trusts it.

**See also.** `canon:point-dont-duplicate` in [`./principles.md`](./principles.md) — the reference-shape rule this article's structure exists to serve.
