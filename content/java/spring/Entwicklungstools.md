---
tags: [Notebooks/Spring]
title: Entwicklungstools
created: '2019-02-10T19:11:12.051Z'
modified: '2021-04-22T16:28:21.473Z'
parent: Spring
grand_parent: Java
---

# Entwicklungstools
- **Testcontainers**
  - für lokale Entwicklung (DB, Cache) statt docker(-compose)
  - <https://bsideup.github.io/posts/local_development_with_testcontainers/>
  - ^sollte man wahrscheinlich mit `@Profile` verbinden
- [devtools](https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-devtools)
- **Maven-Plugin**
  - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/>
  - <https://www.baeldung.com/spring-boot-repackage-vs-mvn-package>
  - Goals
    - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#?> 
    - run
      - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#goals-run> 
    - build-image
      - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#goals-build-image>
      - <https://docs.spring.io/spring-boot/docs/current/maven-plugin/reference/htmlsingle/#build-image.customization>
      - <https://www.baeldung.com/spring-boot-docker-images#buildpacks> 
    - repackage
      - *Repackage existing JAR and WAR archives so that they can be executed from the command line using java -jar. With layout=NONE can also be used simply to package a JAR with nested dependencies (and no main class, so not executable).*
      - `mvn clean package spring-boot:repackage`
- **ReBoot**
  - *refactoring tool to automatically apply best practices in Java / Spring-Boot applications*
  - <https://github.com/thanus/reboot>
- **spring-javaformat**
  - Maven- und Checkstyle-Plugin für Source-Code-Formatierung
  - <https://github.com/spring-io/spring-javaformat>
- **ngrok-spring-boot-starter**
  - *will automatically download Ngrok binary corresponding to your operating system (Windows, Linux, OSX or even Docker) and then cache it into home_directory/.ngrok2. Then every time you will run your Spring Boot application, Ngrok will automatically build http tunnel pointing to your springs web server*
  - <https://github.com/kilmajster/ngrok-spring-boot-starter>
- **Spring Boot Migrator**
  - *allows developers to convert existing, non Spring Boot applications, which are based on technologies such as JAX-RS, EJB and JMS to Spring Boot or upgrade older Spring Boot applications to the latest version*
  - *is based on OpenRewrite*
  - <https://github.com/spring-projects-experimental/spring-boot-migrator> 


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
