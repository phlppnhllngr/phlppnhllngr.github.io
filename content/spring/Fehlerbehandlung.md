---
tags: [Notebooks/Spring]
title: Fehlerbehandlung
created: '2019-02-10T19:06:33.162Z'
modified: '2021-08-15T11:47:08.211Z'
parent: Spring
---

# Error handling
- https://www.baeldung.com/exception-handling-for-rest-with-spring
- https://www.mscharhag.com/spring/rest-api-error-messages


## Was ein ErrorDTO beinhalten sollte
  - ID (für Wiederfinden im Log)
  - message (z.B. Request denied because of missing permissions)
  - detail (z.B. You don't have the permission to do X)
  - code (Zahl oder Enum, z.B. MISSING_PERMISSION)


## Spring-eigene Möglichkeiten
- ErrorController, BasicErrorController
  - *By default, Spring Boot [v2.1] provides a BasicErrorController controller for /error mapping that handles all errors, and getErrorAttributes to produce a JSON response with details of the error, the HTTP status, and the exception message.* 
    ```json
    {
      "timestamp": "2019-02-27T04:03:52.398+0000",
      "status": 500,
      "error": "Internal Server Error",
      "message": "...",
      "path": "/path"
    }
    ```
    Diese json-Attribute können per `CustomErrorAttributes extends DefaultErrorAttributes` geändert werden.
  - *Spring Boot DOES NOT make a new request to /error endpoint. Instead, it wraps the exception in the original request and forwards it to /error endpoint. The request will be processed by BasicErrorHandler if you don't provide a custom error handler.*
  - BasicErrorController extenden ist ErrorController-Impl. i.d.R. vorzuziehen
  - Quellen:
    - https://mkyong.com/spring-boot/spring-rest-error-handling-example/
    - https://www.baeldung.com/exception-handling-for-rest-with-spring#spring-boot
    - https://www.baeldung.com/spring-boot-custom-error-page
- Whitelabel Error Page
- HandlerExceptionResolver
  - DefaultHandlerExceptionResolver
    - *The default implementation of the HandlerExceptionResolver interface, resolving standard Spring MVC exceptions and translating them to corresponding HTTP status codes.*
- @ExceptionHandler
- @ControllerAdvice, ResponseEntityExceptionHandler


## Libs
- Zalando/problem-spring-web
  - https://github.com/zalando/problem-spring-web
- spring-retry
  - https://github.com/spring-projects/spring-retry *900
- errors-spring-boot-starter
  - https://github.com/alimate/errors-spring-boot-starter *216
- → resilience4j
- error-handling-spring-boot-starter
  - https://github.com/wimdeblauwe/error-handling-spring-boot-starter *105
  - https://www.reddit.com/r/java/comments/mul95u/better_error_handling_for_your_spring_boot_rest/
    - Vergleich mit zalando/problem-spring-web
- spring-rest-exception-handler
  - https://github.com/jirutka/spring-rest-exception-handler *350 (inaktiv seit 2016)
  - *handle custom exceptions, customize error responses and even localize them*
