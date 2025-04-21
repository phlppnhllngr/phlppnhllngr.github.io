---
title: Module
parent: Spring
grand_parent: Java
---

# Module
{: .no_toc }
- <https://spring.io/projects/>


## Inhalt
{: .no_toc }
- TOC
{:toc}


## MVC
- **nützliche @ControllerAdvice**
  - ResponseBodyAdvice
  - ResponseEntityExceptionHandler
  - RequestBodyAdvice
- **Events**
  - <https://www.baeldung.com/spring-events>
  - <https://reflectoring.io/spring-boot-application-events-explained/>
  - zu beachten wenn `@EventListener` `@Async` ist: *event dispatcher does not know anything about the @Async annotation. So the dispatcher calls the [EventListener] methods synchronously. Only then, upon calling the proxied async method, the async proxy starts the original method in another thread.*
- **Caching (client side)**
  - <https://www.baeldung.com/spring-mvc-cache-headers>
- **Resource Updates**
  - <https://www.baeldung.com/spring-rest-json-patch>


## Data
-> Spring/Datenbank
- <https://spring.io/projects/spring-data>

### Data Redis
- <https://spring.io/projects/spring-data-redis>
- <https://docs.spring.io/spring-data/data-redis/docs/current/reference/html/>
- <https://www.baeldung.com/spring-boot-redis-cache>
- <https://b-nova.com/en/home/content/distributed-caching-with-redis-and-spring-boot>
- <https://www.digitalocean.com/community/tutorials/spring-boot-redis-cache>
- <https://www.baeldung.com/spring-data-redis-properties>
- Caching allgemein
  - <https://www.baeldung.com/spring-cache-tutorial>
  - <https://spring.io/guides/gs/caching/>
  - <https://reflectoring.io/spring-boot-cache/>
  - Error Handling
    - <https://hellokoding.com/spring-caching-custom-error-handler/>
    - <https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/cache/interceptor/LoggingCacheErrorHandler.html>
    - <https://github.com/gee4vee/circuit-breaker-redis-cache>


## Security
- <https://spring.io/projects/spring-security>
- **Submodul OAuth**
  - langfristig abgelöst durch Spring Authorization Server
- **Submodul Authorization Server**
  - *focused on delivering OAuth 2.1 Authorization Server support*
  - <https://github.com/spring-projects/spring-authorization-server>
- <https://www.baeldung.com/spring-boot-authentication-audit>
  - *Spring Boot Actuator module and the support for publishing authentication and authorization events in conjunction with Spring Security*
- <https://boudhayan-dev.medium.com/demystifying-spring-security-setup-e0491acc7df7>
- <https://www.infoworld.com/article/3630107/how-to-secure-rest-with-spring-security.html>
- [YT - Spring Security, demystified by Daniel Garnier Moiroux, 10/22](https://www.youtube.com/watch?v=iJ2muJniikY)

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
- **AbstractSecurityWebApplicationInitializer**
  - <https://www.javatpoint.com/spring-security-java-example> 


### LDAP
- <https://stevenschwenke.de/LDAPWithSpringSecurity>
- <https://www.baeldung.com/spring-security-ldap>
- <https://www.jhipster.tech/tips/016_tip_ldap_authentication.html>

### Test
- @WithMockUser
- @WithAnonymousUser


## Native
- <https://github.com/spring-projects-experimental/spring-native>


## Integration
- <https://docs.spring.io/spring-integration/docs/current/reference/html>
- Batch + Integration: <https://docs.spring.io/spring-batch/trunk/reference/html/springBatchIntegration.html>
- <https://www.reddit.com/r/java/comments/rscyoe/when_would_you_use_spring_integration/>
- <https://www.wimdeblauwe.com/blog/2024/06/25/transactional-outbox-pattern-with-spring-boot/>


## Batch
- zum Arbarbeiten von IO-Jobs
- jeder Job hat einen oder mehrere "Steps"
- jeder Step hat einen `ItemReader<Input>`, einen `ItemProcessor<Input, Output>` und einen `ItemWriter<Output>`
- Quellen für Inputs können Datenbanken, Dateien, in-Memory-Datenstrukturen, ... sein
- der Status der Steps und Jobs wird defaultmäßig in einer Datenbank festgehalten (konfigurierbar)
- in dem Zusammenhang ist oft von 'ETL' die Rede (Extract, Transform, Load)
- <https://docs.spring.io/spring-batch/reference/>
- Batch + Integration: <https://docs.spring.io/spring-batch/trunk/reference/html/springBatchIntegration.html>
- <https://www.toptal.com/spring/spring-batch-tutorial>
  ![image](https://github.com/phlppnhllngr/phlppnhllngr.github.io/assets/31002126/1e488a34-24c8-44c9-9e68-02b9da7a13ae)
  - Beispiele deprecated seit Spring Batch 5.1 (for Removal in 5.2)

### Job
- represents a batch job
- composed of multiple steps, and it defines the overall flow and configuration of the batch processing
- responsible for coordinating the execution of one or more steps in a specific order

### JobRepository
- responsible for managing metadata about job executions
- stores information such as job instances, job executions, step executions, and the state of each job
- This metadata is crucial for restarting failed jobs, tracking progress, and ensuring data integrity

### JobExecution
- represents the runtime execution of a job.
- Each time a job is started, a new JobExecution instance is created to track the execution status of the job.
- It contains information about the start time, end time, status (e.g., COMPLETED, FAILED), and any exceptions that occurred during the job execution.

### JobInstance
- represents a logical execution of a job.
- A job instance is created each time a job is launched with a unique set of parameters.
- For example, if you run a job to process a file with a specific name and date, each run of the job with different file names or dates would result in a new JobInstance.

## Statemachine
- <https://spring.io/projects/spring-statemachine>


## Plugin
- z. B. um das Strategy-Pattern zu implementieren; <https://spring.io/blog/2021/10/13/spring-tips-spring-plugin>
- <https://github.com/spring-projects/spring-plugin>


## Modulith
- *build well-structured Spring Boot applications and guides developers in finding and working with application modules driven by the domain*
- <https://spring.io/projects/spring-modulith>
- <https://spring.io/blog/2022/10/21/introducing-spring-modulith>
- <https://www.baeldung.com/spring-modulith>
- [YT - Spring Modulith – A Deep Dive (Workshop) - 3h - 09/2023](https://www.youtube.com/watch?v=430YOyMNjhs)
- <https://piotrminkowski.com/2023/10/13/guide-to-modulith-with-spring-boot/>
  - <https://old.reddit.com/r/java/comments/176zlbe/guide_to_modulith_with_spring_boot_piotrs_techblog/>
- <https://www.wimdeblauwe.com/blog/2024/06/25/transactional-outbox-pattern-with-spring-boot/>
  - TransactionalEventListener
  - Retry failed events (IncompleteEventPublications) 


## Actuator
- *Monitoring our app, gathering metrics, understanding traffic, or the state of our database become trivial with this dependency. The main benefit of this library is that we can get production-grade tools without having to actually implement these features ourselves. Actuator is mainly used to expose operational information about the running application — health, metrics, info, dump, env, etc. It uses HTTP endpoints or JMX beans to enable us to interact with it.*
- <https://www.baeldung.com/spring-boot-actuators>
- *support for publishing authentication and authorization events in conjunction with Spring Security* → spring/security
- <https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html>
- -> Libs+Addons/Admin/boost


## AI
- <https://spring.io/projects/spring-ai/>
