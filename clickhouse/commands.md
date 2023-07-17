
select version();

---

подивитись, як саме записуються дані через async_insert
```sql
select event_time, flush_time, bytes,flush_query_id  
	from system.asynchronous_insert_log  
ORDER BY event_time DESC;
```