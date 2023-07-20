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

- `widget.NewWidget` - 