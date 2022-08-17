# Домашнее задание к занятию "6.2. SQL"

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 12) c 2 volume,
в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose манифест.

```yml
version: '2.1'
services:
    postgres:
        image: postgres:12
        restart: always
        environment:
          - POSTGRES_USER=postgres
          - POSTGRES_PASSWORD=postgres
        volumes:
          - ./db_data:/var/lib/postgresql/db_data
          - ./db_backup:/var/lib/postgresql/db_backup
```

## Задача 2

В БД из задачи 1:
- создайте пользователя test-admin-user и БД test_db

```SQL
CREATE DATABASE test_db;
CREATE ROLE "test-admin-user" WITH PASSWORD 'admin123';
```

- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже)

```SQL
CREATE TABLE orders (id integer PRIMARY KEY, name text, price integer);
CREATE TABLE clients (id integer PRIMARY KEY, surname text, country text, "order" integer, FOREIGN KEY ("order") REFERENCES orders (id));
CREATE INDEX countryid ON clients(country);
```

- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db

```SQL
GRANT ALL ON DATABASE test_db to "test-admin-user";
```

- создайте пользователя test-simple-user

```SQL
CREATE ROLE "test-simple-user" WITH PASSWORD 'user123';
```

- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE данных таблиц БД test_db

```SQL
GRANT SELECT,INSERT,UPDATE,DELETE ON TABLE public.clients TO "test-simple-user";
GRANT SELECT,INSERT,UPDATE,DELETE ON TABLE public.orders TO "test-simple-user";
```

Таблица orders:
- id (serial primary key)
- наименование (string)
- цена (integer)

Таблица clients:
- id (serial primary key)
- фамилия (string)
- страна проживания (string, index)
- заказ (foreign key orders)

Приведите:
- итоговый список БД после выполнения пунктов выше,

```
postgres=# \l
                                     List of databases
   Name    |  Owner   | Encoding |  Collate   |   Ctype    |       Access privileges
-----------+----------+----------+------------+------------+--------------------------------
 postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres                   +
           |          |          |            |            | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres                   +
           |          |          |            |            | postgres=CTc/postgres
 test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/postgres                  +
           |          |          |            |            | postgres=CTc/postgres         +
           |          |          |            |            | "test-admin-user"=CTc/postgres
(4 rows)

```

- описание таблиц (describe)

```
test_db-# \dp
                                     Access privileges
 Schema |  Name   | Type  |        Access privileges         | Column privileges | Policies
--------+---------+-------+----------------------------------+-------------------+----------
 public | clients | table | postgres=arwdDxt/postgres       +|                   |
        |         |       | "test-simple-user"=arwd/postgres |                   |
 public | orders  | table | postgres=arwdDxt/postgres       +|                   |
        |         |       | "test-simple-user"=arwd/postgres |                   |
(2 rows)
```

- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db

```SQL
test_db=# SELECT * FROM information_schema.role_table_grants WHERE grantee like 'test-simple-user' AND table_catalog = 'test_db' AND table_name IN ('clients', 'orders');

 grantor  |     grantee      | table_catalog | table_schema | table_name | privilege_type | is_grantable | with_hierarchy
----------+------------------+---------------+--------------+------------+----------------+--------------+----------------
 postgres | test-simple-user | test_db       | public       | orders     | INSERT         | NO           | NO
 postgres | test-simple-user | test_db       | public       | orders     | SELECT         | NO           | YES
 postgres | test-simple-user | test_db       | public       | orders     | UPDATE         | NO           | NO
 postgres | test-simple-user | test_db       | public       | orders     | DELETE         | NO           | NO
 postgres | test-simple-user | test_db       | public       | clients    | INSERT         | NO           | NO
 postgres | test-simple-user | test_db       | public       | clients    | SELECT         | NO           | YES
 postgres | test-simple-user | test_db       | public       | clients    | UPDATE         | NO           | NO
 postgres | test-simple-user | test_db       | public       | clients    | DELETE         | NO           | NO
(8 rows)
```

- список пользователей с правами над таблицами test_db

