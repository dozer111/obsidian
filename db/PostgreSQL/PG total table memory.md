---
tags:
 DB
 PostgreSQL
---

Main => [[Main]]


скільки пам'яті займає таблиця:
```sql
SELECT pg_size_pretty(pg_total_relation_size('players_balances'));
```