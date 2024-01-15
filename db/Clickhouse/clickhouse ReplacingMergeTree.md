---
tags:
 Clickhouse
 Clickhouse_table_engine
---

# ReplacingMergeTree

MergeTree з можливістю видаляти дублікати

Дублікати - 2+ записи з однаковим значенням "order by" ключа

by-default - залишається тільки найновіший дублікат


```sql
-- without ver - the last inserted 'wins'  
CREATE TABLE myFirstReplacingMT  
(  
`key` Int64,  
`someCol` String,  
`eventTime` DateTime  
)  
ENGINE = ReplacingMergeTree  
ORDER BY key;  
  
INSERT INTO myFirstReplacingMT Values (1, 'first', '2020-01-01 01:01:01');  
INSERT INTO myFirstReplacingMT Values (1, 'second', '2020-01-01 00:00:00');  
  
SELECT * FROM myFirstReplacingMT FINAL;  
  
┌─key─┬─someCol─┬───────────eventTime─┐  
│ 1 │ second │ 2020-01-01 00:00:00 │  
└─────┴─────────┴─────────────────────┘
```

---

Варто мати на увазі, що 

- дедуплікація відбувається на етапі мержів(а значить не відразу а у відносно довільний час)
- дедуплікація відбувається в межах партиції. Якщо партиція часова - можуть бути дублі коли дані задублюються в кінець старої партиції і на початок нової


---


## Статті

- clickhouse docs https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/replacingmergetree
- 