---
description: "All documentation lives under docs/ — specification, implementation, testing (by tag) and requests (per-task working files)."
---

# llm-wiki-tags — documentation layout

Companion rules: [`wiki.md`](wiki.md) (index rules), [`tags.md`](tags.md) (tags).

```
docs/
├── index.md                      # index of the documentation
├── tags.md                       # tag registry
├── specification/                # what the program looks like from outside
│   ├── index.md
│   ├── payments.md               # a small area: one page
│   └── payments/                 # a grown area: a directory with its own index.md
│       ├── index.md
│       └── retry.md
├── implementation/               # how it is built inside — same shape
├── testing/                      # how it is tested: strategy, test cases
└── requests/                     # working files of individual tasks
    └── <task_name>/              # request.md, plan.md, debug scripts, notes
```

1. **All documentation lives under `docs/`.** The repository root keeps only what
   must be there: `AGENTS.md`, `CLAUDE.md`, the readme, the license, and files
   that tooling requires at the root (`package.json`, `pyproject.toml`, `go.mod`,
   `Makefile`, CI config, …). Nothing else.
2. **`docs/specification/`** — how the program looks to an outside user: features,
   interfaces, formats, behaviour. **`docs/implementation/`** — how it is built
   inside. **`docs/testing/`** — how it is tested, plus test cases. A page belongs
   to exactly one of the three.
3. **These three trees are organised by tag.** A tag becomes a page
   (`docs/implementation/payments.md`) or, once it grows, a directory with an
   `index.md` (`docs/implementation/payments/`). Both tags and directories are
   **hierarchical, and hierarchy is preferred**: `@tag:payments/retry` ↔
   `docs/implementation/payments/retry.md`.
4. **Naming a file after a tag is preferred, not required.** A page usually
   carries several tags; use a tag as the file name only when that tag is the
   page's main subject. Every tag a page carries goes into its front matter
   regardless of the file name.
5. **Per-task working files go to `docs/requests/<task_name>/`** — the task
   statement (`request.md`), the plan (`plan.md`), debug scripts, scratch notes.
   They are the trail of one task, not part of the permanent wiki: never leave
   such files at the repository root or next to the code.
6. **What outlives the task moves out of `requests/`.** When a task changes how
   the program looks, works or is tested, that knowledge lands in
   `specification/`, `implementation/` or `testing/` in the same change — the
   request folder stays as history and is not the place to look things up.
7. Every directory under `docs/` carries an `index.md` (see [`wiki.md`](wiki.md)).
