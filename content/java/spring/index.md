---
layout: default
title: Spring
has_children: true
parent: Java
---

# Spring
- <https://reflectoring.io/spring-bean-lifecycle/>
- [SpringDeveloper@YouTube](https://www.youtube.com/channel/UC7yfnfvEUlXUIfm8rGLwZdA)
- <https://piotrminkowski.com/2021/01/13/spring-boot-tips-tricks-and-techniques/>
- <https://www.reddit.com/r/java/comments/sos5x1/spring_boot_microservices_coding_style_guidelines/>

## Tipps
- <https://www.baeldung.com/spring-boot-startup-speed>
  - **Lazy Bean Initialization**
    - *means that Spring won't create all beans on startup. Also, Spring will inject no dependencies until that bean is needed. Since Spring Boot version 2.2. it's possible to enable lazy initialization using the application.properties: `spring.main.lazy-initialization=true`*
    - *Depending on the size of our codebase, lazy initialization can result in a significant amount of startup time reduction*
    - *However, lazy initialization has a few drawbacks. The most significant disadvantage is that the application will serve the first request slower. Because Spring needs time to initialize the required beans, another disadvantage is that we can miss some errors on startup. This can result in ClassNotFoundException during runtime.*
  - **Excluding Unnecessary Autoconfiguration**
    - *Spring may initialize beans that our application doesn't require. We can check all autoconfigured beans using startup logs. Setting the logging level to DEBUG on org.springframework.boot.autoconfigure in the application.properties: `logging.level.org.springframework.boot.autoconfigure=DEBUG`*
    - *Using this report, we can exclude parts of the application's configuration. To exclude part of the configuration, we use @EnableAutoConfiguration annotation: `@EnableAutoConfiguration(exclude = {JacksonAutoConfiguration.class, JvmMetricsAutoConfiguration.class, LogbackMetricsAutoConfiguration.class, MetricsAutoConfiguration.class})`*
  - **Turn off JMX**
    - *Spring Boot offers some MBeans to monitor our application using JMX. Turn off JMX entirely and avoid the cost of creating those beans: `spring.jmx.enabled=false`*
- **Open Session In View ausschalten**
  - *OSIV is really a bad idea from a performance and scalability perspective*
  - <https://stackoverflow.com/a/48222934/7437541>
  - `spring.jpa.open-in-view=false`
- <https://piotrminkowski.com/2021/01/13/spring-boot-tips-tricks-and-techniques/>
- <https://www.baeldung.com/spring-boot-build-properties>


## Zugriff auf Request-Body
- **ContentCachingRequestWrapper**
  - <https://www.baeldung.com/spring-reading-httpservletrequest-multiple-times>
- **RequestBodyAdvice**
  - <http://www.javabyexamples.com/quick-guide-to-requestbodyadvice-in-spring-mvc>
  - beforeBodyRead(), afterBodyRead(), handleEmptyBody()
- **Request scoped injectable bean** ("Request context")
  - <https://stackoverflow.com/a/46046430/7437541>
- **HandlerInterceptor, HandlerInterceptorAdapter(deprecated) + RequestBodyAdvice**
  - <https://stackoverflow.com/a/56044110/7437541>


## Validierung
- <https://reflectoring.io/bean-validation-with-spring-boot/>


## Example projects
- **piggymetrics**
  - *tutorial project, which demonstrates Microservice Architecture Pattern using Spring Boot, Spring Cloud and Docker*
  - *auth, config, infrastructure services, service discovery, load balancer, circuit breaker, minitor, log, tracing*
  - <https://github.com/sqshq/piggymetrics> *10.5k
- <https://github.com/corona-warn-app/cwa-server>
- <https://github.com/gtiwari333/spring-boot-web-application-sample> *33
- <https://github.com/ityouknow/spring-boot-examples>
- **books**
  - *A demo project for Spring Boot / Data / security, social / oauth2 logons, JWT, Mongo, SpringBootAdmin, Docker, docker-compose, Github Actions and stateless apps*
  - <https://github.com/aidanwhiteley/books> *80
- **spring-warehouse**
  - <https://github.com/averageflow/spring-warehouse>
  - [Diskussion auf /r/java](https://www.reddit.com/r/java/comments/rqqvbh/spring_warehouse_a_quest_to_learn_more_java_and.compact)


## Docker
- <https://spring.io/guides/gs/spring-boot-docker/>
- <https://www.baeldung.com/dockerizing-spring-boot-application>
- <https://www.baeldung.com/spring-boot-docker-images>
