# Install llm-wiki-tags (agent instructions)

> # llm-wiki-tags IS THE SAME **llm-wiki** BY ANDREJ KARPATHY — WITH **TAGS**.

*Languages: **English** · [Русский](INSTRUCTIONS.ru.md) — About:
[English](README.md) · [Русский](README.ru.md)*

You are an AI coding agent. The user asked you to **install llm-wiki-tags** into
the current repository. Follow the steps below, adapting paths and comment syntax
to the repo. Do not restructure or rewrite existing content beyond what is needed
to satisfy these rules. Make the changes as a normal edit to the repo.

## Concept

Keep the docs as an LLM-readable wiki (llm-wiki —
[original gist by Andrej Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)),
and add **tags** that link code and documentation across the directory tree.

A **tag** is a short kebab-case slug (`[a-z0-9-]+`) written as the token
`@tag:<slug>`. The **same tag is placed in both code and documentation**, so a
concept spanning several files/folders is reachable in one search.

## Steps

### 1. Establish the index.md tree

- Ensure **every meaningful directory has an `index.md`**. Create the missing
  ones.
- Each `index.md` gives a **one-line description of each file and each
  sub-directory** in that folder, and links to its parent index and child
  indexes (bidirectional navigation).
- Index pages describe stable concepts, not changelogs. Prefer many small pages;
  put local detail next to the code it describes. One page owns a detail; others
  link to it.

### 2. Create the tag registry

- Create `docs/tags.md` (use the repo's docs directory if it differs). It lists
  every tag with a one-line description of the concept it links, and documents
  the tag format and search commands (copy the "Tag format" and "Searching"
  sections from [`README.md`](README.md)).
- Add `docs/tags.md` to the docs `index.md`.

### 3. Place tags

When a concept spans **both code and docs**, choose a slug, register it in
`docs/tags.md`, and place the `@tag:<slug>` token at the relevant locations.
Always keep the literal `@tag:<slug>` token (not a bare slug list) — that is what
lets one `grep` find the same concept in code and docs alike.

**Documentation** — put the tag in **YAML front matter** at the very top of the
`.md`, in a `tags` field holding the space-separated tokens:

```markdown
---
tags: "@tag:payments @tag:retry"
---
```

- **A doc file**: front matter at the top of that file.
- **A doc directory**: front matter in that directory's `index.md`.
- **Part of a doc file**: if a tag applies only to one section, put a
  `@tag:<slug>` line in the body next to that section instead of the front matter.

**Code** — put the tag in a comment in the language's syntax, immediately above
the element. A tag can mark four granularities: a **package**, a **file**, a
**class** (or its equivalent) or a **method/function**. Per-language rules:

- [`languages/java.md`](languages/java.md)
- [`languages/python.md`](languages/python.md)
- [`languages/golang.md`](languages/golang.md)

For any other language, apply the same idea: `@tag:<slug>` in a comment
(`// `, `# `, `/* */`) directly above the package, file, class-equivalent or
function it marks.

- Multiple tags: space-separate the token, e.g. `@tag:ui @tag:mechanism`.
- Do **not** invent tags for one-off details; tags are for cross-cutting concepts
  that recur across code and docs.

### 4. Record the convention for future agents

- In the repository's agent guide (`AGENTS.md`, else `AGENTS.md`, else create
  `AGENTS.md`), add an **"llm-wiki-tags"** section stating the rules and
  imperatives below, and link to `docs/tags.md`. This is what makes the
  convention stick.

## Imperatives to record (and to follow yourself)

- **Documentation is an LLM wiki.** Every meaningful directory has an `index.md`
  with a one-line description of each file and sub-directory; keep bidirectional
  links; one page owns each detail.
- **Read before you act.** Before a task, follow `index.md` files from the
  nearest directory down to the code you will touch.
- **Update as you go.** During or after a task, update the affected `index.md`
  files in the same change (files added, moved, removed, or repurposed).
- **Tag cross-cutting concepts.** When a concept spans code and docs, create a
  tag, register it in `docs/tags.md`, place `@tag:<slug>` on the code and doc
  locations, and keep the registry current.

## Search commands

```bash
grep -rn "@tag:<slug>" .                     # all locations of a tag
grep -oE "@tag:[a-z0-9-]+" path/to/file      # tags on a file
grep -rhoE "@tag:[a-z0-9-]+" . | sort -u     # all tags in the repo
```

## Done

After installing, tell the user what you created/changed: the `index.md` files
added, `docs/tags.md`, any tags placed, and the agent-guide section. From now on,
follow the imperatives above on every task in this repository.
