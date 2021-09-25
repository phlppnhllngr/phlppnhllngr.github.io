---
tags: [Notebooks/Spring]
title: Datenbank
created: '2019-02-05T09:27:47.602Z'
modified: '2021-09-13T13:50:32.985Z'
parent: Spring
---

# Datenbank

## Spring JDBC
- *Spring abstractions over the plain JDBC*
- Spring Boot Starter: `spring-boot-starter-jdbc`
- Klassen: @Transactional, DataSource, JdbcTemplate, ResultSet
- JDBC & DATA-JDBC: [https://4comprehension.com/lightweight-jpa-hibernate-alternatives]()


## Spring Data JDBC
- [https://spring.io/projects/spring-data-jdbc]()
- [https://spring.io/blog/2018/09/24/spring-data-jdbc-references-and-aggregates]()
- *provides the Spring Data abstraction over spring-jdbc*
- *Spring Data JDBC aims at being conceptually easy. In order to achieve this it does NOT offer caching, lazy loading, write behind or many other features of JPA. This makes Spring Data JDBC a simple, limited, opinionated ORM.*
- kann z.B. zusammen mit jooq benutzt werden
- Spring Boot Starter: `spring-boot-starter-data-jdbc`
- Klassen: CrudRepository, JdbcAggregateTemplate


## Spring Data JPA
- [https://www.marcobehler.com/guides/spring-transaction-management-unconventional-guide]()
- *keep in mind is that @Transactional methods use up a DB connection from the connection pool. If your method does HTTP calls or heavy computation while within a transaction, you might run out of DB connections. The scope of a transaction should be as narrow as possible.*
- *@Transactional also works on other things, for instance with our AMQP listener, it puts messages back in the queue if processing fails.*
- [https://blog.ippon.tech/boost-the-performance-of-your-spring-data-jpa-application/]()
- [https://thorben-janssen.com/hibernate-features-with-spring-data-jpa/]()
- Tools
  - jplusone
    - *automatic detection and asserting "N+1 SELECT problem" occurences in JPA based Spring Boot Java applications and finding origin of JPA issued SQL statements in general*
    - [https://github.com/adgadev/jplusone]()
  - data-envers
    - *allow access to entity revisions managed by Hibernate Envers*
    - [https://github.com/spring-projects/spring-data-envers]()
    - Bsp-Repo: [https://github.com/rashidi/spring-data-envers-audit-entity]()
  - spring-data-jpa-entity-graph
    - [https://github.com/Cosium/spring-data-jpa-entity-graph]()
  - spring-data-jpa-temporal
    - *an extension of spring-data-jpa that makes it simple to keep an audit of your data in the same table as your main data itself*
    - [https://github.com/ClaudioConsolmagno/spring-data-jpa-temporal]() *1
- Test
  - @DataJpaTest (Spring Boot)
    - *used to test JPA repositories*
    - *By default, tests annotated with @DataJpaTest use an embedded in-memory database*
    - *by default, each test method runs in its own transaction, which is rolled back after the method has executed.*
    - [https://reflectoring.io/spring-boot-data-jpa-test/]()
  - @AutoConfigureTestDatabase
    - *can be applied to a test class to configure a test database to use instead of the application-defined or auto-configured DataSource*
  - spring-test-dbunit
    - *Integration between the Spring testing framework and DBUnit*
    - [https://github.com/springtestdbunit/spring-test-dbunit]()


## Vergleich
- JDBC ohne Spring Data
  - *You get 100% fine-grained control over what is happening*
  - *You probably want to use some library in order to cut down on boilerplate code (jooq, mybatis, Spring JdbcTemplate)*
- JDBC mit Spring Data
  - *You get the benefits of Spring Data, combined with those of JDBC*
- Hibernate (oder anderes JPA-ORM) mit Spring Data
  - *JPA does a lot of things over JDBC: Caching (1st, 2nd level, and query cache), Automated creation of instances from queries, Navigation between entities, Lazy loading*
  - *With all this stuff happening it can be difficult understanding what is happening and why*


## Migration
→ Datenbank/Migration
Besser, die DB-Migration von der Anwendung zu trennen?
- Flyway
  - [https://reflectoring.io/database-migration-spring-boot-flyway/]()
  - [https://reflectoring.io/spring-boot-flyway-testcontainers/]()
  - mit Hibernate
    - [https://rieckpil.de/howto-best-practices-for-flyway-and-hibernate-with-spring-boot/]()
      - `ddl-auto` auf `none` oder `validate` stellen


## Auditing
- [https://www.baeldung.com/database-auditing-jpa]()
- [https://attacomsian.com/blog/spring-data-jpa-auditing]()
- [https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#auditing]()
  - *keep track of who created or changed an entity and when the change happened* (envers wohl mächtiger weil es auch die Änderungen persistiert)


## JOOQ
- [https://blog.jooq.org/tag/spring-boot/]()
- [https://www.baeldung.com/jooq-with-spring]()
- [https://www.baeldung.com/spring-boot-support-for-jooq]()
