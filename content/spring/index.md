---
layout: default
title: Spring
has_children: true
---

- [https://reflectoring.io/spring-bean-lifecycle/](https://reflectoring.io/spring-bean-lifecycle/)
- [SpringDeveloper@YouTube](https://www.youtube.com/channel/UC7yfnfvEUlXUIfm8rGLwZdA)
- [https://piotrminkowski.com/2021/01/13/spring-boot-tips-tricks-and-techniques/](https://piotrminkowski.com/2021/01/13/spring-boot-tips-tricks-and-techniques/)

## Zugriff auf Request-Body
  - **ContentCachingRequestWrapper**
    - [https://www.baeldung.com/spring-reading-httpservletrequest-multiple-times](https://www.baeldung.com/spring-reading-httpservletrequest-multiple-times)
  - **RequestBodyAdvice**
    - http://www.javabyexamples.com/quick-guide-to-requestbodyadvice-in-spring-mvc
    - beforeBodyRead(), afterBodyRead(), handleEmptyBody()
  - **Request scoped injectable bean** ("Request context")
    - https://stackoverflow.com/a/46046430/7437541
  - **HandlerInterceptor, HandlerInterceptorAdapter(deprecated) + RequestBodyAdvice**
    - https://stackoverflow.com/a/56044110/7437541


## Bücher
- [Spring Framework Cookbook](@attachment/Buecher/Spring/Spring-Framework-Cookbook.pdf)
  - Spring 4
  - kaum Erläuterungen
  - Batch
- [Spring 5.0 By Example](@attachment/Buecher/Spring/spring-5-example.pdf)
  - Spring Boot
  - Spring Data
    - Spring Data JPA
- [Mastering Spring 5.0](@attachment/Buecher/Spring/Mastering Spring 5.0.pdf)
- [Learning Spring 5.0](@attachment/Buecher/Spring/Learning Spring 5.0.pdf)
  - Spring DAO
  - Plain JDBC
  - Arten von DataSource
  - JDBCTemplate, versch. Arten
  - ORM
    - Hibernate
  - Transaction Management
      - propagation behaviors
- [Spring Framework Notes For Professionals](@attachment/Buecher/Spring/SpringFrameworkNotesForProfessionals.pdf)
  - JDBC
- [Hands-On High Performance with Spring 5](@attachment/Buecher/Spring/hands-high-performance-spring-5.pdf)
  - Async
  - Security
  - AOP
  - Database interaction
  - Hibernate
  - Messaging
  - Concurrency, Scheduling
  - Monitoring
- [Building a REST API with Spring 4](@attachment/Buecher/Spring/Building_a_REST_API_with_Spring 4.pdf)
- [Spring Boot Cookbook](@attachment/Buecher/Spring/Spring Boot Cookbook.pdf)
- [Spring Essentials](@attachment/Buecher/Spring/Spring Essentials.pdf)
- [spring 5.0 microservices](@attachment/Buecher/Spring/spring 5.0 microservices.pdf)
- [software architecture with spring 5](@attachment/Buecher/Spring/software architecture with spring 5.pdf)
- [Spring Security Essentials](@attachment/Buecher/Spring/Spring Security Essentials.pdf)
- [Spring 5 Design Patterns](@attachment/Buecher/Spring/Spring 5 Design Patterns.pdf)
- [Spring in Action, 5th Ed.](@attachment/Buecher/Spring/Spring in Action, 5th Edition by Craig Walls (z-lib.org).pdf)
- Spring Security In Action

### Boot
- [Learning Spring Boot 2.0](@attachment/Buecher/Spring/Learning Spring Boot 2.0 - Second Edition.pdf)


## Example projects
- piggymetrics
  - *tutorial project, which demonstrates Microservice Architecture Pattern using Spring Boot, Spring Cloud and Docker*
  - *auth, config, infrastructure services, service discovery, load balancer, circuit breaker, minitor, log, tracing*
  - https://github.com/sqshq/piggymetrics *10.5k
- https://github.com/corona-warn-app/cwa-server
- https://github.com/gtiwari333/spring-boot-web-application-sample *33
- https://github.com/ityouknow/spring-boot-examples
- books
  - *A demo project for Spring Boot / Data / security, social / oauth2 logons, JWT, Mongo, SpringBootAdmin, Docker, docker-compose, Github Actions and stateless apps*
  - https://github.com/aidanwhiteley/books *80
