---
description: "Tag format @tag:<slug>, hierarchical slugs, the docs/tags.md registry and the search commands."
---

# llm-wiki-tags — tags

A **tag** is a short kebab-case slug written as the token `@tag:<slug>`. The same
token is placed **in both code and documentation**, so one search finds every
place a concept lives, independently of the directory tree. Companion rules:
[`wiki.md`](wiki.md), [`docs-layout.md`](docs-layout.md).

## Format

- **Slug**: `[a-z0-9-]+`, optionally **hierarchical** with `/` —
  `@tag:payments`, `@tag:payments/retry`. Hierarchy is preferred: a search for
  the parent also matches every child, and the hierarchy mirrors the
  documentation tree.
- **Documentation** (`.md`): YAML front matter at the top of the file, a `tags`
  field with the space-separated tokens; for a directory, in its `index.md`.
  ```
  ---
  tags: "@tag:payments @tag:payments/retry"
  ---
  ```
  A tag that applies to a single section goes as a `@tag:<slug>` line in the body
  next to that section instead.
- **Code**: the token in a comment directly above the element it marks — a
  package, a file, a class (or equivalent) or a method/function. Language
  specifics are in the `code-tags-*.md` rules next to this file.
- **Multiple tags**: space-separated — `@tag:ui @tag:mechanism`.
- Always keep the literal `@tag:<slug>` token; a bare slug list is not findable.

## Registry

Every tag is registered once in `docs/tags.md` with a one-line description of the
concept it links. Register the tag before placing it, and keep the registry
current when tags are added, renamed or retired.

Do **not** invent tags for one-off details — a tag is for a cross-cutting concept
that recurs across code and docs.

## Search

```bash
grep -rn "@tag:payments" .                     # every location of a tag (and its children)
grep -oE "@tag:[a-z0-9/-]+" path/to/file       # tags on one file
grep -rhoE "@tag:[a-z0-9/-]+" . | sort -u      # every tag in the repo
```
