---
tags: [Notebooks/Datenbank]
title: DB
created: '2019-06-02T19:18:35.022Z'
modified: '2021-08-15T13:10:57.455Z'
parent: Datenbank
---

# DB
- <https://random-dev.medium.com/databases-in-5-min-bfd3b9bef86>
- <https://rakyll.medium.com/things-i-wished-more-developers-knew-about-databases-2d0178464f78>

## IDs
- auto generated
  - *doesn't go well with distributed dbs, sharding*
- UUID
- Hash-ID
  - <https://hashids.org/>
- ULID
  - Universally Unique Lexicographically Sortable Identifier
  - <https://github.com/ulid/spec>


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


## Migration
- Um Änderungen an DBs in mehreren Umgebungen vorzunehmen ("schema migration"). Oft müssen dann auch bestehende Daten angepasst werden ("data migration").
- Test z.B. mit Lib "testcontainers"
- **flyway**
  - Skripte: Java oder SQL (die Skripte sind abhängig vom DB-Vendor)
  - CLI oder embedded in (Java-)Anwendung  (beim Start der App)
  - *detects required update operations and executes them*
  - *current versions and updates stored in separate table*
  - *Supported databases: Oracle, SQL Server, DB2, MySQL, Aurora MySQL, MariaDB, Percona XtraDB Cluster, PostgreSQL, Aurora PostgreSQL, Redshift, CockroachDB, SAP HANA, Sybase ASE, Informix, H2, HSQLDB, Derby, SQLite, Firebird*
  - *Supported build tools: Maven and Gradle*
  - <https://github.com/flyway/flyway>
  - <https://flywaydb.org/>
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


## Change data capture
- Debezium
  - <https://github.com/debezium/debezium/> *1800
  - <https://debezium.io/>
  - *Monitoring databases and being notified when data changes. data streaming platform for change data capture (CDC). configure Debezium to monitor your databases, and then your applications consume events for each row-level change made to the database. reusing Kafka and Kafka Connect.*
  - *Common use cases: Cache invalidation, Simplifying monolithic applications, Data integration*


## Diverses
- Sharding
  - <https://en.wikipedia.org/wiki/Shard_(database_architecture)>
- ACID
  - <https://en.wikipedia.org/wiki/ACID>
