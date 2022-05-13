---
tags: [Notebooks/Java]
title: Datenbank
created: '2019-02-17T20:25:41.145Z'
modified: '2021-09-21T12:23:57.799Z'
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

**Vergleich**
<br/>
*Will you do <mark>mostly complex reading and simple writing</mark>, or will you engage in complex writing? <mark>SQL</mark> really shines when reading is complex. When you join many tables, when you aggregate data in your database, when you do reporting etc.
If, however, your <mark>writing becomes complex</mark>, i.e. you have to load a complex object graph with 20 entities involved into memory, perform optimistic locking on it, modify it in many different ways and then persist it again in one go, then SQL / jOOQ will not help you. This is what <mark>Hibernate</mark> has originally been created for.*

## ORM (JPA)

### Hibernate
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


### Andere
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


## NON-JPA-Libs
- **jooq**
  - query builder
  - <https://github.com/jOOQ/jOOQ> *3.4k
  - <https://www.jooq.org/>
  - FOSS (nur open source DBs unterstützt) oder Premium
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
  - <https://github.com/jdbi/jdbi> *1.6k
  - <http://jdbi.org/>
  - <https://www.baeldung.com/jdbi>
- **jasync-sql**
  - *Async DataBase Driver for MySQL and PostgreSQL*
  - <https://github.com/jasync-sql/jasync-sql>
- **Quick SQL test data**
  - *aims to ease the generation of datasets to test SQL queries. It produces INSERT statements taking account of integrity constraints.*
  - *This library can be helpful in the two following situations: Create a dataset before starting the writing of an SQL query. Test an existing SQL query.*
  - ```java
    QuickSqlTestData quickSqlTestData = QuickSqlTestData.buildFrom(dataSource);
    DatasetRow datasetRow = DatasetRow.ofTable("Player").addColumnValue("lastName","Pogba");
    List<String> insertStatements = quickSqlTestData.generateInsertListFor(datasetRow);
    ```
  - <https://github.com/quick-perf/quick-sql-test-data>


## In-memory
- → Datenbank
- <https://www.baeldung.com/java-in-memory-databases>
- <https://github.com/bwaldvogel/mongo-java-server>


## Diverse
- **seata**
  - <https://github.com/seata/seata>
  - ehemals alibaba/fescar
- **velvetdb**
  - <https://github.com/zakgof/velvetdb>
  - embedded oder cloud
  - *high-level API for NoSQL storage perfectly fitting for small websites, desktop and mobile applications*
- <u>connection pool</u>
  - **hikari**
    - <https://github.com/brettwooldridge/HikariCP>
  - **tomcat jdbc**
    - <https://www.baeldung.com/spring-boot-tomcat-connection-pool>
- **datasource-proxy**
  - *intercept JDBC interactions and allows user to perform own logic before/after query or method executions*
  - *Pre-defined listeners support query logging, slow query detection, query execution statistics, interaction tracing, etc.*
  - <http://ttddyy.github.io/datasource-proxy/docs/current/user-guide/>
- **R2DBC**
  - <https://r2dbc.io/>
  - *R2DBC is an endeavor to bring a reactive programming API to relational data stores.*
  - 9.3.18: Support für postgres, h2, mssql
- **fastnate**
  - *tool on top of JPA to generate SQL statements without having access to a database. Its main usecase is to import a bunch of initial data.*
  - <https://github.com/liefke/org.fastnate/wiki>
  - z.B. Nutzung, um JPA-Entities abzuspeichern (java code) und den generierten SQL-Code (DB-Dialekt-spezidisch) zu erhalten:
    <https://medium.com/swlh/code-first-database-design-and-development-using-jpa-hibernate-flway-fastnate-and-spring-boot-3ede35b403a6>


## Dies & das
- **mysql jdbc driver**
  - Zeitzone festlegen (für date columns) `jdbc:mysql:...?serverTimezone=Europe/Berlin`
