---
title: Module
parent: Spring
grand_parent: Java
---

# Module
- <https://spring.io/projects/>

## MVC
- **nützliche @ControllerAdvice**
  - ResponseBodyAdvice
  - ResponseEntityExceptionHandler
  - RequestBodyAdvice
- **Events**
  - <https://www.baeldung.com/spring-events>
- **Caching (client side)**
  - https://www.baeldung.com/spring-mvc-cache-headers
- **Resource Updates**
  - https://www.baeldung.com/spring-rest-json-patch


## Security
- <https://spring.io/projects/spring-security>
- **Submodul OAuth**
  - langfristig abgelöst durch Spring Authorization Server
- **Submodul Authorization Server**
  - *focused on delivering OAuth 2.1 Authorization Server support*
  - https://github.com/spring-projects/spring-authorization-server
- https://www.baeldung.com/spring-boot-authentication-audit
  - *Spring Boot Actuator module and the support for publishing authentication and authorization events in conjunction with Spring Security*
- https://boudhayan-dev.medium.com/demystifying-spring-security-setup-e0491acc7df7
- https://www.infoworld.com/article/3630107/how-to-secure-rest-with-spring-security.html

### API
- **@EnableWebSecurity**
  - *spring-boot-starter-security activates `@EnableWebSecurity` for us. This applies Spring's default security configuration to our application. Default security activates both HTTP security filters and the security filter chain and applies basic authentication to our endpoints.*
  - *Although most of our requirements can be met by extending `WebSecurityConfigurerAdapter`, there may be occasions where we want to replace Spring's default Security configuration entirely. To do this, we can implement `WebSecurityConfigurer` rather than extend WebSecurityConfigurerAdapter*
  - <https://www.baeldung.com/spring-enablewebsecurity-vs-enableglobalmethodsecurity>
- **@EnableGlobalMethodSecurity**
  - *To apply security using an annotation-driven approach, we can use `@EnableGlobalMethodSecurity`.*
  - *Our annotated security only gets applied when we enter a class via a public method*
  - *By default, Spring AOP proxying is used to apply method security. If a secured method A is called by another method within the same class, security in A is ignored altogether. This means method A will execute without any security checking. The same applies to private methods.*
  - *Spring SecurityContext is thread-bound. By default, the security context isn't propagated to child threads.*
  - **@EnableGlobalMethodSecurity**(
      prePostEnabled = boolean, // enables @Pre/Post
      jsr250Enabled = boolean, // enables @RoleAllowed
      securedEnabled = boolean // enables @Secured
    )
  - @Secured
    - *used to specify a list of roles on a method*
  - @RoleAllowed
    - *JSR-250’s equivalent annotation of the @Secured annotation*
  - @RolesAllowed
  - @PreAuthorize
    - *@PreAuthorize and @PostAuthorize annotations provide expression-based access control*
    - *consider putting that annotation at class level*
  - @PostAuthorize
  - https://www.baeldung.com/spring-security-method-security
  - @PreFilter
    - *filter a collection argument before executing the method*
  - @PostFilter
    - *filter the returned collection of a method*
- **WebSecurityConfigurerAdapter**
- **AuthenticationManager**


### LDAP
- <https://stevenschwenke.de/LDAPWithSpringSecurity>
- <https://www.baeldung.com/spring-security-ldap>

### Test
- @WithMockUser
- @WithAnonymousUser


## Native
- <https://github.com/spring-projects-experimental/spring-native>


## Integration
- <https://docs.spring.io/spring-integration/docs/current/reference/html>
- Batch + Integration: <https://docs.spring.io/spring-batch/trunk/reference/html/springBatchIntegration.html>
- <https://www.reddit.com/r/java/comments/rscyoe/when_would_you_use_spring_integration/>


## Batch
- zum Arbarbeiten von IO-Jobs
- jeder Job hat einen oder mehrere "Steps"
- jeder Step hat einen `ItemReader<Input>`, einen `ItemProcessor<Input, Output>` und einen `ItemWriter<Output>`
- Quellen für Inputs können Datenbanken, Dateien, in-Memory-Datenstrukturen, ... sein
- der Status der Steps und Jobs wird defaultmäßig in einer Datenbank festgehalten (konfigurierbar)
- in dem Zusammenhang ist oft von 'ETL' die Rede (Extract, Transform, Load)
- Batch + Integration: <https://docs.spring.io/spring-batch/trunk/reference/html/springBatchIntegration.html>


## Statemachine
- <https://spring.io/projects/spring-statemachine>


## Plugin
- z. B. um das Strategy-Pattern zu implementieren; <https://spring.io/blog/2021/10/13/spring-tips-spring-plugin>
- <https://github.com/spring-projects/spring-plugin>
