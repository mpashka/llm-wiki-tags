# Простановка тэгов в коде Go

*Языки: [English](golang.md) · **Русский** — Родитель: [индекс языков](index.ru.md)*

Тэг — это токен `@tag:<slug>` внутри `//`-комментария (или `/* */`) прямо над
элементом. Лучше ставить в doc-комментарий элемента, чтобы тэг попадал в вывод
`go doc`. В Go нет классов — уровень «класс» отображается на **тип**
(struct/interface). Несколько тэгов — через пробел (`@tag:payments @tag:retry`).

## Уровни

- **Пакет** — в doc-комментарии пакета над строкой `package`; для пакета из
  нескольких файлов используй отдельный `doc.go`:
  ```go
  // Package payments handles charging.
  // @tag:payments
  package payments
  ```

- **Файл** — `//`-комментарий в начале `.go`-файла. Внимание: комментарий прямо
  над `package` — это doc-комментарий *пакета*; для тэга на уровне файла ставь его
  на первое объявление в файле.

- **Тип** (struct / interface) — комментарий прямо над `type`:
  ```go
  // ChargeService charges a card. @tag:payments
  type ChargeService struct{ ... }
  ```

- **Функция / метод** — комментарий прямо над `func`:
  ```go
  // @tag:retry
  func (s *ChargeService) Charge(c Card) error { ... }
  ```
