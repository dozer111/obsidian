```sql
-- EXPLAIN ANALYZE request

explain analyze select * from event_bus WHERE (player_id::numeric % 5) + 1 = 3;
explain analyze select id,name from products;
```