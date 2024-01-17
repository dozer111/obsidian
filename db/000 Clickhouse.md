---
tags:
 MOC
 DB
 Clickhouse
---

MAIN => [[Main]] <= 

---

- queries [[Clickhouse Queries]]
- materialized views [[00 Clickhouse Materialized views]]
- table engines [[00 Clickhouse table engines]]

---

### Гарні ресурси для ознайомлення

- skip indexes https://altinity.com/blog/clickhouse-black-magic-skipping-indices
- replacingMergeTree https://chistadata.com/replacingmergetree-engine-in-clickhouse/
- (Y) more secrets of ch query performance https://www.youtube.com/watch?v=1TGGCIr6dMY
- байка про партиції і як їх використовувати https://medium.com/datadenys/using-partitions-in-clickhouse-3ea0decb89c4
- як вибрати партиційний ключ https://kb.altinity.com/engines/mergetree-table-engine-family/pick-keys/
- debugging memory issues https://clickhouse.com/docs/en/guides/developer/debugging-memory-issues
- варіанти для "multiple primary index"(частина статті в якій розповідається про projection, mv та іншу таблицю) https://clickhouse.com/docs/en/optimize/sparse-primary-indexes#options-for-creating-additional-primary-indexes
- how much is too much? https://kb.altinity.com/altinity-kb-schema-design/how-much-is-too-much/

#### projections

https://medium.com/datadenys/using-projections-to-speedup-queries-in-clickhouse-cd58e393b1cd

класна початкова стаття


---

https://kb.altinity.com/altinity-kb-queries-and-syntax/projections-examples/

класна стаття для розширення

- приклад агрегуючої проекції
- приклад роботи з `allow_experimental_projection_optimization`
- оптимізація через subselect

---