---
title: 'Libs & Addons'
parent: Spring
grand_parent: Java
---

# Libs & Addons
- **dgs-framework**
  - *GraphQL server framework for Spring Boot*
  - <https://github.com/netflix/dgs-framework/> <img loading="lazy" src="https://img.shields.io/github/stars/netflix/dgs-framework?style=flat-square">
- **spring-filter**
  - *dynamically filter entities. Your API will gain a full featured search functionality. You don't work with APIs? No problem, you may still not want to mess with SQL, JPA predicates, security. From a technical point of view, I compile a simple syntax to JPA predicates.*
  - `/search?filter= average(ratings) > 4.5 and brand.name in ('audi', 'land rover') and (year > 2018 or km < 50000) and color : 'white' and accidents is empty`
  - `@GetMapping(value = "/search") public List<Entity> search(@Filter Specification<Entity> spec, Pageable page)`
  - `Filter filter = filter(like("name", "%jose%"));`
  - <https://github.com/turkraft/spring-filter> <img loading="lazy" src="https://img.shields.io/github/stars/turkraft/spring-filter?style=flat-square">
- **specification-arg-resolver**
  - <https://github.com/tkaczmarzyk/specification-arg-resolver> <img loading="lazy" src="https://img.shields.io/github/stars/tkaczmarzyk/specification-arg-resolver?style=flat-square">
  - *API for filtering data with Spring MVC & Spring Data JPA*
  - Query params -> JPA Specification
- **rsql-jpa-specification**
  - *Translate RSQL query into org.springframework.data.jpa.domain.Specification or com.querydsl.core.types.Predicate*
  - ```java
    filter = "company.code=='demo' and company.id>100";
    repository.findAll(RSQLSupport.toSpecification(filter));
    ```
  - <https://github.com/perplexhub/rsql-jpa-specification> <img loading="lazy" src="https://img.shields.io/github/stars/perplexhub/rsql-jpa-specification?style=flat-square">
- **Riptide**
  - *next generation HTTP client*
  - *Based on spring-web and uses the same foundation as Spring's RestTemplate*
  - <https://github.com/zalando/riptide> <img loading="lazy" src="https://img.shields.io/github/stars/zalando/riptide?style=flat-square">
- **moduliths**
  - *Spring Boot extension based on ArchUnit*
  - *Enable developers to write architecturally evident code, i.e. provide means to express architectural concepts in code to close the gap between the two*
  - <https://github.com/odrotbohm/moduliths> <img loading="lazy" src="https://img.shields.io/github/stars/odrotbohm/moduliths?style=flat-square">
- **jasypt-spring-boot**
  - *provides Encryption support for property sources in Spring Boot Applications*
  - <https://github.com/ulisesbocchio/jasypt-spring-boot>
  - <https://www.baeldung.com/spring-boot-jasypt>
  - -> Java/Libs/Jasypt


## Dokumentation
- ~~springfox~~
  - GH Repo inaktiv
  - <http://springfox.github.io/springfox/>
  - <https://www.vojtechruzicka.com/documenting-spring-boot-rest-api-swagger-springfox/>
- **Spring REST Docs**
  - *It combines hand-written documentation written with Asciidoctor and auto-generated snippets produced with Spring MVC Test. This approach frees you from the limitations of the documentation produced by tools like Swagger.*
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
- **microservice-monitoring**
  - <https://github.com/xeraa/microservice-monitoring>
  - *Monitor your Spring Boot application with the Elastic Stack*
- **Ostara**
  - *desktop application that provides various features to monitor and interact with Spring Boot Applications via Actuator* 
  - <https://github.com/krud-dev/boost> 

