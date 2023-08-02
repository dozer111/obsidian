---
tags:
 DB
 PostgreSQL
 PostreSQL explain
---

Main => [[Main]]
00 => [[002 PG explain]]


оригінальна стаття:  https://www.depesz.com/2013/04/16/explaining-the-unexplainable/
переклад habr: https://habr.com/ru/articles/275851/


операція - дія, яку можна побачити
- на першій строці query плана
- на інших строках, які починаються з `->`


QP1 => запит виконався в одну операцію

```                                                                  
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Index Only Scan using idx_brand_player_currency on players_balances  (cost=0.56..231064.07 rows=1245448 width=8) (actual time=0.046..2541.325 rows=1370404 loops=1)
   Index Cond: ((brand_id = 4) AND (currency_id = ANY ('{4}'::integer[])))
   Heap Fetches: 14783
 Planning time: 1.970 ms
 Execution time: 2620.402 ms
(5 rows)
```

QP2 => 2 операції
```
 Bitmap Heap Scan on players_balances  (cost=49656.43..765932.22 rows=3070094 width=8) (actual time=366.532..18151.541 rows=3349685 loops=1)
   Recheck Cond: ((brand_id = 5) AND (currency_id = ANY ('{3}'::integer[])))
   Rows Removed by Index Recheck: 29124543
   Heap Blocks: exact=38212 lossy=524990
   ->  Bitmap Index Scan on balance_currency  (cost=0.00..48888.91 rows=3070094 width=0) (actual time=352.922..352.922 rows=3359173 loops=1)
         Index Cond: ((brand_id = 5) AND (currency_id = ANY ('{3}'::integer[])))
 Planning time: 0.097 ms
 Execution time: 18355.219 ms
```


QP3 => 5 операцій
```
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



# Flashcards

що таке "операція" в queryPlan
?
це дія(одна з дій), що виконується в 