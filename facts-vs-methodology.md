# Facts in the harness, methodology in the workflow (`canon:facts-vs-methodology`)

When you build an agentic feature — a reviewer agent, a review skill, a context doc, a new harness convention — the **facts** it acts on and the **methodology** it applies belong to different products, and must not be conflated. This is the rule that keeps them apart.

## Rule

Put facts and invariants in the harness that can keep them true, and put methodology in the workflow product that defines the operation.

- **Keep target facts with the target.** What must be true of the code or docs under review — the conventions, patterns, practices, and invariants a change has to honor — is a *fact*. It lives in a shared harness for facts common across targets, or the target's own harness for invariants that only make sense there.
- **Give reusable methodology a caller-neutral owner.** How a workflow conducts an operation — what it sequences, which roles it uses, and how it reports — is one team's swappable opinion. When a concrete second executor with different invocation or runtime semantics could plausibly perform the same steps from the same inputs, the workflow product owns one shared method and each executor adapts it.
- **Keep one-executor methodology self-contained.** When no plausible second executor exists, the skill or agent whose runtime semantics define the operation may own the method directly. Do not extract a shared core for a hypothetical caller with no credible use.
- **Derive criteria instead of embedding them.** A reusable reviewer reads the harness and target, discovers the invariants and patterns that apply, and reviews against those. It must not hard-code target criteria into its method or adapter.

## Why

A reviewer with the target's invariants baked into its method reviews against stale criteria the moment the target changes, and a method copied across executors drifts for the same reason. Kept apart, the harness is the single source of *what is true*, the workflow product owns *how to act on it*, and runtime adapters own only what differs at invocation.

## Detect

- A reviewer or skill prompt carrying target facts inline — naming conventions, architectural invariants, a catalog of components — rather than instructions to read them from the harness and target.
- The same semantic procedure copied into a skill and an agent even though both receive equivalent inputs and produce the same result.
- A shared method extracted from a self-contained executor without a concrete second invocation or runtime that could use it.

## Do

Two executors depend on one workflow-owned review method, which reads the target's conventions at runtime:

```text
review skill -----\
                  > shared review method ---> target harness
review agent -----/
```

The workflow product owns the shared method; the skill and agent own their invocation-specific adaptation. If only the skill could plausibly execute the operation, the skill would keep the method self-contained instead.

## Don't

A reviewer prompt that pastes the target's invariants inline and reviews against that copy:

```markdown
You are the doc reviewer. Enforce these naming rules:           ← target facts copied into the reviewer
- skills are named <verb>-<noun>
- every index.md must have a Scope section
- the catalog lists component-a, component-b, ...               ← will rot when the target changes
Review the target against the list above.
```

The facts now live in two places and drift; the reviewer cannot be reused against a target with different facts. Move the list into the relevant harness and have the reviewer read it.

## See also

- [`./principles.md`](./principles.md) — cross-cutting authoring principles for the markdown these features are written in.
