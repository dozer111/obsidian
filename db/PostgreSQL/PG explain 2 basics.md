---
tags:
 DB
 PostgreSQL
---

Main => [[Main]]
00 => [[002 PG explain]]

оригінальна стаття:  https://www.depesz.com/2013/04/16/explaining-the-unexplainable/
переклад habr: https://habr.com/ru/articles/275851/

Базово з `explain analyze` ми можемо дізнатись:

- скільки часу затратилось на виконання запиту
- скільки рядків даних знайдено
- за скільки циклів вибрались дані


```
For example:
                                                        QUERY PLAN
---------------------------------------------------------------------------------------------------------------------------
 Sort  (cost=146.63..148.65 rows=808 width=138) (actual time=55.009..55.012 rows=71 loops=1)
   Sort Key: n.nspname, p.proname, (pg_get_function_arguments(p.oid))
   Sort Method: quicksort  Memory: 43kB
   ->  Hash Join  (cost=1.14..107.61 rows=808 width=138) (actual time=42.495..54.854 rows=71 loops=1)
         Hash Cond: (p.pronamespace = n.oid)
         ->  Seq Scan on pg_proc p  (cost=0.00..89.30 rows=808 width=78) (actual time=0.052..53.465 rows=2402 loops=1)
               Filter: pg_function_is_visible(oid)
         ->  Hash  (cost=1.09..1.09 rows=4 width=68) (actual time=0.011..0.011 rows=4 loops=1)
               Buckets: 1024  Batches: 1  Memory Usage: 1kB
               ->  Seq Scan on pg_namespace n  (cost=0.00..1.09 rows=4 width=68) (actual time=0.005..0.007 rows=4 loops=1)
                     Filter: ((nspname <> 'pg_catalog'::name) AND (nspname <> 'information_schema'::name))
```


розбираємо верхню строку `Sort  (cost=146.63..148.65 rows=808 width=138) (actual time=55.009..55.012 rows=71 loops=1)`:


## перші значення - затрати на отримання даних, і їх приблизні об'єми

### cost

`cost=146.63..148.65` - затрати на отримання даних

- 146.63 => перше значення => затрати на отримання першого рядка
- 148.65 => друга значення => загальні затрати на отримання всіх рядків

в нашому випадку видно що майже всі затрати на видачу даних йдуть саме на отримання першого рядка, тому що ми додатково сортуємо дані

якби ми не сортували, наші затрати можуть виглядати так: `cost=0.56..231064.07`


### rows 

приблизна кількість даних, які повернуться в результаті запиту

### width

скільк