```
test_db=# \du
                                       List of roles
    Role name     |                         Attributes                         | Member of
------------------+------------------------------------------------------------+-----------
 postgres         | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 test-admin-user  | Cannot login                                               | {}
 test-simple-user | Cannot login                                               | {}
```

## Задача 3

Используя SQL синтаксис - наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|

```SQL
INSERT INTO orders VALUES (1, 'Шоколад', 10), (2, 'Принтер', 3000), (3, 'Книга', 500), (4, 'Монитор', 7000), (5, 'Гитара', 4000);
```

Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|

```SQL
INSERT INTO clients VALUES (1, 'Иванов Иван Иванович', 'USA'), (2, 'Петров Петр Петрович', 'Canada'), (3, 'Иоганн Себастьян Бах', 'Japan'), (4, 'Ронни Джеймс Дио', 'Russia'), (5, 'Ritchie Blackmore', 'Russia');
```

Используя SQL синтаксис:
- вычислите количество записей для каждой таблицы
- приведите в ответе:
    - запросы
    - результаты их выполнения.

```SQL
test_db=# SELECT COUNT (*) FROM clients;

 count
-------
     5
(1 row)

test_db=# SELECT COUNT (*) FROM orders;

 count
-------
     5
(1 row)
```

## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения данных операций.

```SQL
UPDATE clients SET "order" = 3 WHERE id = 1;
UPDATE clients SET "order" = 4 WHERE id = 2;
UPDATE clients SET "order" = 5 WHERE id = 3;
```

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.

```SQL
test_db=# SELECT * FROM clients WHERE "order" IS NOT NULL;
 id |       surname        | country | order
----+----------------------+---------+-------
  1 | Иванов Иван Иванович | USA     |     3
  2 | Петров Петр Петрович | Canada  |     4
  3 | Иоганн Себастьян Бах | Japan   |     5
(3 rows)
```

Подсказка - используйте директиву `UPDATE`.

## Задача 5

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните что значат полученные значения.

```SQL
test_db=# EXPLAIN SELECT * FROM clients WHERE "order" IS NOT NULL;
                        QUERY PLAN
-----------------------------------------------------------
 Seq Scan on clients  (cost=0.00..18.10 rows=806 width=72)
   Filter: ("order" IS NOT NULL)
(2 rows)
```

`cost=0.00..18.10` - "стоимость" получения первой строки и "стоимость" получения всех строк.  
`rows=806` - приблизительное количество возвращаемых строк.  
`width=72` - средний размер одной строки в байтах.

## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. Задачу 1).

```bash
root@a3e5d74c1840: pg_dump -U postgres test_db > /var/lib/postgresql/db_backup/test_db.sql
```

Остановите контейнер с PostgreSQL (но не удаляйте volumes).

```bash
asm@asm-edu:~/netology/06-db-02-sql$ sudo docker-compose stop postgres
Stopping 06-db-02-sql_postgres_1 ... done
```

Поднимите новый пустой контейнер с PostgreSQL.

Восстановите БД test_db в новом контейнере.

Приведите список операций, который вы применяли для бэкапа данных и восстановления.

```
asm@asm-edu:~/netology/06-db-02-sql$ sudo docker-compose ps
          Name                        Command              State     Ports
----------------------------------------------------------------------------
06-db-02-sql_postgres2_1   docker-entrypoint.sh postgres   Up       5432/tcp
06-db-02-sql_postgres_1    docker-entrypoint.sh postgres   Exit 0

asm@asm-edu:~/netology/06-db-02-sql$ sudo docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS          PORTS      NAMES
0730233f22c4   postgres:12   "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes    5432/tcp   06-db-02-sql_postgres2_1
a3e5d74c1840   postgres:12   "docker-entrypoint.s…"   2 days ago      Up 38 seconds   5432/tcp   06-db-02-sql_postgres_1

asm@asm-edu:~/netology/06-db-02-sql$ sudo docker exec -it 0730233f22c4 /bin/bash

root@0730233f22c4:/# psql -U postgres -c 'CREATE DATABASE test_db;'
CREATE DATABASE

root@0730233f22c4:/# psql -U postgres -d test_db -f /var/lib/postgresql/db_backup/test_db.sql
```
