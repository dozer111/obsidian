---
tags:
 DB
 PostgreSQL
---

00 => [[000 PG]]

оригінальна стаття: https://www.tangramvision.com/blog/how-to-benchmark-postgresql-queries-well

---

створити функцію
```sql
CREATE FUNCTION bench(query TEXT, iterations INTEGER = 100)  
    RETURNS TABLE(avg FLOAT, min FLOAT, q1 FLOAT, median FLOAT, q3 FLOAT, p95 FLOAT, max FLOAT) AS $$  
DECLARE  
    _start TIMESTAMPTZ;  
    _end TIMESTAMPTZ;  
    _delta DOUBLE PRECISION;  
BEGIN  
    CREATE TEMP TABLE IF NOT EXISTS _bench_results (  
        elapsed DOUBLE PRECISION  
    );  
  
    -- Warm the cache  
    FOR i IN 1..5 LOOP  
            EXECUTE query;  
        END LOOP;  
  
    -- Run test and collect elapsed time into _bench_results table  
    FOR i IN 1..iterations LOOP  
            _start = clock_timestamp();  
            EXECUTE query;  
            _end = clock_timestamp();  
            _delta = 1000 * ( extract(epoch from _end) - extract(epoch from _start) );  
            INSERT INTO _bench_results VALUES (_delta);  
        END LOOP;  
  
    RETURN QUERY SELECT  
                     avg(elapsed),  
                     min(elapsed),  
                     percentile_cont(0.25) WITHIN GROUP (ORDER BY elapsed),  
                     percentile_cont(0.5) WITHIN GROUP (ORDER BY elapsed),  
                     percentile_cont(0.75) WITHIN GROUP (ORDER BY elapsed),  
                     percentile_cont(0.95) WITHIN GROUP (ORDER BY elapsed),  
                     max(elapsed)  
                 FROM _bench_results;  
    DROP TABLE IF EXISTS _bench_results;  
  
END  
$$  
    LANGUAGE plpgsql;
```

використовуємо функцію:
```sql
SELECT * FROM bench('SELECT columnName FROM mytableName WHERE c1=4 and c2 = ANY (array[3])');

select * from bench('select count(*) from tblName');
```


видалити функцію:
```sql
DROP function if exists bench(query TEXT, iterations INTEGER);
```

перевірити чи є вже така функція:
```sql
SELECT EXISTS (  
    SELECT 1  
    FROM pg_proc  
    WHERE proname = 'bench'  
);
```