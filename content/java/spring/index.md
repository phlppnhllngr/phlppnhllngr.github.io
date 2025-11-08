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
- ```
  Spring effectively:
  - scans the classpath for resources - that includes jars, file system
  - loads every single class matching the scanned directories as a byte array
  - parses it in java (not by JVM) to check what annotations it has (it doesn't load the classes actually)
  - builds dependency tree
  - enhances the previously loaded byte arrays, i.e. generates different byte code
  - loads the newly enhanced classes and create instances (usually through standard reflection)
  - makes calls like PostInit (life cycle)
  - in some cases it uses the standard java reflection to set fields/call methods; in lots of cases java reflection is generating (and loading) a new class (byte code) to carry the process
  ```

## Tipps
- <https://www.baeldung.com/spring-boot-memory-usage-optimization>
- <https://www.baeldung.com/spring-boot-startup-speed>
  - **Lazy Bean Initialization**
    - *means that Spring won't create all beans on startup. Also, Spring will inject no dependencies until that bean is needed. Since Spring Boot version 2.2. it's possible to enable lazy initialization using the application.properties: `spring.main.lazy-initialization=true`*
    - *Depending on the size of our codebase, lazy initialization can result in a significant amount of startup time reduction*
    - *However, lazy initialization has a few drawbacks. The most significant disadvantage is that the application will serve the first request slower. Because Spring needs time to initialize the required beans, another disadvantage is that we can miss some errors on startup. This can result in ClassNotFoundException during runtime.*
  - **Excluding Unnecessary Autoconfiguration**
    - *Spring may initialize beans that our application doesn't require. We can check all autoconfigured beans using startup logs. Setting the logging level to DEBUG on org.springframework.boot.autoconfigure in the application.properties: `logging.level.org.springframework.boot.autoconfigure=DEBUG`*
    - *Using this report, we can exclude parts of the application's configuration. To exclude part of the configuration, we use @EnableAutoConfiguration annotation: `@EnableAutoConfiguration(exclude = {JacksonAutoConfiguration.class, JvmMetricsAutoConfiguration.class, LogbackMetricsAutoConfiguration.class, MetricsAutoConfiguration.class})`*
    - siehe auch depclean-maven-plugin
  - **Turn off JMX**
    - *Spring Boot offers some MBeans to monitor our application using JMX. Turn off JMX entirely and avoid the cost of creating those beans: `spring.jmx.enabled=false`*
- **Open Session In View ausschalten**
  - *OSIV is really a bad idea from a performance and scalability perspective*
  - <https://stackoverflow.com/a/48222934/7437541>
  - `spring.jpa.open-in-view=false`
- <https://spring.io/blog/2018/11/08/spring-boot-in-a-container> (8.11.2018)
  - Performance-Tipps unter "Tweaks"
    - spring-context-indexer
    - -Dspring.config.location; Spring sucht (ggf. unnötig) an verschiedenen Stellen nach Config-Files
    - -Dspring.jmx.enabled=false; false ist der Default ab Spring Boot 2.2.0
    - -noverify, -XX:TieredStopAtLevel=1
    - -XX:+UnlockExperimentalVMOptions, -XX:+UseCGroupMemoryLimitForHeap (Java 8)
    - keine Actuators (Health, Metrics); Actuators erzeugen ca. 150 zusätzliche Beans
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


## Container
- <https://odedia.org/production-considerations-for-spring-on-kubernetes>
  - Tipps für Actuator + Probes: <https://odedia.org/production-considerations-for-spring-on-kubernetes#heading-liveness-and-readiness-probes>
    - *Spring Boot 2.3 took this concept [[Health Groups]](https://docs.spring.io/spring-boot/docs/2.2.x/reference/html/production-ready-features.html#health-groups) further by creating two health groups out of the box: a readiness group and a liveness group*
  - Spring Cloud <https://odedia.org/production-considerations-for-spring-on-kubernetes#heading-spring-cloud>
    - k8s Service Discovery
    - Configuration Watcher
- <https://spring.io/guides/gs/spring-boot-docker/>
- <https://www.baeldung.com/dockerizing-spring-boot-application>
- <https://www.baeldung.com/spring-boot-docker-images>
- -> Spring-Boot-Maven-Plugin:build-image
