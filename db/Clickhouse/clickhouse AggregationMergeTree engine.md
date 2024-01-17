---
tags:
 Clickhouse
---

AggregationMergeTree - движок який дозволяє використовувати агрегаційні функції в колонках

https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/aggregatingmergetree

З мого досвіду, такий движок покладається на так звані "state" функції: https://clickhouse.com/docs/en/sql-reference/aggregate-functions/combinators#-state

Наприклад, є MV

```sql
CREATE MATERIALIZED VIEW spin_dates  
            ENGINE = AggregatingMergeTree()  
                PARTITION BY BrandID  
                ORDER BY (BrandID, PlayerID)  
AS  
SELECT  
    BrandID,  
    PlayerID,  
    minState(CreatedAt) as MinCreatedAtState,  
    maxState(CreatedAt) as MaxCreatedAtState  
FROM  
    journal2  
WHERE EntryType = 'bet'  
GROUP BY  
    BrandID,  
    PlayerID;
```


тут колонки це 

```
BrandID,  
PlayerID,  
minState(CreatedAt) as MinCreatedAtState,  
maxState(CreatedAt) as MaxCreatedAtState  
```


суть `minState`, `maxState` - це не конкретні дані(напряму через select значення не достанеш), а певний агрегований стан даних

щоб достати дані з такої таблиці, користуємось іншими агрегуючими функціями(згідно оф. доків)

```sql
SELECT PlayerID Player  
FROM spin_dates  
WHERE  
    BrandID = 1
GROUP BY PlayerID  
HAVING minMerge(MinCreatedAtState) BETWEEN '%s' and '%s'
```




-  ClickHouse AggregateFunctions and AggregateState https://medium.com/@f1yegor/clickhouse-aggregatefunctions-and-aggregatestate-e3fd46b7be74