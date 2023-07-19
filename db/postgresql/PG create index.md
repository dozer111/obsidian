```sql
CREATE INDEX idxName  
ON tableName condition;


CREATE UNIQUE INDEX CONCURRENTLY IF NOT EXISTS idxName  
ON tableName condition;
```

```sql
CREATE UNIQUE INDEX CONCURRENTLY IF NOT EXISTS event_bus_handle_5  
ON event_bus (((player_id::numeric % 5) + 1));
```