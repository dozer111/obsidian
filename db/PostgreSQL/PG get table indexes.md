---
tags:
 DB
 PostgreSQL
---

00 => [[000 PG]]

```sql
SELECT indexname  
FROM pg_indexes  
WHERE tablename = 'event_bus';
```

```sql
SELECT schemaname AS schema_name,  
       tablename AS table_name,  
       indexname AS index_name,  
       indexdef AS index_definition  
FROM pg_indexes  
WHERE tablename = 'players_balances'  
ORDER BY schemaname, tablename, indexname;
```