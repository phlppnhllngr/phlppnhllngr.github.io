---
tags: [Notebooks/Spring]
title: 'Libs & Addons'
created: '2019-02-10T19:55:28.326Z'
modified: '2021-07-15T07:27:37.041Z'
parent: Spring
---

# Libs & Addons
- **dgs-framework**
  - *GraphQL server framework for Spring Boot*
  - <https://github.com/netflix/dgs-framework/>
- **spring-filter**
  - *dynamically filter entities. Your API will gain a full featured search functionality. You don't work with APIs? No problem, you may still not want to mess with SQL, JPA predicates, security. From a technical point of view, I compile a simple syntax to JPA predicates.*
  - `/search?filter= average(ratings) > 4.5 and brand.name in ('audi', 'land rover') and (year > 2018 or km < 50000) and color : 'white' and accidents is empty`
  - `@GetMapping(value = "/search") public List<Entity> search(@Filter Specification<Entity> spec, Pageable page)`
  - `Filter filter = filter(like("name", "%jose%"));`
  - <https://github.com/turkraft/spring-filter> *43
- **specification-arg-resolver**
  - <https://github.com/tkaczmarzyk/specification-arg-resolver> *405
  - *API for filtering data with Spring MVC & Spring Data JPA*
  - Query params -> JPA Specification
- **rsql-jpa-specification**
  - *Translate RSQL query into org.springframework.data.jpa.domain.Specification or com.querydsl.core.types.Predicate*
  - ```java
    filter = "company.code=='demo' and company.id>100";
    repository.findAll(RSQLSupport.toSpecification(filter));
    ```
  - <https://github.com/perplexhub/rsql-jpa-specification>
- **Riptide**
  - *next generation HTTP client*
  - *Based on spring-web and uses the same foundation as Spring's RestTemplate*
  - <https://github.com/zalando/riptide>
- **moduliths**
  - *Spring Boot extension based on ArchUnit*
  - *Enable developers to write architecturally evident code, i.e. provide means to express architectural concepts in code to close the gap between the two*
  - <https://github.com/odrotbohm/moduliths>
- **jasypt-spring-boot**
  - *provides Encryption support for property sources in Spring Boot Applications*
  - <https://github.com/ulisesbocchio/jasypt-spring-boot>
  - <https://www.baeldung.com/spring-boot-jasypt>
  - -> Java/Libs/Jasypt


## Dokumentation
- **swagger, springfox**
  - <http://springfox.github.io/springfox/>
  - <https://www.vojtechruzicka.com/documenting-spring-boot-rest-api-swagger-springfox/>
- **Spring REST Docs**
  - <https://spring.io/projects/spring-restdocs>
  - <https://github.com/ScaCap/spring-auto-restdocs>
- **springdoc-openapi**
  - <https://github.com/springdoc/springdoc-openapi>
  - *helps automating the generation of API documentation using spring boot projects*
- **openapi-generator-for-spring**
  - *automagically generates a OpenApi v3 specification at runtime for Spring Boot applications*
  - *Integrated Swagger UI*
  - *based on experience while using Spring Fox and SpringDoc OpenApi. As those libraries have turned out to be not flexible enough (...), this library aims at being fully customizable.*
  - <https://github.com/qaware/openapi-generator-for-spring>


## Admin
- **spring-boot-admin**
  - <https://github.com/codecentric/spring-boot-admin>
- <https://github.com/xeraa/microservice-monitoring>
  - *Monitor your Spring Boot application with the Elastic Stack*
- **Actuator**
  - *Monitoring our app, gathering metrics, understanding traffic, or the state of our database become trivial with this dependency. The main benefit of this library is that we can get production-grade tools without having to actually implement these features ourselves. Actuator is mainly used to expose operational information about the running application — health, metrics, info, dump, env, etc. It uses HTTP endpoints or JMX beans to enable us to interact with it.*
  - <https://www.baeldung.com/spring-boot-actuators>
  - *support for publishing authentication and authorization events in conjunction with Spring Security* → spring/security
