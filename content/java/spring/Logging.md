---
tags: [Notebooks/Spring]
title: Logging
created: '2020-07-27T12:18:30.563Z'
modified: '2021-09-09T07:01:08.840Z'
parent: Spring
grand_parent: Java
---

# Logging
- → Java/Logging
- *The mandatory logging dependency in Spring is the Jakarta Commons Logging API (JCL)* [2]
- *the modules in Spring depend explicitly on (Apache-)commons-logging (the canonical implementation of JCL)* [2]
- *Default configurations are provided for Java Util Logging, Log4J2, and Logback.*
- commons-logging nicht benutzen: <https://docs.spring.io/spring/docs/5.0.0.M5/spring-framework-reference/html/overview.html#overview-not-using-commons-logging>
- Slf4j benutzen: <https://docs.spring.io/spring/docs/5.0.0.M5/spring-framework-reference/html/overview.html#overview-logging-slf4j>


## spring-boot-starter-logging
- *every starter (...) depends on spring-boot-starter-logging* [1]
- *When using starters, <mark>Logback is used for logging by default</mark>* [1]
  - erweitert die XML-Tags von Logback; z.B. `<springProfile>` oder `<springProperty>`


## spring-cloud-sleuth
- *automatically adds trace and span IDs to our logs and propagates them from one service to the next via request headers when using supported HTTP clients*
  (<https://reflectoring.io/structured-logging/>)
- <https://github.com/spring-cloud/spring-cloud-sleuth>


## MDC
- denkbare Stellen zum Befüllen des MDC für Tracing
  - Filter (javax.servlet)
    - [4]
  - HandlerInterceptorAdapter
    - preHandle() [5, 8]
  - MDC zwischen Threads teilen: [6]
  - AOP-Annotationen [7]
  - (RequestBody)ControllerAdvice

<br/>
<hr/>
**Quellen**
- 1: <https://www.baeldung.com/spring-boot-logging>
- 2: <https://docs.spring.io/spring/docs/5.0.0.M5/spring-framework-reference/html/overview.html#overview-logging>
- 3: <https://reflectoring.io/springboot-logging/>
- 4: <https://oddblogger.com/spring-boot-mdc-logging> (14.3.21)
- 5: <https://dzone.com/articles/mdc-better-way-of-logging-1>
- 6: <https://www.sipios.com/blog-tech/how-to-use-logj-and-mdc-in-java-spring-boot-application>
- 7: <https://dzone.com/articles/setting-up-mdc-context-with-aop-in-spring-boot-app>
- 8: <https://reflectoring.io/structured-logging/>
