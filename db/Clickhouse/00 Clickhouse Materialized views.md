---
tags:
 Clickhouse
---

Materialized View - одна з технік для пришвидшення запитів

Її суть - створюється щось типу таблиці. Mv прив'язується до певної таблиці звідки вона буде брати дані. Як тільки в оригінальну таблицю робиться INSERT, то ці ж дані додатково ідуть і в MV.

Таким чином ми маємо якусь свою унікальну окрему псевдотаблицю, яка оперує оригінальними даними

Загалом - починати ознайомлення варто з цієї статті: https://clickhouse.com/docs/en/optimize/sparse-primary-indexes#options-for-creating-additional-primary-indexes

---

## Особливості:

- МV ніяким чином не стягує старі дані з оригінала сама.
- Якщо в оригіналі є зміни(що не пов'язані з INSERT, наприклад архівування партиції) - MV про це не в курсі(тобто MV може показувати те, чого в самій базі вже давно немає)

Якщо є необхідність докинути певні дані з оригіналу в MV - це треба робити якось вручну. Такий процес докидання "старих" даних називається "backfill"

- Backfill/populate MV in a controlled manner https://kb.altinity.com/altinity-kb-schema-design/materialized-views/backfill-populate-mv-in-a-controlled-manner/

---

## Queries

```sql
-- очистити MV
Alter TABLE partitionNam DELETE WHERE 1 == 1
```
