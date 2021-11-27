---
layout: default
title: Spring
has_children: true
---

- <https://reflectoring.io/spring-bean-lifecycle/>
- [SpringDeveloper@YouTube](https://www.youtube.com/channel/UC7yfnfvEUlXUIfm8rGLwZdA)
- <https://piotrminkowski.com/2021/01/13/spring-boot-tips-tricks-and-techniques/>

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
