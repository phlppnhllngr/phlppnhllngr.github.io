---
title: Test
parent: Spring
grand_parent: Java
---

# Test
- <https://rieckpil.de/test-your-spring-mvc-controller-with-webtestclient-against-mockmvc/>
- [YT - Things I Wish I Knew When I Started Testing Spring Boot Applications by Philip Riecks, 10/22](https://www.youtube.com/watch?v=5Td7vAS9qJI)
- <https://www.baeldung.com/spring-boot-testing-pitfalls>
- Chaos Monkey
  - <https://github.com/codecentric/chaos-monkey-spring-boot>
- Junit4 von spring-boot-starter-test ausschließen
  ```xml
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
    <exclusions>
        <exclusion>
            <groupId>org.junit.vintage</groupId>
            <artifactId>junit-vintage-engine</artifactId>
        </exclusion>
    </exclusions>
  </dependency>
  ```

## Klassen
- 🥾 = Spring-Boot-API
- <https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html#integration-testing-annotations>
- **@SpringBootTest** (🥾)
  - *automagically spins up your application with all dependencies instrumenting it for use in tests. It can replace dependencies and provide customized properties for the application context.*
  - *it bootstraps the whole application the same way as it would be running otherwise*
  - *can take a very long time to start—most of it related to database initialization, the configuration of remote sources, and other IO (input/output).*
  - *End-to-end tests would be the best place for the tests with @SpringBootTest, assuming the whole application is a black box.*
  - *need to manually override bean definitions*
  - *@SpringBootTest, by default, starts searching in the current package of the test class and then searches upwards through the package structure, looking for a class annotated with @SpringBootConfiguration, from which it then reads the configuration to create an application context. This class is usually our main application since the @SpringBootApplication annotation includes the @SpringBootConfiguration annotation. It then creates an application context similar to the one that would be started in a production environment.*
  - *If we need a different (minimal) ApplicationContext for our test class, we can create a static inner @Configuration class* (<https://www.baeldung.com/spring-boot-testing-pitfalls#2-minimize-applicationcontext>)
- **@ContextConfiguration**
  - *loads an ApplicationContext for Spring integration test*
  - *can load the JavaConfig annotated with @Configuration. can also load a component annotated with @Component, @Service, @Repository etc.*
- **@TestConfiguration** (🥾)
  - *can use it to override certain bean definitions, for example to replace real beans with fake beans or to change the configuration of a bean to make it better testable*
  - <https://reflectoring.io/spring-boot-testconfiguration>
- **@TestExecutionListeners**
  - Lifecycle-Callbacks für Tests ("Erweiterung" des Junit-Lifecycle)
  - <https://www.baeldung.com/spring-testexecutionlistener>
- **@TestPropertySource**
  - *used to configure the locations of properties files and inlined properties to be added to the Environment's set of PropertySources for an ApplicationContext for integration tests.*
  - org.springframework.test.context.TestPropertySource
  - ```java
    @TestPropertySource(
      locations = {
        "classpath:config/test/test.properties"
      },
      properties = {
        "hibernate.hbm2ddl.auto = create-drop",
        "hibernate.dialect = org.hibernate.dialect.H2Dialect",
        "hibernate.hbm2ddl.import_files = development/testdata.sql"
      }
    )
    class FooTest {}
    ```
  - <https://www.baeldung.com/spring-test-property-source>
  - <https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/context/TestPropertySource.html>
- **@DynamicPropertySource**
  - *Method-level annotation for integration tests that need to add properties with dynamic values* 
  - <https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/context/DynamicPropertySource.html> 
- **@AutoConfigureMockMvc** (🥾)
- **@MockBean** (🥾)
  - *Spring Test Framework includes Mockito to create and use mocks. When using @MockBean, we let Mockito create a mock instance and put it into the ApplicationContext*
  - *The consequence is that we cannot share the ApplicationContext with other test classes* (<https://www.baeldung.com/spring-boot-testing-pitfalls#3-pitfall-mocking>)
- **@DataJpaTest** -> Spring/Datenbank/Data JPA/Test
- **@AutoConfigureTestDatabase** -> Spring/Datenbank/Data JPA/Test
- **@WebFluxTest**
  - *We can use the @WebFluxTest annotation to test Spring WebFlux controllers. It's often used along with @MockBean to provide mock implementations for required dependencies.*
- **@JdbcTest**
  - *We can use the @JdbcTest annotation to test JPA applications, but it's for tests that only require a DataSource. The annotation configures an in-memory embedded database and a JdbcTemplate.*
- **@JooqTest**
  - *To test jOOQ-related tests, we can use @JooqTest annotation, which configures a DSLContext.*
- **@DataMongoTest**
  - *To test MongoDB applications, @DataMongoTest is a useful annotation. By default, it configures an in-memory embedded MongoDB if the driver is available through dependencies, configures a MongoTemplate, scans for @Document classes, and configures Spring Data MongoDB repositories.*
- **@DataRedisTest**
  - *makes it easier to test Redis applications. It scans for @RedisHash classes and configures Spring Data Redis repositories by default.*
- **@DataLdapTest**
  - *configures an in-memory embedded LDAP (if available), configures a LdapTemplate, scans for @Entry classes, and configures Spring Data LDAP repositories by default.*
- **@RestClientTest**
  - *We generally use the @RestClientTest annotation to test REST clients. It auto-configures different dependencies such as Jackson, GSON, and Jsonb support; configures a RestTemplateBuilder; and adds support for MockRestServiceServer by default.*
- **@JsonTest** (🥾)
  - *Initializes the Spring application context only with those beans needed to test JSON serialization.*
- **ReflectionTestUtils**
- **TestPropertyValues** (🥾)
- **SpringExtension** (JUnit5 @ExtendWith)
  - *As of Spring Boot 2.1, we no longer need to load the SpringExtension because it's included as a meta annotation in the Spring Boot test annotations like @DataJpaTest, @WebMvcTest, and @SpringBootTest.*
- **SpringRunner** (alias für SpringJUnit4ClassRunner; JUnit4 @RunWith)
- **@WebMvcTest** (🥾)
  - für Controller-Layer
  - <https://reflectoring.io/spring-boot-web-controller-test/>
  - <https://spring.io/guides/gs/testing-web/>
- **MockMvc**
  - *Main entry point for server-side Spring MVC test support* 
  - <https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/web/servlet/MockMvc.html> 
- **@AutoConfigureMockMvc** (🥾)
  - *enable and configure auto-configuration of `MockMvc`* 
  - <https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/web/servlet/AutoConfigureMockMvc.html> 
- **TestRestTemplate**
  - *Convenient alternative of `RestTemplate` that is suitable for integration tests. TestRestTemplate is fault-tolerant. This means that 4xx and 5xx do not result in an exception being thrown and can instead be detected through the response entity and its status code.*
  - <https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/web/client/TestRestTemplate.html>
- **@DirtiesContext**
  - *marks the ApplicationContext as dirty, so it is closed and removed from the cache after the test*
  - für Testmethoden, die z. B. den Zustand von Singleton-Beans verändern, und die Änderung den nächsten Test beeinflussen könnte 
  - <https://www.baeldung.com/spring-boot-testing-pitfalls#1-petservice-sample-solutions>
- **@ActiveProfiles**
  - *class-level annotation that is used to declare which active bean definition profiles should be used when loading an ApplicationContext for test classes*
- **@ServiceConnection** (🥾)
  - Verwendung mit Testcontainers 
  - SB 3.1.0+
  - <https://spring.io/blog/2023/06/23/improved-testcontainers-support-in-spring-boot-3-1>
  - <https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/testcontainers/service/connection/ServiceConnection.html> 
