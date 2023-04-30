---
title: SQL
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
- <https://hinty.io/devforth/sql-query-optimization-understanding-key-principle>


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
- **PRQL**
  - *a modern language for transforming data — a simple, powerful, pipelined SQL replacement*
  - compiled zu SQL
  - <https://prql-lang.org/> 


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
  - *the INSERT IGNORE can also increments the auto-increment value when the insertion fails*
- **replace**
  - *MySQL actually does a DELETE followed by an INSERT internally, which has some unexpected side effects: A new auto-increment ID is allocated. Dependent rows with foreign keys may be deleted (if you use cascading foreign keys) or else prevent the REPLACE.*
- **merge**
- **insert wenn nicht schon vorhanden**
  - `insert into persons(firstname, lastname) select 'John', 'Smith' where not exists (select 1 from persons where firstname = 'John' and lastname = 'Smith')`
  - mögliche Alternative (?): `IF NOT EXISTS(QUERY) Then INSERT`
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
  - current_timestamp()
    - *In MySQL, the CURRENT_TIMESTAMP returns the current date and time in ‘YYYY-MM-DD HH:MM:SS’ format or YYYYMMDDHHMMSS.uuuuuu format depending on whether numeric or string is used in the function. NOW() and CURRENT_TIMESTAMP() are the synonym of CURRENT_TIMESTAMP.*
    - *determined by the time zone of your MySQL server.*
  - utc_timestamp()
    - *used to check current Coordinated Universal Time (UTC) date and time value. It returns the current UTC date and time value in YYYY-MM-DD HH:MM:SS or YYYYMMDDHHMMSS.uuu format, depending on whether the function is used in string or numeric context.* 
  - unix_timestamp(date?)
    - *The server interprets date as a value in the current time zone and converts it to an internal value in UTC.* 
    - returned Unix-Zeitstempel (Sekunden von 1970-01-01 00:00:00 bis date-Argument bzw. bis jetzt) 
