# Governance voice

## Governance voice (`canon:governance-voice`)

Write governance context the way a thoughtful senior software engineer explains a system to a colleague they respect.
The reader is capable and will build on what you say, so say it plainly and give it room. Trust them to follow a name,
to see what the structure already implies, and to wonder why only where the answer isn't obvious. Write the simplest,
most elegant prose that says what they need, and leave them to infer the rest: whatever an intelligent person or a
frontier model would work out on their own doesn't need saying. Good governance reads like a well-written design doc,
not a statute: someone can read it straight through once and come away knowing how things work and what is expected of
them.

> Config lives at the workspace root and, when the workspace has environments, in each environment folder. A worktree
> has no config of its own; it uses its environment's.
>
> A setting that more than one environment needs belongs at the root.

The same idea written as a statute is harder to read and says nothing more:

> Config sits at exactly two levels: the workspace's at the root, and, in a workspace with environments, one in each
> environment folder (see `layout.md`). A worktree never holds config; its settings resolve from the level above it.
> Each environment's config holds only the settings specific to that environment and never restates the workspace's.

This voice is for governance context: the markdown a repo keeps to govern something else, whether that's code,
documents, or another repo's rules. It is the source code of a harness, and the people who maintain the harness need to
be able to read all of it.

Whatever governance governs has its own voice, set by that governance. The canon is governance, so it is written this
way too. READMEs and docs sites are not governance and have their own voice. Formatting, such as line wrapping and table
alignment, is the linters' job.

## Rewriting into the voice

When rewriting existing governance in this voice, distill its ideas and remove whatever doesn't fit the voice. Read
neighbouring files only as needed to understand what a term means.

- Keep every rule that a reader could not work out for themselves. You may drop what the names or structure already make
  obvious, and you may drop justification clauses.
- Rules may be restructured, merged, or reordered.
- Citations of other rules may be kept, moved, or dropped where they get in the way of reading; keep the ones a reader
  actually needs to follow.
- Tables are fine where they help; dense cells are not.
- A file's house style, such as a recurring detect line, a "never" list, or coded columns, gets the same scrutiny as its
  prose: keep, reshape, or drop it as the voice suggests.
