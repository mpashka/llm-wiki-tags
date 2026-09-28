# Release notes

*Languages: **English** · [Русский](RELEASE-NOTES.ru.md) — About:
[README.md](README.md) · Install: [INSTRUCTIONS.md](INSTRUCTIONS.md)*

llm-wiki-tags is a convention, not a program: a "version" is the state of the
pages an agent installs from. To move an installed repository to a newer version,
point your agent at [`INSTRUCTIONS.md`](INSTRUCTIONS.md) again — it re-copies the
rule files over the old ones.

## v0.4.0

**The system around the program and where to test it.** The `docs/` tree gets a
fourth view, `docs/external/`: the overall architecture of the system the program
is part of, its neighbours and the contracts with them — a consumer's knowledge,
not the neighbours' own documentation. The layout rule now says which diagrams go
where — the outside architecture (components or deployment, cross-component
sequences) in `external/`, use cases in `specification/`, classes, states and inner
sequences in `implementation/` — and that the outside one is drawn first.
`docs/testing/` now describes test environments, approaches and accounts (as a
pointer to where the credential is stored), keeps test cases short and moves long
step descriptions into reference pages.

To upgrade, point your agent at [`INSTRUCTIONS.md`](INSTRUCTIONS.md) again: it
re-copies `docs-layout.md`; create `docs/external/` when the program has
neighbours worth describing.

## v0.3.0

**Glossary.** A new always-loaded rule, [`glossary.md`](rules/glossary.md), and a
new page, `docs/terms.md`: one concept — one word, in code, docs and task
statements alike. Each entry gives the main term, the synonyms it replaces, a
short definition and a link to the owning page. A new name is introduced only
after searching the glossary by meaning, and a new name for an old concept is
recorded as a synonym instead of becoming a second concept. The tag registry links
to a glossary entry instead of defining the concept again.

To upgrade, point your agent at [`INSTRUCTIONS.md`](INSTRUCTIONS.md) again: it
installs `glossary.md` next to the other rule files and seeds `docs/terms.md`.

## v0.2.0

**Documentation layout.** The convention now says *where* pages live, not only
how they are indexed: everything under `docs/`, split into `specification/` (the
outside view), `implementation/` (the inside view) and `testing/`, organised by
tag; the repository root keeps only the files that must be there.

**Per-task working files.** `docs/requests/<task_name>/` is the place for the
task statement, the plan and debug scripts — not the repository root. What
outlives the task moves into the permanent pages in the same change.

**Hierarchical tags.** A slug may now be hierarchical with `/`:
`@tag:payments/retry` is a child of `@tag:payments`, one search for the parent
finds every child, and the tag path mirrors the documentation path. Flat slugs
stay valid, so tags placed under v0.1.0 keep working; the search commands changed
to `@tag:[a-z0-9/-]+`.

**Installed as rules, copied verbatim.** The convention now ships as ready-made
rule files in [`rules/`](rules/index.md), which an agent copies into the target
repository as `.claude/rules/llm-wiki-tags/` — Claude Code loads them on every
task there. Previously the instructions only asked the agent to write a section
into `AGENTS.md` in its own words; now every repository gets the same wording.
The per-language files (`code-tags-java.md`, `code-tags-python.md`,
`code-tags-golang.md`) carry a `paths:` glob in their front matter, so they are
loaded only when code in that language is touched. `AGENTS.md` keeps a short
section pointing at the rule files, for agents that do not read `.claude/rules/`.

**`INSTRUCTIONS.md` restructured** around that: step 1 installs the rule files,
the remaining steps apply them. The page no longer paraphrases the convention —
`rules/` owns the wording, `README.md` describes it for humans.

**Scope stated plainly.** llm-wiki-tags is for repositories whose subject is
code, with documentation serving the code; this repository is documentation-only
and therefore does not install its own rules.

## v0.1.0

The initial published convention: llm-wiki (an `index.md` in every meaningful
directory, bidirectional links, one page owns each detail) **plus tags** — the
`@tag:<slug>` token placed in *both* code and documentation, so one `grep` spans
the two.

- Tag format: YAML front matter in docs (`tags: "@tag:x @tag:y"`), a comment
  above the element in code, four granularities (package, file, class,
  method/function).
- A single tag registry in `docs/tags.md`.
- `INSTRUCTIONS.md` / `INSTRUCTIONS.ru.md` as the install payload an agent is
  pointed at, `README.md` / `README.ru.md` as the human description.
- Per-language placement rules for Java, Python and Go in `languages/`.
