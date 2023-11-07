---
tags:
 Clickhouse
---

00 => [[000 Clickhouse]]

### звіт по проекціям
```sql
SELECT  
    database,  
    table,  
    name,  
    formatReadableSize(sum(data_compressed_bytes) AS size) AS compressed,  
    formatReadableSize(sum(data_uncompressed_bytes) AS usize) AS uncompressed,  
    round(usize / size, 2) AS compr_rate,  
    sum(rows) AS rows,  
    count() AS part_count  
FROM system.projection_parts  
WHERE active  
GROUP BY  
    database,  
    table,  
    name  
ORDER BY size DESC;
```

### покажи таблиці, rowsCount, і скільки займають по-пам'яті
```sql
SELECT 
    database,
    table,
    formatReadableSize(sum(bytes)) as size,
    sum(rows) as row_count
FROM system.parts 
WHERE active 
GROUP BY database, table 
ORDER BY database, table;
```

### покажи мені всі materializedView
```sql
SELECT 
	database, 
	name AS materialized_view_name, 
	engine 
FROM system.tables 
WHERE 
	engine = 'MaterializedView' 
	AND database NOT IN ('system');
```
