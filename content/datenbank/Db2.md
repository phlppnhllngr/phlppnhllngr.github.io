---
title: Db2
parent: Datenbank
---

# Db2
- "LUW" = Linux, Unix, Windows

## CLI
```
db2start
su - db2admin
db2ilist -> listet alle Instanzen
db2 attach to <instance>
db2 create database foo
db2 connect to foo
db2 create schema bar
db2 create table bar.baz ...
db2stop
```

## Docker
- [Installing the Db2 Community Edition Docker image on Windows systems](https://www.ibm.com/docs/en/db2/11.5?topic=SSEPGG_11.5.0/com.ibm.db2.luw.qb.server.doc/doc/t_install_db2CE_win_img.html)
- <https://hub.docker.com/r/ibmcom/db2>
- select from update
- ````
  db2 "create table foo(id int generated always as identity, bar varchar(255))"
  db2 "select bar from final table (update foo set bar = 'D' where id = 1)"
  ```

## Transaktionen
- *there is no BEGIN TRANSACTION statement*
- *The transaction begins on the first statement after a previous transaction ends, or after a connect. The transaction ends when there is a COMMIT, or a ROLLBACK. But any COMMIT can either be explicit in your code, or implicit made by the tool that submits the SQL (in this case IBM Data Studio) by autocommit after each line. Usually autocommit is the default behaviour for such tools, but is configurable.*
- Auto-Commit in CLI ausschalten und manuell committen: `db2 +c "update..." / db2 commit`
- *DB2 has 4 isolation levels. All 4 have advantages and disadvantages.*

### Isolation Levels
- **Repeatable Read (RR)**
  - JDBC: Serializable
  - *means that the same query can be executed multiple times within the same unit of work, and the results of the query will be identical every time (repeatable).*
  - *A Share lock will be set and will stay on each row or page until the query or logical unit of work has completed.*
  - *All Share locks with RR are held until a commit takes place. These share locks would effectively prevent updates, inserts, or deletes (X locks) from occurring on any of the rows/pages from any other process until a commit is executed.*
  - *Select query with RR obtains Shared Lock at table level*
- **Read Stability (RS)**
  - JDBC: Repeatable Read
  - *enables an application to read the same pages or rows more than once and prevents updates or deletes to qualifying rows by other processes. However, other applications can insert or update rows that did not satisfy the search condition of the original application.*
  - *With RS is very much like With RR, except that it will allow inserts from other users.*
  - *Select query `with RS` obtains Shared Locks at row level [locks each selected row] and an IS (intent share) lock at the table level*
  - *Select query `with RS use and keep shared/update/exclusive locks` to obtain other locks [at row level] and an IX (intent exclusive) lock at the table level*
- **Cursor Stability (CS)**
  - default
  - JDBC: Read Committed
  - *sets a Share lock on each row or page processed, and the moment the cursor moves on to another row or page, it releases the lock.*
  - *So at any one time, there is only one lock being held either on a row or page of data. This obviously allows good concurrency and some data integrity.*
- **Uncommitted Read (UR)**
  - JDBC: Uncommitted Read
  - *means that no Share locks are placed on any rows or pages processed by this query, and it does not matter if other processes have any locks on any of the data being retrieved.*
  - *This can improve efficiency because it reduces overall processing time. But the one issue in using UR is that if some other process has applied updates to data being retrieved, UR will return the updated data from the buffer before the other process has executed a commit.*
  - *If for some reason the other process does a rollback of its updates, then this UR process has updated data that was never committed.*
  - *Select query with UR obtains Shared Lock at row level*
  - `select lastname from persons where firstname = 'John' with UR`
- **das derzeitige Isolation-Level erhalten:**
  ```
  db2 "values(current isolation)" (anf??nglich null)
  oder
  db2 "values current isolation"
  oder
  db2 "select current isolation from sysibm.sysdummy1"
  ```
- **das Isolation-Level setzen**: `db2 "SET CURRENT ISOLATION ur/rr/cs/rs"`

## Locking
- List the current database activities: `db2top -d [dbname]`
- This command will show you database locks: `db2pd -d [dbname] -lock wait`
- `db2 list applications` (Agent-ID = Appl. Handle) -> `db2 get snapshot for locks for application agentid <?>`
- **Skip locked**
  - *specifies that rows are skipped when incompatible locks that would block the progress of the statement are held on the rows by other transactions. These rows can belong to any accessed table that is specified in the statement. SKIP LOCKED DATA can be used only with isolation CS or RS and applies only to row level or page level locks.* [Quelle](https://www.ibm.com/docs/en/db2-for-zos/12?topic=statement-skip-locked-data)
  - `select foo from bar where x = y skip locked data`