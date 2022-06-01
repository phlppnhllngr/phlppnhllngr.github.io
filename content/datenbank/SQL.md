---
tags: [Notebooks/Datenbank]
title: SQL
created: '2021-05-18T08:08:20.752Z'
modified: '2021-09-05T11:51:39.598Z'
parent: Datenbank
---

# SQL
- Prepared statements
  - *a prepared statement or parameterized statement is a feature used to execute the same or similar database statements repeatedly with high efficiency. ... The application may execute the statement as many times as it wants with different values*

## SQL lernen
- **sqlbolt**
  - *a series of interactive lessons and exercises designed to help you quickly learn SQL right in your browser*
  - <https://sqlbolt.com/>
- **Buch "the art of postgresql"**
  - <https://theartofpostgresql.com>
- **use-the-index-luke**
  - *A site explaining SQL indexing to developers*
  - *SQL indexing is the most effective tuning method—yet it is often neglected during development. Use The Index, Luke explains SQL indexing from grounds up and doesn’t stop at ORM tools like Hibernate.*
  - <https://use-the-index-luke.com/>
- <https://hinty.io/devforth/sql-query-optimization-understanding-key-principle>
- *Rule #1: If its linked by it, filtered by it, or sorted by it....index by it.*


## Tools
- **sqlglot**
  - *Python SQL Parser and Transpiler*
  - *Easily translate from one dialect to another.*
  - unterstütze Dialekte: <https://github.com/tobymao/sqlglot/blob/main/sqlglot/dialects.py>
  - <https://github.com/tobymao/sqlglot> *250
- **jooq translate**
  - *translate any SQL statement(s) to a different dialect*
  - <https://www.jooq.org/translate/>
- **sqlfluff**
  - Linter
  - Python
  - beta (18.5.21)
  - <https://github.com/sqlfluff/sqlfluff>
- **SQLPad**
  - *A web app for writing and running SQL queries and visualizing the results.*
  - *supports Postgres, MySQL, SQL Server, ClickHouse, Crate, Vertica, Trino, Presto, SAP HANA, Cassandra, Snowflake, Google BigQuery, SQLite, TiDB and many more via ODBC.*
  - <https://github.com/sqlpad/sqlpad>
- **SQL Fiddle**
  - MySQL, MS SQL Server, PostgreSQL, SQLite
  - <http://sqlfiddle.com/> 


## Schnipsel
- **composite key**
  - `create table mytable (col1, col2, primary key(col1, col2))`
- **insert on duplicate key update**
  - ```
    create table persons(id int primary key, lastname varchar)
    insert into persons(id, lastname) values (1, 'Miller') -- insert 1
    insert into persons(id, lastname) values (1, 'Smith') on duplicate key update lastname = 'Smith' -- update 1
    insert into persons(id, lastname) values (2, 'Jonson') on duplicate key update lastname = 'Jonson' -- insert 2
    insert into persons(id, lastname) values (2, 'Jonson') on duplicate key update lastname = 'Jonson' -- 0 row(s) affected
    ```
- **insert ignore**
  - kein insert bei
    - duplicate key (primary key, unique)
    - null obwohl not null constraint
  - `insert ignore into persons (...) values (...)`
- **replace**
- **merge**
- **insert wenn nicht schon vorhanden**
  - `insert into persons(firstname, lastname) select 'John', 'Smith' where not exists (select 1 from persons where firstname = 'John' and lastname = 'Smith')` 
- <u>joins</u>
  - (inner) join
    - *Returns records that have matching values in both tables* 
  - left (outer) join
    - *Returns all records from the left table, and the matched records from the right table* 
  - right (outer) join
    - *Returns all records from the right table, and the matched records from the left table* 
  - full (outer) join
    - *Returns all records when there is a match in either left or right table*
  - cross join
  - natural join
- <u>Funktionen</u>
  - current_timestamp
  - utc_timestamp
  - unix_timestamp 
