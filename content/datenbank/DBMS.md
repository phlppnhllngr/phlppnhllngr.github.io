---
title: DBMS
parent: Datenbank
---

# DBMS

## Relationale Client/Server
- **MySQL**
- **PostgreSQL**
  - -> Message Broker / PG 
  - [HN: Dbdev – A database package manager for PostgreSQL trusted language extensions](https://news.ycombinator.com/item?id=35570758)
  - <https://github.com/Olshansk/postgres_for_everything>
  - Sammlung Extensions etc.: <https://gist.github.com/cpursley/c8fb81fe8a7e5df038158bdfe0f06dbb>
  - VSC-Support: <https://news.ycombinator.com/item?id=44073588>
  - CloudNativePG
    - *operator designed to manage PostgreSQL workloads on any supported Kubernetes cluster running in private, public, hybrid, or multi-cloud environments*
    - *leverages Kubernetes by extending its controller and by defining, in a programmatic way, all the actions that a good DBA would normally do when managing a highly available PostgreSQL database cluster* 
    - <https://github.com/cloudnative-pg/cloudnative-pg>
  - readyset
    - *a MySQL and Postgres wire-compatible caching layer that sits in front of existing databases to speed up queries and horizontally scale read throughput. Under the hood, ReadySet caches the results of cached select statements and incrementally updates these results over time as the underlying data changes.* 
    - <https://github.com/readysettech/readyset>
  - pgmock
    - *In-memory Postgres for unit/E2E tests*
    - *runs entirely within WebAssembly on both Node.js and the browser.* 
    - <https://github.com/stackframe-projects/pgmock>
  - pg-mem
    - *in memory postgres DB instance for your unit tests*
    - Nodejs & Browser 
    - <https://github.com/oguimbal/pg-mem>
  - pglite
    - *Lightweight Postgres packaged as WASM into a TypeScript library for the browser, Node.js, Bun and Deno*
    - <https://github.com/electric-sql/pglite>
  - pgjwt
    - *implementation of JWT* 
    - <https://github.com/michelp/pgjwt>
  - electric
    - *Real-time sync for Postgres*
    - *syncs data out of Postgres into ... anything you like. The core sync protocol is based on a low-level HTTP API*
    - <https://github.com/electric-sql/electric>
  - pg_graphql
    - <https://github.com/supabase/pg_graphql>
  - pg_mooncake
    - *Real-time analytics on Postgres tables* 
    - <https://github.com/Mooncake-Labs/pg_mooncake>
  - pg_cron
    - *Run periodic jobs in PostgreSQL*
    - *allows you to schedule PostgreSQL commands directly from the database* 
    - <https://github.com/citusdata/pg_cron>
  - pgroll
    - *zero-downtime migrations made easy*
    - HN: <https://news.ycombinator.com/item?id=37752366> 
    - <https://github.com/xataio/pgroll>
  - pg_timeseries
    - <https://news.ycombinator.com/item?id=40417347>
  - Neosync
    - *Open-Source Data Anonymization for Postgres and MySQL* 
    - <https://news.ycombinator.com/item?id=40443927>
  - pg_datanymizer
    - *Powerful database anonymizer with flexible rules* 
    - <https://github.com/datanymizer/datanymizer>
  - greenmask
    - <https://github.com/GreenmaskIO/greenmask>
    - *database anonymization and synthetic data generation tool*
- **DB2** -> Db2


## Relationale Embedded
- **H2**
  - *either embedded into a Java application or used as a database server*
  - *Embedded and server modes; disk-based or in-memory databases*
  - <u>Connection modes</u>
    - <http://h2database.com/html/features.html#connection_modes> 
    - *Embedded mode*
      - *local connections using JDBC* 
      - *an application opens a database from within the same JVM using JDBC. This is the fastest and easiest connection mode. The disadvantage is that a database may only be open in one virtual machine (and class loader) at any time. As in all modes, both persistent and in-memory databases are supported. There is no limit on the number of database open concurrently, or on the number of open connections.*
    - *Server mode*
      - *remote connections using JDBC or ODBC over TCP/IP*
      - *When using the server mode (sometimes called remote mode or client/server mode), an application opens a database remotely using the JDBC or ODBC API. A server needs to be started within the same or another virtual machine, or on another computer. Many applications can connect to the same database at the same time, by connecting to this server. Internally, the server process opens the database(s) in embedded mode.*
    - *Mixed mode*
      - *local and remote connections at the same time*
      - *The first application that connects to a database does that in embedded mode, but also starts a server so that other applications (running in different processes or virtual machines) can concurrently access the same data. The local connections are as fast as if the database is used in just the embedded mode, while the remote connections are a bit slower.*
        - Automatic mixed mode
          - <http://h2database.com/html/features.html#auto_mixed_mode>
          - *Multiple processes can access the same database without having to start the server manually. To do that, append `;AUTO_SERVER=TRUE` to the database URL. You can use the same database URL independent of whether the database is already open or not. This feature doesn't work with in-memory databases.*
          - *Internally, when using this mode, the first connection to the database is made in embedded mode, and additionally a server is started internally (as a daemon thread).*
          - *the first connection to the database uses the embedded mode, which is faster than the server mode. Therefore the main application should open the database first if possible.*
  - Shell
    ```
    java -cp ~/.m2/repository/com/h2database/h2/1.4.200/h2-1.4.200.jar org.h2.tools.Shell
    ```
    Transaction:
    ```
    autocommit false
    prepare commit test_ta;
    create table foo (id int identity primary key, value varchar(255));
    insert into foo (value) values ('A'), ('B');
    commit transaction test_ta; / rollback transaction test_ta;
    ```
  - [Settings](http://h2database.com/html/features.html?highlight=AUTO_SERVER&search=AUTO_SERVER#database_url)
    - Encryption
      - <http://h2database.com/html/features.html#file_encryption>
    - Compatibility modes
      - *For certain features, this database can emulate the behavior of specific databases. However, only a small subset of the differences between databases are implemented in this way.* 
      - <http://h2database.com/html/features.html#compatibility>
  - [FAQ](http://h2database.com/html/faq.html)
    - *Is it reliable?*
      - *When using one of the following features for production, please ensure your use case is well tested (if possible with automated test cases). The areas that are not well tested are: (...) AUTO_SERVER and AUTO_RECONNECT (...)*  
  - vs SQLite
    - *More data types than SQLite.*
    - *H2 is encrypted. It is multi-user, password-protected database. This feature is not available in SQLite.*
    - *Has inbuilt database management console*
  - <http://www.h2database.com/html/features.html>
  - <https://www.baeldung.com/h2-embedded-db-data-storage> 
- **HSQLDB**
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
  - Fiddle: <https://sqlite.org/fiddle/>  
- **libSQL**
  - *fork of SQLite that is both Open Source, and Open Contributions* 
  - <https://github.com/libsql/libsql> 
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


## Cloud, Serverless
- **PlanetScale**
  - *Serverless databases*
  - *Deploy, branch, and query your database directly from the UI, or download our CLI and run commands there.*
  - *fully managed database with the reliability of MySQL (our databases run on MySQL 8.0) and the scale of open source Vitess*
  - <https://planetscale.com/>
- **Neon**
- **xata**

## Graphendatenbank
- **neo4j**
  - <https://neo4j.com/>
- **Memgraph**
  - Drop-in-replacement für Neo4j
  - <https://github.com/memgraph/memgraph> 
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


## NextGen
- **SurrealDB**
  - <https://github.com/surrealdb/surrealdb> <img loading="lazy" src="https://img.shields.io/github/stars/surrealdb/surrealdb?style=flat-square"/> 
  - [YT_: Fireship - SurrealDB in 100 Seconds](https://www.youtube.com/watch?v=C7WFwgDRStM)
- **Dolt**
  - *Git for data*
  - *SQL database that you can fork, clone, branch, merge, push and pull just like a Git repository*
  - *Connect to Dolt just like any MySQL database to run queries or update the data using SQL commands.* 
  - <https://github.com/dolthub/dolt> <img loading="lazy" src="https://img.shields.io/github/stars/dolthub/dolt?style=flat-square"/>
  - <https://www.dolthub.com/blog/2022-07-11-dolt-case-studies/>
  - DoltgreSQL
    - *Version Controlled PostgreSQL*
    - <https://github.com/dolthub/doltgresql>
- **8base**
  - mit GraphQL + Lowcode-UI-Builder
- **fauna**
- **Meilisearch**
  - full text search
  - Mailisearch Instant für Frontend-Integration
- **KeyDB**
  - In-memory cache 
