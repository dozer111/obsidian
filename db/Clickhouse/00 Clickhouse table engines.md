---
tags:
 Clickhouse
---


Движки в clickhouse - способи зберігати та працювати з даними.

https://clickhouse.com/docs/en/engines/table-engines

---

Поки що я користуюсь переважно сімейством MergeTree

- MergeTree - просто збери дані в кучу
- ReplacingMergeTree - збери дані в кучу і по можливості відсій дублікати
- CollapsingMergeTree - збери дані, і якщо мені потрібно щось переписати - перепиши
- SummingMergeTree - класно для якихось лічильників коли власне повні дані не треба
- AggregatingMergeTree - таблиця заточена під роботу з функціями-агрегаціями(min,max, sum, uniq, ...)


