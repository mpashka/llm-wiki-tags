# llm-wiki-tags

> # llm-wiki-tags IS THE SAME **llm-wiki** BY ANDREJ KARPATHY — WITH **TAGS**.

*Languages: **English** · [Русский](README.ru.md) — Agent instructions:
[English](INSTRUCTIONS.md) · [Русский](INSTRUCTIONS.ru.md)*

## What it is

**llm-wiki** ([original gist by Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f))
is the idea of keeping a codebase's documentation as an *LLM-readable wiki*:
every meaningful directory carries an `index.md`, pages
are small and single-purpose, links are bidirectional (parent ⇄ child), and one
page owns each detail. An agent navigates the tree top-down through `index.md`
files instead of blindly grepping.

**llm-wiki-tags** is exactly that, **plus tags** — nothing about llm-wiki
changes; tags are added on top.

## What "+ tags" adds

A **tag** is a short kebab-case slug written as the token `@tag:<slug>`. The same
tag is placed **both in code and in documentation**, which creates an explicit
**code ⇄ documentation link** that does not depend on the directory tree. With
tags you can:

- **find code and docs by tag** — one search returns every file (code or docs)
  that carries a concept, even when they are scattered across the tree;
- **see which tags a piece of code has** — read the tags at the top of a file or
  directory to learn which cross-cutting concepts it participates in;
- **see which tags a document has** — the same, for a doc page;
- keep a single **tag registry** (`docs/tags.md`) describing what each tag means;
- **lay the documentation out by tag** — `docs/external/`, `docs/specification/`,
  `docs/implementation/` and `docs/testing/` follow the tag hierarchy, so the
  page describing a concept is where its tag says it is.

Tags complement `index.md` navigation (which follows the directory tree) with a
second, orthogonal axis: a concept that spans several folders is reachable in one
step.

### Tag format

Slugs are lowercase kebab-case (`[a-z0-9-]+`) and may be **hierarchical**, with
`/` as the separator (`@tag:payments/retry`); the same `@tag:<slug>` token is
placed in both code and docs.

- **Documentation** (`.md`): in **YAML front matter** at the top of the file, a
  `tags` field holding the space-separated tokens; for a directory, in that
  directory's `index.md`. A tag that applies to just one section may instead sit
  as a `@tag:<slug>` line in the body next to it.
  ```
  ---
  tags: "@tag:payments @tag:retry"
  ---
  ```
- **Code**: a comment in the language's syntax containing the token, placed above
  the element. A tag can mark a **package**, a **file**, a **class** (or
  equivalent) or a **method/function**. Per-language rules live in
  [`languages/`](languages/index.md) — [Java](languages/java.md),
  [Python](languages/python.md), [Go](languages/golang.md).
- **Multiple tags**: repeat the token, space-separated: `@tag:ui @tag:mechanism`.
- **Hierarchy**: `@tag:payments/retry` is a child of `@tag:payments`; one search
  for the parent finds the parent and every child. Hierarchy is preferred over
  long flat slugs, and it mirrors the documentation tree.

### Searching

```bash
# every code + doc location that carries a tag (and its children)
grep -rn "@tag:payments" .

# which tags a given file has
grep -oE "@tag:[a-z0-9/-]+" path/to/file

# every tag used in the repo
grep -rhoE "@tag:[a-z0-9/-]+" . | sort -u
```

Every tag is registered once in `docs/tags.md` with a one-line description.

## The index.md rules

llm-wiki-tags keeps (and makes explicit) llm-wiki's documentation rules:

1. **Every meaningful directory has an `index.md`** giving a **one-line
   description of each file and each sub-directory** in that folder.
2. Index files describe stable concepts, not changelogs. Prefer many small pages
   over one large document; put local detail next to the code it describes.
3. **Bidirectional navigation**: parent indexes link to child pages; child pages
   link back to the parent index and to related pages.
4. **One page owns a detail**; other pages link to it — do not duplicate.
5. **Read before you act**: before a task, follow `index.md` files from the
   nearest directory down to the code you will touch.
6. **Update as you go**: during or after the task, update the affected `index.md`
   files (and tags) in the same change.

## Documentation layout

llm-wiki-tags also fixes **where** the pages live, so that both a human and an
agent can guess the path of a page from the concept it describes:

