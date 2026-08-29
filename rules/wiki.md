---
description: "Documentation is an LLM wiki — an index.md in every meaningful directory; read before acting, update as you go."
---

# llm-wiki-tags — the wiki

Documentation in this repository is an **LLM-readable wiki** ([llm-wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
by Andrej Karpathy) **plus tags**. Companion rules: [`docs-layout.md`](docs-layout.md)
(where pages live), [`tags.md`](tags.md) (the tag mechanism).

1. **Every meaningful directory has an `index.md`** giving a one-line description
   of each file and each sub-directory in it.
2. **Bidirectional navigation**: a parent index links to its child pages; every
   page links back to its parent index and to related pages.
3. **One page owns a detail**; other pages link to it instead of repeating it.
4. Pages describe stable concepts, not changelogs. Prefer many small,
   single-purpose pages over one large document, and hierarchy over a flat list.
5. **Read before you act.** Before a task, walk `index.md` from the repository
   root down to the files you are going to touch.
6. **Update as you go.** In the same change, update every `index.md`, doc page and
   tag affected by what you added, moved, removed or repurposed. Documentation
   that no longer matches the code is a defect, not a backlog item.
