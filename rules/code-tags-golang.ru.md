---
description: "Куда ставить токены @tag: в Go-коде."
paths: ["**/*.go"]
---

# llm-wiki-tags — тэги в Go

Токен `@tag:<slug>` ставится в `//`-комментарии (или `/* */`) прямо над
элементом; лучше — в doc-комментарий элемента, чтобы тэг попадал в вывод
`go doc`. Классов в Go нет: уровень класса — это **тип**. Несколько тэгов — через
пробел. Формат и реестр: [`tags.md`](tags.md).

- **Пакет** — в doc-комментарии пакета над строкой `package`; для пакета из
  нескольких файлов заведи отдельный `doc.go`:
  ```go
  // Package payments handles charging.
  // @tag:payments
  package payments
  ```
- **Файл** — `//`-комментарий вверху `.go`-файла. Комментарий прямо над `package`
  — это doc-комментарий *пакета*, поэтому тэг уровня файла ставь на первое
  объявление в файле.
- **Тип** (struct / interface) — прямо над `type`:
  ```go
  // ChargeService charges a card. @tag:payments
  type ChargeService struct{ ... }
  ```
- **Функция / метод** — прямо над `func`:
  ```go
  // @tag:payments/retry
  func (s *ChargeService) Charge(c Card) error { ... }
  ```
