# Домашнее задание к занятию "6.4. PostgreSQL"

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

```yml
version: '3.1'
services:
  postgresql:
    image: postgres:13
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    volumes:
      - ./dbdata:/var/lib/postgresql/data
      - ./dbbackup:/var/lib/postgresql/backup
```

Подключитесь к БД PostgreSQL используя `psql`.

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:
- вывода списка БД  
`\l`
- подключения к БД  
`\c {db_name}`
- вывода списка таблиц  
`\dt`
- вывода описания содержимого таблиц  
`\d {table_name}`
- выхода из psql  
`\q`

## Задача 2

Используя `psql` создайте БД `test_database`.

```
postgres=# CREATE DATABASE test_database;
CREATE DATABASE
```

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

```
postgres=# \c test_database
You are now connected to database "test_database" as user "postgres".

test_database=# ANALYZE VERBOSE orders;
INFO:  analyzing "public.orders"
INFO:  "orders": scanned 1 of 1 pages, containing 8 live rows and 0 dead rows; 8 rows in sample, 8 estimated total rows
ANALYZE
```

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders`
с наибольшим средним значением размера элементов в байтах.

**Приведите в ответе** команду, которую вы использовали для вычисления и полученный результат.

```
test_database=# SELECT avg_width FROM pg_stats WHERE TABLENAME='orders';
 avg_width | attname
-----------+---------
         4 | id
        16 | title
         4 | price
(3 rows)
```

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам, как успешному выпускнику курсов DevOps в нетологии предложили
провести разбиение таблицы на 2 (шардировать на orders_1 - price>499 и orders_2 - price<=499).

Предложите SQL-транзакцию для проведения данной операции.

```
test_database=# ALTER TABLE orders RENAME TO orders_main;
ALTER TABLE

test_database=# CREATE TABLE orders (id integer, title varchar(80), price integer) PARTITION BY RANGE(price);
CREATE TABLE

test_database=# CREATE TABLE orders_small PARTITION OF orders FOR VALUES FROM (500) TO (MAXVALUE);
CREATE TABLE

test_database=# CREATE TABLE orders_big PARTITION OF orders FOR VALUES FROM (MINVALUE) TO (500);
CREATE TABLE

test_database=# INSERT INTO orders (id, title, price) SELECT * FROM orders_main;
INSERT 0 8

test_database=# SELECT * FROM orders_small;
 id |       title        | price
----+--------------------+-------
  2 | My little database |   500
  6 | WAL never lies     |   900
  8 | Dbiezdmin          |   501
(3 rows)

test_database=# SELECT * FROM orders_big;
 id |        title         | price
----+----------------------+-------
  1 | War and peace        |   100
  3 | Adventure psql time  |   300
  4 | Server gravity falls |   300
  5 | Log gossips          |   123
  7 | Me and my bash-pet   |   499
(5 rows)
```

Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?

> Да, если спроектировать её как секционированную.

## Задача 4

Используя утилиту `pg_dump` создайте бекап БД `test_database`.

```
root@53bcd551bd87:/var/lib/postgresql# pg_dump -U postgres test_database -f backup/dump_test_database.sql
```

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

```
CREATE TABLE public.orders (
    id integer NOT NULL,
    title character varying(80) NOT NULL,
    price integer DEFAULT 0,
    UNIQUE(title)
);
```