```
docs/
├── index.md                      # index of the documentation
├── tags.md                       # tag registry
├── terms.md                      # glossary: one concept — one word
├── external/                     # the system around the program: architecture, neighbours
├── specification/                # what the program looks like from outside
│   ├── index.md
│   ├── payments.md               # a small area: one page
│   └── payments/                 # a grown area: a directory with its own index.md
│       ├── index.md
│       └── retry.md
├── implementation/               # how it is built inside — same shape
├── testing/                      # how it is tested: environments, approaches, test cases
└── requests/                     # working files of individual tasks
    └── <task_name>/              # request.md, plan.md, debug scripts, notes
```

- **All documentation lives under `docs/`.** The repository root keeps only what
  must be there: `AGENTS.md`, `CLAUDE.md`, the readme, the license, and files
  tooling requires at the root (`package.json`, `go.mod`, `Makefile`, CI config…).
- **Four views, one page each**: `external/` — the system around the program
  and the outside architecture; `specification/` — the outside view;
  `implementation/` — the inside view; `testing/` — where and how it is tested:
  environments, approaches, short test cases.
- **The outside architecture is drawn before the inside one**: components or
  deployment and cross-component sequences in `external/`, use cases in
  `specification/`, classes, states and inner sequences in `implementation/`.
- **Organised by tag, hierarchically**: `@tag:payments/retry` ↔
  `docs/implementation/payments/retry.md`. Naming a file after a tag is preferred
  but not required — use the tag as the name when it is the page's main subject;
  a page usually carries several tags in its front matter.
- **Per-task working files go to `docs/requests/<task_name>/`** — the task
  statement, the plan, debug scripts. Whatever outlives the task moves into
  `external/`, `specification/`, `implementation/` or `testing/` in the same change; the
  request folder stays as history.
- **One concept — one word**: `docs/terms.md` is the glossary — for each concept,
  the main term, the synonyms it replaces, a short definition and a link to the
  owning page. A new name is introduced only after searching the glossary by
  meaning; a new name for an old concept becomes a synonym.

## Where the rules live

Installing llm-wiki-tags writes the convention into the repository's **rules** —
`.claude/rules/llm-wiki-tags/`, which Claude Code loads on every task:

```
.claude/rules/llm-wiki-tags/
├── wiki.md               # index.md rules, read before you act, update as you go
├── docs-layout.md        # the docs/ tree above
├── tags.md               # tag format, registry, search commands
├── glossary.md           # docs/terms.md: search before naming, one definition
├── code-tags-java.md     # paths: ["**/*.java"]   — loaded only when Java is touched
├── code-tags-python.md   # paths: ["**/*.py"]
└── code-tags-golang.md   # paths: ["**/*.go"]
```

These files are shipped ready-made in [`rules/`](rules/index.md) (each with a
Russian twin) and copied **verbatim** — the installing agent does not paraphrase
the convention, so every repository ends up with the same wording. A rule file
with a `paths:` field in its front matter is loaded only when a matching file is
in play, so per-language rules cost nothing until they apply. Agents that do not
read `.claude/rules/` are served by a short "llm-wiki-tags" section in `AGENTS.md`
that points at these files.

## How to adopt it

Point your coding agent at the instruction page and ask it to install:

```
поставь https://github.com/mpashka/llm-wiki-tags/blob/main/INSTRUCTIONS.md
# or, in English:
install https://github.com/mpashka/llm-wiki-tags/blob/main/INSTRUCTIONS.md
```

The agent reads [`INSTRUCTIONS.md`](INSTRUCTIONS.md) (or
[`INSTRUCTIONS.ru.md`](INSTRUCTIONS.ru.md)) and sets up the `docs/` layout, the
`index.md` tree, the tag mechanism, the `docs/tags.md` registry and the
`docs/terms.md` glossary in the current repository, then installs the convention as rules in
`.claude/rules/llm-wiki-tags/` (plus a pointer in the repo's agent guide) so
future agents keep following it.

## Versions

What changed in each version is in
[`RELEASE-NOTES.md`](RELEASE-NOTES.md). To move an already-configured
repository to a newer version, point your agent at
[`INSTRUCTIONS.md`](INSTRUCTIONS.md) again.

## License

Public domain — [The Unlicense](LICENSE). Do whatever you want.
