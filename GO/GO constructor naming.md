---
tags:
 GO
 naming
 constructorNaming
---

загалом, в GO прийнята практика іменування конструктора в стилі `New<Type>`

> NewFile()
> NewStoragePG()
> NewStorageMongo()
> NewStringDescriptor()

---

https://google.github.io/styleguide/go/decisions#package-vs-exported-symbol-name

якщо пакет має тільки 1 експортований тип, і ім'я типа співпадає з назвою пакета (widget/Widget,storage/Storage, ...) - пишемо більш простий конструктор `New`, тому що

1. це легше читати
2. з контексту зрозуміло що ж саме буде повернуто

> bad: widget.NewWidget()
>> good: widget.New()

> bad: money.NewMoney()
>> good: money.New()

---


# Flashcards

в якому випадку треба писати повне ім'я в конструкторі (`New<Type>`)
?
тоді, коли в пакеті декілька імпортованих структур, і так сходу буде не зрозуміло, що ж саме верне конструктор

в якому випадку можна написати скорочене ім'я конструктора `New`
?
тоді, коли в пакеті тільки одна експортована структура, і з контексту буде прекрасно зрозуміло що саме повернеться.
Приклади:
```go
m := money.New()
d := decimal.New()

s := storage.New()
```