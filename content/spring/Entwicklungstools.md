---
tags: [Notebooks/Spring]
title: Entwicklungstools
created: '2019-02-10T19:11:12.051Z'
modified: '2021-04-22T16:28:21.473Z'
parent: Spring
---

# Entwicklungstools
- **Testcontainers**
  - für lokale Entwicklung (DB, Cache) statt docker(-compose)
  - <https://bsideup.github.io/posts/local_development_with_testcontainers/>
  - ^sollte man wahrscheinlich mit `@Profile` verbinden
- [devtools](https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-devtools)
- **Maven-Plugin**
  - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/html/>
  - <https://www.baeldung.com/spring-boot-repackage-vs-mvn-package>
- **ReBoot**
  - *refactoring tool to automatically apply best practices in Java / Spring-Boot applications*
  - <https://github.com/thanus/reboot>
- **spring-javaformat**
  - Maven- und Checkstyle-Plugin für Source-Code-Formatierung
  - <https://github.com/spring-io/spring-javaformat>


## Codegeneratoren, Meta-Frameworks
- **jhipster**
  - <https://www.jhipster.tech/>
  - Tools
    - <https://start.jhipster.tech/jdl-studio/>
    - <https://start.jhipster.tech/>
  - Bücher
    - <http://www.jhipster-book.com/#!/>
    - <https://github.com/PacktPublishing/Full-Stack-Development-with-JHipster>
- **gemini**
  - <https://github.com/gemini-projects/gemini> *100
  - *Model Driven REST framework to automatically generate CRUD APIs*
  - *Gemini has a modular structure but the artifact is always a Spring Boot application that you can run everywhere*
  - *No Code Generation: Gemini uses internal engine to handle entities data and web controllers*
- **hilla**
  - *Build fast reactive web apps with full type safety. Powered by Lit and Spring Boot. Built by Vaadin.*
  - <https://github.com/vaadin/hilla>
  - [Spring Tips: Hilla, a new frontend and backend framework from Vaadin](ttps://www.youtube.com/watch?v=ADLbkZnKjA0)