---
description: "Where to put @tag: tokens in Java code."
paths: ["**/*.java"]
---

# llm-wiki-tags — tags in Java

The `@tag:<slug>` token goes in a comment immediately above the element it marks.
Any comment style works — `//`, `/* */` or Javadoc; prefer Javadoc where the
element already has documentation, so the tag travels with the API docs. Multiple
tags are space-separated. Format and registry: [`tags.md`](tags.md).

- **Package** — in `package-info.java`, in the Javadoc above the `package`
  declaration:
  ```java
  /**
   * Payments domain.
   * @tag:payments
   */
  package com.example.payments;
  ```
- **File** — a comment at the very top of the `.java` file, above `package`:
  ```java
  // @tag:payments
  package com.example.payments;
  ```
- **Class** (also interface, enum, record) — directly above the declaration:
  ```java
  /** Charges a card. @tag:payments @tag:payments/retry */
  public class ChargeService { ... }
  ```
- **Method** — directly above the method:
  ```java
  // @tag:payments/retry
  public void charge(Card card) { ... }
  ```
