---
title: Datenbank
parent: Java
---

# Datenbank
<https://www.marcobehler.com/guides/java-databases-jdbc-hibernate-spring-data>

## JDBC vs JPA
**JDBC**
  - Standard für Datenbankzugriff
  - low-level-Abstraktion, pures SQL
  - "schneller als JPA, wenn man weiß, was man tut"
  - Klassen: Connection, Statement, PreparedStatement, ResultSet
  
**JPA**
- Spezifikation für ORM
- high-level-Abstraktion, "versteckt" SQL
- besonders geeignet für komplexe Queries
- Mapping zw. Klasse und Tabelle über Annotationen oder XML
- vereinfacht Caching
- einige Annotationen:
  - @Access: ob Getter/Setter oder Fields für Zugriff verwendet werden sollen
  - @EntityListeners: @PrePersist etc in separate Klasse auslagern
  - @UniqueConstraint: auf @Table-Ebene (Kombinationen von Spalten) als unique festlegen
- *JPA is not just a SQL generator. It is a write-through cache - a layer between your application and your database with a short-lived session storage. In practice, this means that when you fetch an entity and update it, then even saving it explicitly does not immediately execute SQL statements. Instead, JPA accumulates changes and "flushes" them in one optimized batch when the transaction is commited. It can do this because your entities are "managed", meaning that they are proxies with field-based change tracking. Sometimes you want your SQL statements to be executed immediately, for example, if you mix native and JPA queries. In this case you can call flush immediately and this executes SQL statements for all accumulated changes so far (basically, syncs local and database states). Note that this does not commit the transaction and it still can be rolled back.* (<https://www.reddit.com/r/java/comments/uommj4/flushing_in_jpa/i8fdual/>)
- Tipps
  - <https://java-persistence-performance.blogspot.com/2011/06/how-to-improve-jpa-performance-by-1825.html>
  - mit lombok
    - <https://mdeinum.github.io/2019-02-13-Lombok-Data-Ojects-Arent-Entities>
    - <https://www.reddit.com/r/java/comments/hlzvy5/lombok_hibernate_how_to_avoid_common_pitfalls>
    - <https://www.jpa-buddy.com/blog/lombok-and-jpa-what-may-go-wrong>
  - <https://vladmihalcea.com/14-high-performance-java-persistence-tips>
  - @ManyToMany sollten aus Performance-Gründen immer mit Set und nicht mit List kombiniert werden
  - mit `@Basic(fetch=FetchType.LAZY) String str` können auch einzelne Spalten lazy geladen werden. Allerdings erfordert dies Bytecodeinstumentation (z.B. hibernate-enhance-maven-plugin)
  - [The Ultimate Guide on Client-Generated IDs in JPA Entities](https://www.jpa-buddy.com/blog/the-ultimate-guide-on-client/)

**Vergleich**
<br/>
*Will you do <mark>mostly complex reading and simple writing</mark>, or will you engage in complex writing? <mark>SQL</mark> really shines when reading is complex. When you join many tables, when you aggregate data in your database, when you do reporting etc.
If, however, your <mark>writing becomes complex</mark>, i.e. you have to load a complex object graph with 20 entities involved into memory, perform optimistic locking on it, modify it in many different ways and then persist it again in one go, then SQL / jOOQ will not help you. This is what <mark>Hibernate</mark> has originally been created for.*


## JDBC
- *The default behavior of a Connection is auto-commit. To clarify, what this means is that every single statement is treated as a transaction and is automatically committed right after execution.*


## JPA

### Transactions, Query Hints & Locking
- -> Datenbank/DB/Transactions/Locking
- *By default JPA impose Read committed isolation level if you don't specify any locking (same behaviour as using LockModeType.NONE).*

#### Locking
- **optimistic**
  - *Using optimistic locking in JPA rises isolation level to Repetable reads.*
  - *JPA achieves Repetable reads in the simplest way possible: by preventing Non-Repetable read phenomenon. JPA is not sophisticated enough to keep snapshots of your reads. It simply prevents second read from happening by rising an exception (if the data has changed from the first read).*
  - *fully controlled by JPA, completely independent of underlying DB engine*
  - *The downside of optimistic locking is that a rollback will be triggered by the data access framework upon catching an OptimisticLockException, therefore losing all the work we've done previously by the currently executing transaction.*
  - @javax.persistence.Version
  - <https://www.baeldung.com/jpa-optimistic-locking>
- **pessimistic**
  - *uses locking mechanism provided by underlying database to lock existing records in tables. JPA needs to know how to trigger these locks and some databases do not support them or only partially.*
  - <https://www.baeldung.com/jpa-pessimistic-locking>
- <u>javax.persistence.LockModeType</u>
  - **NONE**
    - *this is the default if entities don't provide a version field. It means that no locking is enabled conflicts will be resolved on best effort basis and will not be detected. This is the only lock mode allowed outside of a transaction*
  - **OPTIMISTIC** (alias READ)
    - *If entities specify a version field, this is the default.*
    - *it increments the version while committing*
  - **OPTIMISTIC_FORCE_INCREMENT** (alias WRITE)
    - *it increments the version column even though the entity is not updated.*
  - **PESSIMISTIC_READ**
    - *For repeatable reads, used to ensure that data isn't updated between reads. It is a shared lock meaning different processes can perform read operations (no write operations are permitted).* 
    - *issues a select for update nowait (if no hint timeout specified)*
    - *it should not block reading the entity. It also allows other transactions to lock using LockModeType.PESSIMISTIC_READ.*
  - **PESSIMISTIC_WRITE**
    - *An exclusive lock which forces serialization of updates. Where optimistic locking only saved state, here it is locked to prevent transaction failure/deadlock in cases where this would happen with concurrent operations.* 
    - *LockModeType.PESSIMISTIC_WRITE translates to using a READ_COMMITTED isolation level with a SELECT .. FOR UPDATE in SQL*
    - *also issues a select for update nowait (if no hint timeout specified).*
    - *this is a stronger version of LockModeType.PESSIMISTIC_READ. When WRITE lock is in place, JPA with the help of the database will prevent any other transaction to read the entity, not only to write as with READ lock.*
  - **PESSIMISTIC_FORCE_INCREMENT**
    - *Analogous to its optimistic counterpart, a pessimistic write that updates the object's version. Throws an exception for non-versioned objects.*
    - *this does select for update nowait (if no hint timeout specified) and also increments the version number.*
    - *it is an option where you need to combine PESSIMISTIC and OPTIMISTIC mechanisms. Using plain PESSIMISTIC_WRITE would fail in following scenario:*
      ```
      transaction A uses optimistic locking and reads entity E
      transaction B acquires WRITE lock on entity E
      transaction B commits and releases lock of E
      transaction A updates E and commits
      ```
  - <https://docs.oracle.com/javaee/7/api/javax/persistence/LockModeType.html>
- <https://dzone.com/articles/concurrency-and-locking-with-jpa-everything-you-ne>

#### Query Hints
- javax.persistence.lock.timeout
- javax.persistence.query.timeout


### ORMs

#### Hibernate
- Buch: [Hibernate Notes For Professionals](https://goalkicker.com/HibernateBook/HibernateNotesForProfessionals.pdf)
- **Tipps**
    - mit [ColumnTransformer](https://docs.jboss.org/hibernate/orm/current/javadocs/org/hibernate/annotations/ColumnTransformer.html) können bei read und write SQL-Funktionen auf Felder aufgerufen werden
    - die generierten SQLs können mit der Klasse StatementInspector [verändert werden](https://vladmihalcea.com/hibernate-statementinspector/)
      - z. B. können so Logs & SQL-kommentare zum Debuggen eingefügt werden (→ use_sql_comments)
    - Projections
      - <https://thorben-janssen.com/dto-projections>
- <u>Tools</u>
  - <https://hibernate.org/orm/tooling>
  - <https://github.com/vladmihalcea/hibernate-types>
  - → Maven/Plugins/hibernate-enhance
  - **envers**
    - trackt Änderungen an @Entitys in separaten Tables
    - *works both with Hibernate and JPA. In fact, you can use Envers anywhere Hibernate works whether that is standalone, inside WildFly or JBoss AS, Spring, Grails, etc.*
    - *aims to provide an easy auditing / versioning solution for entity classes*
    - <https://hibernate.org/orm/envers>
  - **search**
    - *Full-text search for entities*
    - *automatically extracts data from Hibernate ORM entities to push it to local Apache Lucene indexes or remote Elasticsearch/OpenSearch indexes.*
    - <https://hibernate.org/search>
- **dirty checking & bytecode enhancement**
  - *Hibernate is able to automatically save an attached entity instance on flush if you’ve made any changes to it. By default, it does to by keeping the initial state of the object in memory and comparing it to the actual state before flushing. However, keeping the whole initial state of the object in memory is costly, and doing a field-by-field comparison before flushing wastes time. So there’s another mechanism in Hibernate for dirty checking, that takes advantage of Hibernate’s bytecode enhancement.*
  - <https://medium.com/@forketyfork/hibernate-extended-bytecode-enhancement-ae73962c9bf4>
- **Logging**
  - `show_sql`, `format_sql` und `use_sql_comments` (https://mkyong.com/hibernate/hibernate-display-generated-sql-to-console-show_sql-format_sql-and-use_sql_comments/)
  - ```xml
    <!-- zeigt die SQL-Param-Bindings -->
    <logger name="org.hibernate.type">
        <level value="trace"/>
    </logger>
    <!-- Verwendung zusammen mit hibernate.generate_statistics=true -->
    <logger name="org.hibernate.stat">
        <level value="debug"/>
    </logger>
    <!--
        ignorierbare Fehlermeldungen wenn level="debug" & @Transactional(readOnly=true)
        https://confluence.atlassian.com/confkb/connection-readonly-mode-is-not-enforceable-after-the-connection-has-been-established-error-messages-182683282.html
    -->
    <logger name="org.hibernate.engine.jdbc.spi.SqlExceptionHelper">
        <level value="info"/>
    </logger>
    ```
  - slow-query-log: <https://thorben-janssen.com/hibernate-slow-query-log>


#### Andere ORMs
- **objectdb**
  - <https://www.objectdb.com>
  - *ObjectDB is about 10 times faster than other JPA/DBMS solutions*
  - keine reine API, sondern DBMS (client/server oder embedded)
- **openjpa**
- **eclipselink**


### Tools
- **jpa buddy**
  - *plugin for IntelliJ IDEA intended to simplify and accelerate everything related to JPA and surrounding mainstream technology*
  - *Create JPA entities and Spring Data repositories fast. Easily generate migration scripts for Liquibase and Flyway.*
  - <https://www.jpa-buddy.com/>
- **JaVers**
  - *library for auditing changes in your data*
  - *easy to use in applications based on the Spring Framework*
  - <https://github.com/javers/javers>
- **JPA Streamer**
  - *library for expressing JPA/Hibernate/Spring queries using standard Java streams*
  - <https://jpastreamer.org/>
- **P6Spy**
  - *framework that enables database data to be seamlessly intercepted and logged with no code changes to the application*
  - <https://github.com/p6spy/p6spy>


## Non-JPA-Libs, Query-Builder
- **jooq**
  - query builder
  - <https://github.com/jOOQ/jOOQ> *3.4k
  - <https://www.jooq.org/>
  - FOSS (nur open source DBs unterstützt) oder Premium
  - R2dbc: ja
- **mybatis**
  - SQL-Mapper
  - <https://github.com/mybatis/mybatis-3> *12.1k
- **javalite activejdbc**
  - <https://github.com/javalite/javalite> *700
  - <http://javalite.io/activejdbc>
- **apache cayenne**
  - <https://cayenne.apache.org/>
  - <https://github.com/apache/cayenne>
- **querydsl**
  - <https://github.com/querydsl/querydsl/> *3.8k
  - *type-safe SQL-like queries for multiple backends including JPA, MongoDB and SQL in Java.*
- **persism**
  - *A zero ceremony ORM for Java*
  - *Derby, Firebird, H2, HSQLDB, Informix, MSAccess, MSSQL, MySQL/MariaDB, Oracle (12+), PostgreSQL, SQLite.*
  - <https://github.com/sproket/Persism> *10
- **ebean**
  - <https://github.com/ebean-orm/ebean> *1200
- **doma**
  - *DAO oriented database mapping framework*
  - *generates source code at compile time using annotation processing.*
  - *Provides type-safe Criteria API*
  - <https://github.com/domaframework/doma> *311
- **jdbi**
  - *uses lambda expressions and reflection to provide a friendlier, higher level interface than JDBC to access the database*
  - *has an optional SQL Object mapping module*
  - R2dbc: Nein
  - <https://github.com/jdbi/jdbi> *1.6k
  - <http://jdbi.org/>
  - <https://www.baeldung.com/jdbi>
- **sql2o**
  - *makes it easy to convert the result of your sql-statements into objects*
  - *A key feature of sql2o is performance. Execute 1000 SELECT statements against a DB and map the data returned to a POJO.*

    Method                                                              | Duration               |
    ------------------------------------------------------------------- | ---------------------- |
    Hand coded <code>ResultSet</code>                                   | 60ms                   |
    Sql2o                                                               | 75ms (25% slower)      |
    [Apache DbUtils](http://commons.apache.org/proper/commons-dbutils/) | 98ms (63% slower)      |
    [JDBI](http://jdbi.org/)                                            | 197ms (228% slower)    |
    [MyBatis](http://mybatis.github.io/mybatis-3/)                      | 293ms (388% slower)    |
    [jOOQ](http://www.jooq.org)                                         | 447ms (645% slower)    |
    [Hibernate](http://hibernate.org/)                                  | 494ms (723% slower)    |
    [Spring JdbcTemplate](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/jdbc.html) | 636ms (960% slower) |

  - <https://github.com/aaberg/sql2o>
- **FluentJdbc**
  - *convenient native SQL querying*
  - *Blends well with Java 8 / functional code*
  - *no dependencies* 
  - <https://github.com/zsoltherpai/fluent-jdbc> 
- **TSID Creator**
  - *A Java library for generating Time-Sorted Unique Identifiers (TSID). It brings together ideas from Twitter's Snowflake and ULID Spec.* 
  - <https://github.com/f4b6a3/tsid-creator>
- **FriendlyID**
  - *converts a given UUID (with 36 characters) to a URL-friendly ID (a "FriendlyID") which is based on Base62 (with a maximum of 22 characters)*
  - <https://github.com/Devskiller/friendly-id>


## Test
- **Quick SQL test data**
  - *aims to ease the generation of datasets to test SQL queries. It produces INSERT statements taking account of integrity constraints.*
  - *This library can be helpful in the two following situations: Create a dataset before starting the writing of an SQL query. Test an existing SQL query.*
  - ```java
    QuickSqlTestData quickSqlTestData = QuickSqlTestData.buildFrom(dataSource);
    DatasetRow datasetRow = DatasetRow.ofTable("Player").addColumnValue("lastName","Pogba");
    List<String> insertStatements = quickSqlTestData.generateInsertListFor(datasetRow);
    ```
  - <https://github.com/quick-perf/quick-sql-test-data>
- **Testcontainers** -> Java/Test


## In-memory
- → Datenbank
- <https://www.baeldung.com/java-in-memory-databases>
- <https://github.com/bwaldvogel/mongo-java-server>


## Migration
- -> Datenbank/DB/Migration


## Diverse
- **velvetdb**
  - <https://github.com/zakgof/velvetdb>
  - embedded oder cloud
  - *high-level API for NoSQL storage perfectly fitting for small websites, desktop and mobile applications*
- <u>connection pool</u>
  - **hikari**
    - <https://github.com/brettwooldridge/HikariCP>
  - **tomcat jdbc**
    - <https://www.baeldung.com/spring-boot-tomcat-connection-pool>
  - **MiniConnectionPoolManager**
    - *A lightweight standalone Java JDBC connection pool manager* 
    - <https://github.com/chdh/miniconnectionpoolmanager>
  - **FlexyPool**
    - <https://www.baeldung.com/spring-flexypool-guide>
      - *connection pool management tool*
      - *acts as a proxy to major connection pools such as Hikari, C3P0, DBCP2, Tomcat, and Vibur*  
      - *provides metrics and failover strategies to help resize a given pool on demand*

- **datasource-proxy**
  - *intercept JDBC interactions and allows user to perform own logic before/after query or method executions*
  - *Pre-defined listeners support query logging, slow query detection, query execution statistics, interaction tracing, etc.*
  - <http://ttddyy.github.io/datasource-proxy/docs/current/user-guide/>
- **fastnate**
  - *tool on top of JPA to generate SQL statements without having access to a database. Its main usecase is to import a bunch of initial data.*
  - <https://github.com/liefke/org.fastnate/wiki>
  - z.B. Nutzung, um JPA-Entities abzuspeichern (java code) und den generierten SQL-Code (DB-Dialekt-spezidisch) zu erhalten:
    <https://medium.com/swlh/code-first-database-design-and-development-using-jpa-hibernate-flway-fastnate-and-spring-boot-3ede35b403a6>


## Dies & das
- **mysql jdbc driver**
  - Zeitzone festlegen (für date columns) `jdbc:mysql:...?serverTimezone=Europe/Berlin`


## R2dbc
- <https://r2dbc.io/>
- *R2DBC is an endeavor to bring a reactive programming API to relational data stores.*
- Connection Pool
  - <https://github.com/r2dbc/r2dbc-pool>
- Proxy
  - <https://github.com/r2dbc/r2dbc-proxy> 
- H2
  - *Because various parts of H2 are blocking, like file and network access, the only non-blocking assurances are in the layers above H2. Nevertheless, r2dbc-h2 is a great way to warm up to the usage of R2DBC with a small footprint.* 
  - <https://github.com/r2dbc/r2dbc-h2>
- Postgres
  - <https://github.com/pgjdbc/r2dbc-postgresql>
- MSSQL
- MySQL
  - <https://github.com/mirromutth/r2dbc-mysql>

### Clients
- <https://r2dbc.io/clients/> 
- **vertx-sql-client**
  - Support: Postgres, MySQL, MSSQL, DB2, Oracle 
  - <https://github.com/eclipse-vertx/vertx-sql-client>
- **jasync-sql**
  - *Async DataBase Driver for MySQL and PostgreSQL*
  - <https://github.com/jasync-sql/jasync-sql>

### Migration
- Flyway: Nein, <https://github.com/flyway/flyway/issues/2502>
- Liquibase: Nein, <https://github.com/liquibase/liquibase/issues/1470>
- r2dbc-migrate
  - *Supported databases: PostgreSQL, Microsoft SQL Server, MySQL, H2, MariaDB. It also supports user-provided dialect* 
  - <https://github.com/nkonev/r2dbc-migrate> *77
