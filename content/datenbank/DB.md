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


## Relationale DBMS

### Client/Server
- **MySQL**
- **PostgreSQL**
- **DB2**
  - "LUW" = Linux, Unix, Windows
  - CLI
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
  - Docker

    ```yml
    database:
      image: 'store/ibmcorp/db2_developer_c:11.1.4.4-x86_64'
      environment:
      - LICENSE=accept #agree to the terms and conditions of the Db2 software contained in this image
      - DB2INSTANCE=db2inst1 #specify the Db2 Instance name
      - DB2INST1_PASSWORD=db2pwd123 # specify the respective Db2 Instance Password
      - DBNAME=ddsdb #creates an initial database with the name provided or leave empty if no database is needed
      - BLU=false #can be set to true to enable BLU Acceleration for instance
      - ENABLE_ORACLE_COMPATIBILITY=false #can be set to true to enable Oracle Compatibility on the instance
      - UPDATEAVAIL=NO #can be set to yes if there is an existing instance and running a new container with a higher Db2 level. Will be deprecated on next release
      - TO_CREATE_SAMPLEDB=false #can be set to true to create a sample (pre-populated) database
      - REPODB=false #can be set to true to create a Data Server Manager repository database
      - IS_OSXFS=false #set IS_OSXFS=true if you are running on macOS
      - PERSISTENT_HOME=true #is true by default, only specify to false if you are running Docker for Windows
      - HADR_ENABLED=false #if set to true, Db2 HADR will be configured. The following three env variables depend on HADR_ENABLED to be true
      - ETCD_ENDPOINT= #1
      - ETCD_USERNAME= #2
      - ETCD_PASSWORD= #3
      #volumes:
      #- "/c/docker_volumes/ibm/db2_dev_c_data:/database"
      ports:
      - '50000:50000'
      - '55000:55000'
      privileged: true
    ```
- **Dolt**
  - *marries two familiar concepts, Git and MySQL. The first and only SQL database that supports clone, branch, and merge.*
  - <https://www.dolthub.com/>

### Embedded
- **H2**
  - *either embedded into a Java application or used as a database server*
  - *Embedded and server modes; disk-based or in-memory databases*
- **hsqldb**
  - Java
  - *Embedded (into Java applications) and Client-Server operating modes*
  - *In-memory tables for fastest operation. Disk based tables for large data sets*
- **SQLite**
  - *SQLite is a C-language library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine. SQLite is the most used database engine in the world.*
  - [FAQ](https://www.sqlite.org/faq.html)
    - *What datatypes does SQLite support?*
      - *SQLite uses dynamic typing. Content can be stored as INTEGER, REAL, TEXT, BLOB, or as NULL.*
    - *Can multiple applications or multiple instances of the same application access a single database file at the same time?*
      - *Multiple processes can have the same database open at the same time. Multiple processes can be doing a SELECT at the same time. But only one process can be making changes to the database at any moment in time, however. SQLite uses reader/writer locks to control access to the database.* 
  - [Appropriate Uses For SQLite](https://www.sqlite.org/whentouse.html)
    - *Situations Where A Client/Server RDBMS May Work Better*
      - *If there are many client programs sending SQL to the same database over a network*
      - *if the website is write-intensive or is so busy that it requires multiple servers*
      - *Very large datasets*
      - *High Concurrency: SQLite supports an unlimited number of simultaneous readers, but it will only allow one writer at any instant in time. For many situations, this is not a problem. Writers queue up.*
    - *Checklist For Choosing The Right Database Engine*
      - *Is the data separated from the application by a network? → choose client/server*
      - *Many concurrent writers? → choose client/server*
      - *Big data? → choose client/server*
      - *Otherwise → choose SQLite! For device-local storage with low writer concurrency and less than a terabyte of content, SQLite is almost always a better solution.*
  - <https://www.sqlite.org/index.html>    
- **DuckDB**
  - *in-process SQL OLAP Database Management System* 
  - <https://github.com/duckdb/duckdb> 
  - <https://duckdb.org/>
  - Java, Python, ...
- **Apache Derby**
  - *based on the Java, JDBC, and SQL standards.* 
  - *provides an embedded JDBC driver that lets you embed Derby in any Java-based solution.*
  - *also supports the more familiar client/server mode*
  - <https://db.apache.org/derby/>

### Cloud
- **PlanetScale**
  - *Serverless databases*
  - *Deploy, branch, and query your database directly from the UI, or download our CLI and run commands there.*
  - *fully managed database with the reliability of MySQL (our databases run on MySQL 8.0) and the scale of open source Vitess*
  - <https://planetscale.com/>


## Graphendatenbank
- **neo4j**
  - <https://neo4j.com/>
- **TerminusDB**
  - *immutable graph database that creates a graph from JSON documents*
  - *toolkit for building collaborative applications*
  - *If your application or data product needs approval workflows, implement them with TerminusDB's Git-like collaboration features.*
  - <https://terminusdb.com/>


## NOSQL
- **mongodb**
- **FerretDB**
  - *A truly Open Source MongoDB alternative*
  - <https://github.com/FerretDB/FerretDB>
- **cassandra**
  - <https://cassandra.apache.org/>
  

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
  - <https://flywaydb.org/>
  - Skripte: Java oder SQL (die Skripte sind abhängig vom DB-Vendor)
  - CLI oder embedded in (Java-)Anwendung  (beim Start der App)
  - *detects required update operations and executes them*
  - *current versions and updates stored in separate table*
- **liquibase**
  - <https://www.liquibase.org/>
  - kann - im Gegensatz zu flyway - DB-Vendor-unabhängige Migrationen (?)
- **bytebase**
  - *database schema change and version control management tool for teams*
  - *it supports 2 mainstream schema change workflow: UI based SQL review / Version control based schema migration (Database-as-Code)*
  - *Supported database engines: MySQL / Planned: PostgreSQL*


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
