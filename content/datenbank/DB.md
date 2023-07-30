---
title: DB
parent: Datenbank
---

# DB
- <https://random-dev.medium.com/databases-in-5-min-bfd3b9bef86>
- <https://rakyll.medium.com/things-i-wished-more-developers-knew-about-databases-2d0178464f78>
- [The Database Cookbook For Developers](https://sqlfordevs.com/ebook)
- <https://planetscale.com/courses/mysql-for-developers/introduction/course-introduction>
- <https://www.crunchydata.com/blog/demystifying-database-performance-for-developers>
- **use-the-index-luke**
  - *A site explaining SQL indexing to developers*
  - *SQL indexing is the most effective tuning method—yet it is often neglected during development. Use The Index, Luke explains SQL indexing from grounds up and doesn’t stop at ORM tools like Hibernate.*
  - <https://use-the-index-luke.com/>
- *Rule #1: If its linked by it, filtered by it, or sorted by it....index by it.*
- <https://architecturenotes.co/things-you-should-know-about-databases/>

## IDs
- [Vlad Mihalcea: The best UUID type for a database Primary Key](https://vladmihalcea.com/uuid-database-primary-key/)
- **auto generated**
  - *doesn't go well with distributed dbs, sharding*
- **UUID**
  - <https://en.wikipedia.org/wiki/Universally_unique_identifier>
  - <https://www.ietf.org/id/draft-peabody-dispatch-new-uuid-format-03.html>
  - v7
    - <https://www.ietf.org/archive/id/draft-peabody-dispatch-new-uuid-format-04.html#name-uuid-version-7> 
- **Hash-ID**
  - <https://hashids.org/>
- **ULID**
  - Universally Unique Lexicographically Sortable Identifier
  - <https://github.com/ulid/spec>
- **Snowflake ID**
  - <https://en.wikipedia.org/wiki/Snowflake_ID>
    - *Snowflakes are sortable by time, because they are based on the time they were created. Additionally, the time a snowflake was created can be calculated from the snowflake. This can be used to get snowflakes (and their associated objects) that were created before or after a particular date.* 


## GUI Clients
- **dbeaver**
  - <https://github.com/dbeaver/dbeaver>
- **falcon**
  - <https://github.com/plotly/falcon> *4.8k
  - für Windows & Mac
  - SQL-Client & Visualisierung (Charts)
  - *supports connecting to RedShift, MySQL, PostgreSQL, IBM DB2, Impala, MS SQL, Oracle, SQLite and more*
- **jailer**
  - *Database Subsetting and Relational Data Browsing Tool.*
  - <https://github.com/Wisser/Jailer> *800
- **SQuirreL SQL**
  - <http://squirrel-sql.sourceforge.net>
- **DbVisualizer**
  - free/pro
  - <https://www.dbvis.com/>
- **DbSchema**
  - <https://dbschema.com/>


## Migration
- Um Änderungen an DBs in mehreren Umgebungen vorzunehmen ("schema migration"). Oft müssen dann auch bestehende Daten angepasst werden ("data migration").
- Test z.B. mit Lib "testcontainers"
- <https://kiranrao.ca/2022/05/04/zero-downtime-migrations.html>
  <br/>
  <https://news.ycombinator.com/item?id=31269515>
- **flyway**
  - *Flyway was sold a while ago and moved to an 'open core' business model: There is an open source edition (Apache 2.0) where critical feature (e.g. dry-run, rollback) were deliberately patched out, and a payed version (closed source) that adds those features back in.* 
  - Skripte: Java oder SQL (die Skripte sind abhängig vom DB-Vendor)
  - CLI oder embedded in (Java-)Anwendung  (beim Start der App)
  - *detects required update operations and executes them*
  - *current versions and updates stored in separate table*
  - *Supported databases: Oracle, SQL Server, DB2, MySQL, Aurora MySQL, MariaDB, Percona XtraDB Cluster, PostgreSQL, Aurora PostgreSQL, Redshift, CockroachDB, SAP HANA, Sybase ASE, Informix, H2, HSQLDB, Derby, SQLite, Firebird*
  - *Supported build tools: Maven and Gradle*
  - <https://github.com/flyway/flyway>
  - <https://flywaydb.org/>
  - <https://www.reddit.com/r/java/comments/t9krd1/how_we_run_database_migrations_with_flyway_jooq/.compact>
    <https://airbyte.com/blog/database-migrations-with-flyway-jooq-and-testcontainers>
- **liquibase**
  - kann - im Gegensatz zu flyway - DB-Vendor-unabhängige Migrationen (?)
  - *works with the following databases: Apache Derby, CockroachDB, Firebird, H2, HSQL, Informix, InterBase, MariaDB, MSSQL, MySQL, Oracle, PostgreSQL, SQLite, Sybase Anywhere, Sybase Enterprise.*
  - *The databases that require extensions are: Azure Cosmos DB, Cassandra, Cache, DB2i, Hibernate, Impala/Hive, MaxDB, MongoDB, Redshift, SAP HANA, SQLFire, Snowflake, Teradata, Vertica, VoltDB*
  - *can be integrated with Maven, Ant, Gradle, Spring Boot, and other CI/CD tools. You can use Liquibase GitHub Actions, Liquibase and Jenkins with Spinnaker, and many different workflows.*
  - <https://github.com/liquibase/liquibase>
  - <https://www.liquibase.org/>
- **bytebase**
  - *database schema change and version control management tool for teams*
  - *it supports 2 mainstream schema change workflow: UI based SQL review / Version control based schema migration (Database-as-Code)*
  - *Supported database engines: MySQL / Planned: PostgreSQL*
  - <https://github.com/bytebase/bytebase>
- **goose**
  - *Supports SQL migrations and Go functions*
  - <https://github.com/pressly/goose>
- **Prisma**
  - <https://www.prisma.io/migrate> 


## Change data capture
- **Debezium**
  - <https://github.com/debezium/debezium/> *1800
  - <https://debezium.io/>
  - *Monitoring databases and being notified when data changes. data streaming platform for change data capture (CDC). configure Debezium to monitor your databases, and then your applications consume events for each row-level change made to the database. reusing Kafka and Kafka Connect.*
  - *Common use cases: Cache invalidation, Simplifying monolithic applications, Data integration*


## Diverses
- **Sharding**
  - <https://en.wikipedia.org/wiki/Shard_(database_architecture)>
- **ACID**
  - Atomicity
  - Consistency
  - Isolation
    - *Isolation determines how transaction integrity is visible to other users and systems. It uses for resource locking i.e. concurrency control, make sure that only one transaction can access the resource at a given point.*
  - Durability
  - <https://en.wikipedia.org/wiki/ACID>

### Transactions
- *Transactions are usually used when you have CREATE, UPDATE or DELETE statements and you want to have the atomic behavior, that is, Either commit everything or commit nothing. However, you could use a transaction for READ select statements to: Make sure nobody else could update the table of interest while the bunch of your select query is executing.*

#### Transaction Isolation
- *Defines the data contract between transactions*
- *It is about how much a transaction may be impacted by the activities of other concurrent transactions. It a supports consistency leaving the data across many tables in a consistent state. It involves locking rows and/or tables in a database.*
- *Defaults may vary between difference databases. As an example, for MariaDB it is REPEATABLE READ.*
- *The different levels have different performance characteristics in a multi-threaded application*
- *level determines the duration that locks are held.*
- <u>Mögliche Probleme bei gleichzeitigen Transaktionen</u>
  - **Dirty Reads**
    - *A transaction reads data written by a concurrent uncommitted transaction.*
  - **Non-Repeatable Reads**
    - *A transaction re-reads data it has previously read and finds that data has been modified [updated] by another transaction (that committed since the initial read).*
  - **Phantom Reads / Phantom rows**
    - *A transaction re-executes a query returning a set of rows that satisfy a search condition and finds that the set of rows satisfying the condition has changed [inserts/deletes] due to another recently-committed transaction.*
    - *Suchkriterien treffen während einer Transaktion auf unterschiedliche Datensätze zu, weil eine (während des Ablaufs dieser Transaktion laufende) andere Transaktion Datensätze hinzugefügt, entfernt oder verändert hat.*
  - **Lost Update anomaly**
    - tritt auf bei read-modify-write
    - manche DBMS verhindern (Error) "gleichzeitige" Updates bei höheren Isolation Levels
    - <https://www.2ndquadrant.com/en/blog/postgresql-anti-patterns-read-modify-write-cycles/>
    <img src="https://i.stack.imgur.com/vCagm.png" loading="lazy"/>
    <br/><br/><img src="https://i.stack.imgur.com/y8ozP.jpg" loading="lazy"/>
    <pre>
    | Isolation Level | Oracle | SQL Server | PostgreSQL | MySQL |
    |-----------------|--------|------------|------------|-------|
    | Read Committed  | Yes    | Yes        | Yes        | Yes   |
    | Repeatable Read | N/A    | No         | No         | Yes   |
    | Serializable    | No     | No         | No         | No    |
    </pre>
- <u>Levels</u>
  - **Read Uncommitted**
    - *Allows to read changes [from another transaction] that haven’t yet been committed.*
    - Beste Performance, dafür anfällig für Dirty, Non-Repeatable und Phantom Reads
  - **Read Committed**
    - *Allows reads from concurrent transactions that have been committed.*
    - *states that a transaction can't read data that is not yet committed by other transactions.*
    - *When a transaction uses this isolation level, a SELECT query (without a FOR UPDATE/SHARE clause) sees only data committed before the query began; it never sees either uncommitted data or changes committed during query execution by concurrent transactions. In effect, a SELECT query sees a snapshot of the database as of the instant the query begins to run. However, SELECT does see the effects of previous updates executed within its own transaction, even though they are not yet committed.*
    - *setzt für die gesamte Transaktion Schreibsperren auf Objekten, die verändert werden sollen, setzt Lesesperren aber nur kurzzeitig beim tatsächlichen Lesen der Daten ein*
    - anfällig für Non-Repeatable und Phantom Reads
    - *The Lost Update anomaly can happen in the Read Committed isolation level.*
  - **Repeatable Read**
    - *states that if a transaction reads one record from the database multiple times the result of all those reading operations must always be the same.*
    - *If a row is read twice in the same transaction, the result will always be the same.*
    - *If T1 reads some data at the beginning and at the end of the transaction, Repetable reads assures that T1 sees the same data even if T2 changed the data and committed in the middle of T1.*
    - *sichergestellt, dass wiederholte Leseoperationen mit den gleichen Parametern auch dieselben Ergebnisse haben. Sowohl bei Lese- als auch bei Schreiboperationen werden für die gesamte Dauer der Transaktion Sperren gesetzt.*
    - Anfällig für Phantom Reads (nicht in Postgresql)
  - **Serializable**
    - Alle Read-Probleme ausgeschlossen, auf Kosten Performanz
    - *Transactions are executed with locking at all levels (read, range and write locking) so they appear as if they were executed in a serialized way.*
    - *garantiert, dass die Wirkung parallel ablaufender Transaktionen exakt dieselbe ist wie sie die entsprechenden Transaktionen zeigen würden, liefen sie nacheinander in Folge ab.*
    - *[Lost Updates] Kann auftreten, wenn eine Transaktion mit einer Leseoperation beginnt und später eine Schreiboperation durchführt. Wenn zwischen den beiden Operationen eine Transaktion eine Schreiboperation durchführt, greift diese auf dieselbe Version zu wie die erste. Deshalb geht eine der Schreibaktionen verloren.*<br/><br/>
  <pre>
  +---------------------------+-------------------+-------------+-------------+------------------------+
  | Isolation Level Mode      |  Read             |   Insert    |   Update    |       Lock Scope       |
  +---------------------------+-------------------+-------------+-------------+------------------------+
  | READ_UNCOMMITTED          |  uncommitted data | Allowed     | Allowed     | No Lock                |
  | READ_COMMITTED (Default)  |   committed data  | Allowed     | Allowed     | Lock on Committed data |
  | REPEATABLE_READ           |   committed data  | Allowed     | Not Allowed | Lock on block of table |
  | SERIALIZABLE              |   committed data  | Not Allowed | Not Allowed | Lock on full table     |
  +---------------------------+-------------------+-------------+-------------+------------------------+
  </pre>
  <pre>
  +---------------------------+----------------+----------------------+----------------+
  | Isolation Level Mode      |  Dirty reads   | Non-repeatable reads | Phantoms reads |
  +---------------------------+----------------+----------------------+----------------+
  | READ_UNCOMMITTED          | allows         | allows               | allows         |
  | READ_COMMITTED (Default)  | prevents       | allows               | allows         |
  | REPEATABLE_READ           | prevents       | prevents             | allows         |
  | SERIALIZABLE              | prevents       | prevents             | prevents       |
  +---------------------------+----------------+----------------------+----------------+
  </pre>

#### Locking
- *read operators acquire shared locks on the data they read, before reading the data*
- *write operators acquire exclusive locks on the data they modify before modifying the data*
- *incompatible requests are suspended until the incompatible grant blocking them is released*
- <u>Lock types</u>
  - **Shared (S)**
    - *also called read lock*
    - *ensure that a record is not in process of being updated during a read-only request.*
    - *can also be used to prevent any kind of updates of record.*
    - mehrere Transaktionen können gleichzeitig ein S-Lock besitzen
    - Warum kann es zu non-repeatable Reads kommen, wenn doch ein Select ein Shared Lock platziert und ein Update aber ein Exclusive lock erfordert?
      - *Even if shared row locks are taken (perhaps because another concurrent transaction has modified the page the row is on) they can be released long before the SELECT statement completes. In most cases, the row is 'unlocked' just before the server processes the next row. There are circumstances in which shared locks taken at the default isolation level are held to the end of the current statement, but not to the end of the transaction. Overriding the current isolation level with the NOLOCK table hint is almost always a bad idea. Locking is an implementation detail. SQL Server takes locks when necessary to ensure it meets the semantic guarantees provided by the current isolation level. There are certainly times where it is useful to know a little bit about why locks are taken, but attempting to predict them is very often counter-productive.*
      - *The shared lock type determines when it will be released. Row locks are released before the next row is processed. Page locks are released when the next page is read, and table locks are released when the statement finishes.*
      - *Your shared lock is immediately released after the select gets executed even it is inside the transaction. [SQL Server]*
      - *SQL Server uses by default READ COMMITTED as transaction isolation level, in which shared locks are acquired and released immediately. Should you want to use an exclusive lock for your SELECT then you need to use transaction level SERIALIZABLE.*
  - **Exclusive (X)**
    - *Also called write lock.*
    - *prevents any other locker from obtaining any sort of a lock on the object.*
    - *can be owned by only one transaction at a time.*
  - **Update (U)**
    - *Update Lock is kind of Exclusive Lock except it can be placed on the row which already have Shared Lock on it. Update Lock reads the data of row which has Shared Lock, as soon as Update Lock is ready to change the data it converts itself to Exclusive Lock.*
    - *Update locks prevent a common form of deadlock. A typical update pattern consists of a transaction reading a record, acquiring a shared (S) lock on the resource (page or row), and then modifying the row, which requires lock conversion to an exclusive (X) lock. If two transactions acquire shared-mode locks on a resource and then attempt to update data concurrently, one transaction attempts the lock conversion to an exclusive (X) lock. The shared-mode-to-exclusive lock conversion must wait because the exclusive lock for one transaction is not compatible with the shared-mode lock of the other transaction; a lock wait occurs. The second transaction attempts to acquire an exclusive (X) lock for its update. Because both transactions are converting to exclusive (X) locks, and they are each waiting for the other transaction to release its shared-mode lock, a deadlock occurs. To avoid this potential deadlock problem, update (U) locks are used. Only one transaction can obtain an update (U) lock to a resource at a time. If a transaction modifies a resource, the update (U) lock is converted to an exclusive (X) lock. Otherwise, the lock is converted to a shared-mode lock.*
    - *Update statement consists of 3 parts: reading data, calculating new values, writing data. We can't apply Exclusive (X) Locks for the reading part. So Update locks are not really a separate kind of lock, but rather are a hybrid of SHARED and EXCLUSIVE locks.*
    - *UPDATE locks are compatible with SHARED locks, but are not compatible with EXCLUSIVE locks or other UPDATE locks. So if two processes were searching for the same data resource, the first one to reach it would acquire an UPDATE lock, and then the second process could not get any lock and would wait for the first process to be done. Since the first process was not blocked, it could convert its UPDATE lock to an EXCLUSIVE lock, make the data modification, and finish its transaction and release its locks. Then the second process could make its change.*
  - ...
  - <https://www.geeksforgeeks.org/difference-between-shared-lock-and-exclusive-lock/>
- **optimistic**
  - *you allow the conflict to occur, but you need to detect it upon committing your transactions, and that's what Optimistic Locking does.*
  - *Optimistic Locking is a strategy where you read a record, take note of a version number (other methods to do this involve dates, timestamps or checksums/hashes) and check that the version hasn't changed before you write the record back. When you write the record back you filter the update on the version to make sure it's atomic. (i.e. hasn't been updated between when you check the version and write the record to the disk) and update the version in one hit. If the record is dirty (i.e. different version to yours) you abort the transaction and the user can re-start it.*
  - *Optimistic locking is used when you don't expect many collisions. It costs less to do a normal operation but if the collision DOES occur you would pay a higher price to resolve it as the transaction is aborted.*
  - *For optimistic locking every participant in data modification must agree in using this kind of locking. But if someone modifies the data without taking care about the version column, this will spoil the whole idea of the optimistic locking.*
- **pessimistic**
  - *You can try to avoid the conflict, and that's what Pessimistic Locking does.*
  - *Pessimistic Locking is when you lock the record for your exclusive use until you have finished with it. It has much better integrity than optimistic locking but requires you to be careful with your application design to avoid Deadlocks*
  - *The more contention, the more conflicts, and the greater the chance of aborting transactions. Rollbacks can be costly for the database system as it needs to revert all current pending changes which might involve both table rows and index records. For this reason, pessimistic locking might be more suitable when conflicts happen frequently, as it reduces the chance of rolling back transactions.*
  - *Pessimistic locking is used when a collision is anticipated. The transactions which would violate synchronization are simply blocked. To select proper locking mechanism you have to estimate the amount of reads and writes and plan accordingly.*
  - *Pessimistic locking is useful if there are a lot of updates and relatively high chances of users trying to update data at the same time. For example, if each operation can update a large number of records at a time (the bank might add interest earnings to every account at the end of each month), and two applications are running such operations at the same time, they will have conflicts. Pessimistic locking is also more appropriate in applications that contain small tables that are frequently updated. In the case of these so-called hotspots, conflicts are so probable that optimistic locking wastes effort in rolling back conflicting transactions.*
- **select for update (of colX)**
  - *takes a row-level write lock. Any other transaction that tries to UPDATE the row or SELECT ... FOR UPDATE (or FOR SHARE) it will pause until the transaction that holds the lock rolls back or commits.*
  - *The main difference between SERIALIZABLE and using SELECT FOR UPDATE is that with SERIALIZABLE everything is always locked [but this depends heavily on the DBMS implementation (Postgres for example does not do that)]. Where as with SELECT FOR UPDATE you get to choose what and when you lock.*
  - *Concurrent transactions can get the wrong value with SERIALIZABLE level, because it holds shared (read) lock for SELECT. But SELECT ... FOR UPDATE will work properly because it will hold an exclusive lock until the end of a transaction and will force other transactions to wait.*
  - *select ... for update is for row locking. This will cause other transactions that tries to do select ... for update for the already-locked rows (and each's foreign key referenced columns) to wait for the locking transaction to finish before continuing.*
  - *The FOR UPDATE say "This process may change this row(s); keep your hands off." and "If any other process is busy mucking with this row(s), I should wait."*
  - *Another way of looking at it, it is as if the following two statements are executed atomically:*
    ```
    select * from my_table where my_condition;
    update my_table set my_column = my_column where my_condition;
    ```
    *Since the rows affected by my_condition are locked, no other transaction can modify them in any way, and hence, transaction isolation level makes no difference here.*
  - *transactions guarantee locks on an UPDATE, but not a SELECT (read). so if you do a SELECT ... without FOR UPDATE at the beginning of your transaction then use the selected row(s) information later in your transaction for an update, it's possible that another transaction updated the row(s) that you queried earlier in your transaction. Hence it is necessary to use a SELECT ... FOR UPDATE within a transaction if you need to use the queried rows later.*
  - *after the SELECT [for update] statement runs, if you have another SELECT [for update?] from a different user, it won't run until your first transaction hits the COMMIT line.*
  - *If your RDBMS doesn't support FOR UPDATE then you can simulate it by performing a useless update*
- **skip locked**
  - *useful for implementing a job queue (a.k.a batch queue) so that you can skip over locks that are already locked by a concurrent transaction.*
- **no wait**
  - *useful for avoiding waiting until a concurrent transaction releases the locks that we are also interested in locking. Without NO WAIT, we either have to wait until the locks are released (at commit or release time by the transaction that currently holds the locks) or the lock acquisition times out. NO WAIT acts as a lock timeout with a value of 0.*
