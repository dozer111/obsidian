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