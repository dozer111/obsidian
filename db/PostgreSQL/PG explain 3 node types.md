---
tags:
 DB
 PostgreSQL
 explain
---

00 => [[002 PG explain]]

оригінальна стаття:  https://www.depesz.com/2013/04/27/explaining-the-unexplainable-part-2/
переклад habr: https://habr.com/ru/articles/276973/
стаття про те, як взагалі працює запит в postgres: https://habr.com/ru/articles/304258/

---

отож, запит складається з операцій. Операції являють собою дерево, в якому кожна операція може бути основною, а може бути лише частиною чогось іншого

основні види операцій:
1. seq scan - почергове проходження по таблиці oneByOne
2. index scan - знаходим по індексу значення в таблиці, йдем в таблицю і вибираємо дані
3. index only scan - знаходимо все що потрібно в індексі, в таблицю вже не йдемо
4. Bitmap Index Scan - створюється бітова карта сторінок на яких можуть бути дані, далі почергово проходимось по сторінках і дістаємо дані


# Flashcards

які є типи операцій в query plan
? 
1. seq scan
2. index scan
3. index only scan
4. bitmap index scan

що такe `seq scan`
? 
це тип вибірки(операція), коли ми по-черзі проходимось по таблиці і її значенням, і таким чином перебираємо всю таблицю(або скільки треба) в пошуках даних

що такe `index scan`
?

що такe `index only scan`
?

що такe `bitmap index scan`
?

що значить, коли у нас `index scan`
?

що значить, коли у нас `index only scan`
?

що краще: `index scan` чи `index only scan`
?



