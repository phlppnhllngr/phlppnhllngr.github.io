---
title: Micronaut
parent: Java
---

# Micronaut
- <http://micronaut.io/>
- <https://micronaut.io/launch> (wie Spring initializer)
- [Introduction to Micronaut • Graeme Rocher • GOTO 2019](https://www.youtube.com/watch?v=RtjSqRZ_md4)
- <https://github.com/micronaut-projects/micronaut-comparisons>

## Projects
- <https://github.com/micronaut-projects/>
- **core**
  - <https://github.com/micronaut-projects/micronaut-core> *2600
- <u>data</u>
  - *database access toolkit that uses Ahead of Time (AoT) compilation to pre-compute queries for repository interfaces that are then executed by a thin, lightweight runtime layer.*
  - *provides a general API for translating a compile time Query model into a query at compilation time and provides runtime support for the following backends: JPA (Hibernate), SQL (JDBC, R2DBC), MongoDB*
  - <https://micronaut-projects.github.io/micronaut-data/latest/guide/>
  - <https://github.com/micronaut-projects/micronaut-data>
  - **data-jpa**
    - <https://micronaut-projects.github.io/micronaut-data/latest/guide/#introduction> 
  - **data-jdbc**
    - *Micronaut Data JDBC / R2DBC supports all of the features of Micronaut Data for JPA including dynamic finders, pagination, projections, Data Transfer Objects (DTO), Batch Updates, Optimistic locking and so on. However, Micronaut Data JDBC / R2DBC is not a Object Relational Mapping (ORM) implementation and does not and will not include any of the following concepts: Lazy Loading or Proxying of Associations, Dirty Checking, Persistence Contexts / Sessions, First Level Caching and Entity Proxies. Micronaut Data JDBC / R2DBC is designed for users who prefer a lower-level experience and working directly with SQL.* 
    - *Micronaut Data JDBC / R2DBC is useful for implementing the majority of the simple SQL queries that exist in a typical application and does not include any runtime query building DSLs. For more complex queries Micronaut Data JDBC / R2DBC can be paired with one of the many great existing Java SQL DSLs out there like JOOQ, QueryDSL, Requery or even JPA*
    - *An important aspect of Micronaut Data JDBC / R2DBC is that regardless whether you use JPA annotations or Micronaut Data annotations the entity classes must be compiled with Micronaut Data. This is because Micronaut Data pre-computes the persistence model (the relationships between entities, the class/property name to table/column name mappings) at compilation time, which is one of the reasons Micronaut Data JDBC can startup so fast.*
    - *Supported JDBC / R2DBC Dialects: H2, MYSQL, POSTGRES, SQL_SERVER, ORACLE*
    - <https://micronaut-projects.github.io/micronaut-data/latest/guide/#sql> 
- <u>sql</u>
  - <https://micronaut-projects.github.io/micronaut-sql/latest/guide/> 
  - <https://github.com/micronaut-projects/micronaut-sql>
  - **jooq**
    - <https://micronaut-projects.github.io/micronaut-sql/latest/guide/index.html#jooq>
    - <https://github.com/micronaut-projects/micronaut-sql/tree/master/jooq> 
  - **jdbi**
    - <https://micronaut-projects.github.io/micronaut-sql/latest/guide/index.html#jdbi> 
  - **vertx-pg**
    - <https://github.com/micronaut-projects/micronaut-sql/tree/master/vertx-pg-client>
  - **jasync**
    - <https://micronaut-projects.github.io/micronaut-sql/latest/guide/index.html#jasync>
- **r2dbc**
  -  <https://github.com/micronaut-projects/micronaut-r2dbc>
- **servlet**
  - *Provides integration between Micronaut and the Servlet API*
  - *provides support for replacing the Netty-based HTTP server that comes with the Micronaut framework with either Jetty, Tomcat, or Undertow*
  - *for users who*
    - *want to use Micronaut but the target deployment environment is based on Servlets*
    - *prefer the thread per connection model of the Servlet API over the Event Loop model provided by the default Netty-based HTTP server*
    - *have existing Servlets and/or Filters that they wish to combine with Micronaut.*
  - wenig Docs
  - HealthCheck-Bug: <https://github.com/micronaut-projects/micronaut-servlet/issues/296>
  - H2-Console
    ```
    tomcatFactory.getApplicationContext().registerSingleton(org.h2.server.web.WebServlet);
    ```
    (<https://github.com/tevore/micronaut-h2-console/blob/master/h2/src/main/java/com/tevore/h2/console/H2ConsoleSupport.java>)
  - <https://micronaut-projects.github.io/micronaut-servlet/latest/guide/>
  - <https://github.com/micronaut-projects/micronaut-servlet>
- **http-client**
  - *By default, Micronaut’s HTTP client is configured to support HTTP 1.1. To enable support for HTTP/2, set the supported HTTP version in configuration*
  - <https://guides.micronaut.io/latest/micronaut-http-client.html>
- **problem-json**
  - *makes it easy to produce application/problem+json responses from a Micronaut application*
  - *connects the [Problem library](https://github.com/zalando/problem) and Micronaut Error Formatting capabilities.* 
  - <https://micronaut-projects.github.io/micronaut-problem-json/latest/guide/>
- **flyway**
- **management**
- **micrometer**
  - <https://micronaut-projects.github.io/micronaut-micrometer/latest/guide/> 


## Test
- <https://melix.github.io/blog/2022/08/micronaut-test-resources.html>
  - *Micronaut Test Resources simplifies testing of applications which depend on external resources, by handling the provisioning and lifecycle of such resources automatically*
  - *while lots of test resources use Testcontainers under the hood, you can use any other technology to create resources* 


## Libs
- **jobrunr-micronaut-feature**
  - -> Java/Libs/Jobrunr 
  - <https://www.jobrunr.io/en/documentation/configuration/micronaut/>
- **micronaut-camunda**
  - <https://github.com/camunda-community-hub/micronaut-camunda-platform-7> 


## Tools
- **maven-plugin**
  - <https://github.com/micronaut-projects/micronaut-maven-plugin>
- **aot**
  - *implements ahead-of-time (AOT) optimizations for Micronaut application and libraries*
  - *Micronaut AOT is an experimental project. Use at your own risk.* (23.8.22) 
  - <https://micronaut-projects.github.io/micronaut-aot/latest/guide/> 
- **VSCode-Plugin**
  - -> IDE/VSCode 
- **generator-jhipster-micronaut**
  - <https://github.com/jhipster/generator-jhipster-micronaut> 
