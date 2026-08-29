---
description: "Where to put @tag: tokens in Go code."
paths: ["**/*.go"]
---

# llm-wiki-tags — tags in Go

The `@tag:<slug>` token goes in a `//` comment (or `/* */`) immediately above the
element; prefer the element's doc comment, so the tag lives with `go doc` output.
Go has no classes — the class-level granularity maps to a **type**. Multiple tags
are space-separated. Format and registry: [`tags.md`](tags.md).

- **Package** — in the package doc comment above the `package` clause; for a
  package spanning several files use a dedicated `doc.go`:
  ```go
  // Package payments handles charging.
  // @tag:payments
  package payments
  ```
- **File** — a `//` comment at the top of the `.go` file. A comment directly above
  `package` is the *package* doc comment, so for a file-scoped tag put it on the
  file's first declaration instead.
- **Type** (struct / interface) — directly above the `type`:
  ```go
  // ChargeService charges a card. @tag:payments
  type ChargeService struct{ ... }
  ```
- **Function / method** — directly above `func`:
  ```go
  // @tag:payments/retry
  func (s *ChargeService) Charge(c Card) error { ... }
  ```
