---
description: "Where to put @tag: tokens in Python code."
paths: ["**/*.py"]
---

# llm-wiki-tags — tags in Python

The `@tag:<slug>` token goes in a `#` comment immediately above the element, or
inside the element's docstring. Multiple tags are space-separated. Format and
registry: [`tags.md`](tags.md).

- **Package** — in the package's `__init__.py`, a top-of-file comment or the
  module docstring:
  ```python
  # @tag:payments
  ```
- **Module / file** — a `#` comment near the top of the `.py` file (below any
  `from __future__` import), or the module docstring:
  ```python
  """Payments domain. @tag:payments"""
  ```
- **Class** — a comment directly above `class`, or its docstring:
  ```python
  # @tag:payments
  class ChargeService:
      """Charges a card. @tag:payments/retry"""
  ```
- **Function / method** — a comment directly above `def`, or its docstring:
  ```python
  # @tag:payments/retry
  def charge(card): ...
  ```
