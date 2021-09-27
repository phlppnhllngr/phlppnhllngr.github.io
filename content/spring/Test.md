---
tags: [Notebooks/Spring]
title: Test
created: '2019-02-10T19:09:11.609Z'
modified: '2021-08-29T16:06:34.251Z'
parent: Spring
---

# Test
- https://rieckpil.de/test-your-spring-mvc-controller-with-webtestclient-against-mockmvc/
- Chaos Monkey
  - https://github.com/codecentric/chaos-monkey-spring-boot
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
- [https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html#integration-testing-annotations]()
- **@SpringBootTest** (🥾)
  - *automagically spins up your application with all dependencies instrumenting it for use in tests. It can replace dependencies and provide customized properties for the application context.*
  - *it bootstraps the whole application the same way as it would be running otherwise*
  - *can take a very long time to start—most of it related to database initialization, the configuration of remote sources, and other IO (input/output).*
  - *End-to-end tests would be the best place for the tests with @SpringBootTest, assuming the whole application is a black box.*
  - need to manually override bean definitions
- **@ContextConfiguration**
  - *loads an ApplicationContext for Spring integration test*
  - *can load the JavaConfig annotated with @Configuration. can also load a component annotated with @Component, @Service, @Repository etc.*
- **@TestConfiguration** (🥾)
  - *can use it to override certain bean definitions, for example to replace real beans with fake beans or to change the configuration of a bean to make it better testable*
  - [https://reflectoring.io/spring-boot-testconfiguration/]()
- **@TestExecutionListeners**
  - Lifecycle-Callbacks für Tests ("Erweiterung" des Junit-Lifecycle)
  - [https://www.baeldung.com/spring-testexecutionlistener]()
- **@TestPropertySource**
  - *used to configure the locations of properties files and inlined properties to be added to the Environment's set of PropertySources for an ApplicationContext for integration tests.*
  - [https://www.baeldung.com/spring-test-property-source]()
  - [https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/context/TestPropertySource.html]()
- **@AutoConfigureMockMvc** (🥾)
- **@MockBean** (🥾)
- **@DataJpaTest** (🥾)
  - für Repository-Layer
- **@AutoConfigureTestDatabase** (🥾)
  - *you don’t override beans manually to provide an additional configuration, as it would be necessary with @SpringBootTest annotation. @DataJpaTest along with @AutoConfigureTestDatabase automatically prepare the context for the repository component and configure the H2 database engine to mimic an actual database*
- **@WebMvcTest** (🥾)
  - für Controller-Layer
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
- **MockMvc**
- **TestRestTemplate**
