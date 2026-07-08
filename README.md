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
- keep a single **tag registry** (`docs/tags.md`) describing what each tag means.

Tags complement `index.md` navigation (which follows the directory tree) with a
second, orthogonal axis: a concept that spans several folders is reachable in one
step.

### Tag format

Slugs are lowercase kebab-case (`[a-z0-9-]+`); the same `@tag:<slug>` token is
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

### Searching

```bash
# every code + doc location that carries a tag
grep -rn "@tag:<slug>" .

# which tags a given file has
grep -oE "@tag:[a-z0-9-]+" path/to/file

# every tag used in the repo
grep -rhoE "@tag:[a-z0-9-]+" . | sort -u
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

## How to adopt it

Point your coding agent at the instruction page and ask it to install:

```
поставь https://github.com/mpashka/llm-wiki-tags/blob/main/INSTRUCTIONS.md
# or, in English:
install https://github.com/mpashka/llm-wiki-tags/blob/main/INSTRUCTIONS.md
```

The agent reads [`INSTRUCTIONS.md`](INSTRUCTIONS.md) (or
[`INSTRUCTIONS.ru.md`](INSTRUCTIONS.ru.md)) and sets up the `index.md` tree, the
tag mechanism and the `docs/tags.md` registry in the current repository, and
records the convention in the repo's agent guide so future agents keep following
it.

## License

Public domain — [The Unlicense](LICENSE). Do whatever you want.
