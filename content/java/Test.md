---
tags: [Notebooks/Java]
title: Test
created: '2019-02-10T19:18:08.769Z'
modified: '2021-09-13T12:20:37.269Z'
parent: Java
---

# Test
- <https://phauer.com/2019/modern-best-practices-testing-java>
- <https://github.com/akullpp/awesome-java#testing>

## BDD
- **cucumber**
  - <https://cucumber.io/docs/guides/10-minute-tutorial>
  - Integration mit Junit
  - Tools
    - courgette
      - <https://github.com/prashant-ramcharan/courgette-jvm> *60
      - *Multi-threaded / Parallelize your Java Cucumber tests on a feature level or on a scenario level*
- **jbehave**
  - <https://jbehave.org>
- **serenity**
  - <https://serenity-bdd.info>


## Unit
- **JUnit**
  - <https://junit.org>
  - <u>Plugins & Erweiterungen</u>
    - JUnitParams
      - <https://github.com/Pragmatists/JUnitParams>
        ```java
          @Test @Parameters({"17, false", "22, true" })
          public void personIsAdult(int age, boolean valid) throws Exception {
            assertThat(new Person(age).isAdult(), is(valid));
          }
        ```
      - Modul für Integration mit Spring
    - junit-dataprovider
      - <https://github.com/TNG/junit-dataprovider>
      - ähnlich JUnitParams, aber konfigurierbarer
    - DbUnit
      - <http://dbunit.sourceforge.net>
      - *targeted at database-driven projects that, among other things, puts your database into a known state between test runs*
      - database rider
        - *aims for bringing DBUnit closer to your JUnit tests*
        - <https://github.com/database-rider/database-rider>
    - junit-pioneer
      - <https://github.com/junit-pioneer/junit-pioneer>
      - *Default Locale and TimeZone, Setting Environment Variables, Retrying, Stopwatch, ...*
    - JfrUnit
      - *for asserting JDK Flight Recorder events*
      - <https://github.com/moditect/jfrunit>
      - <https://www.morling.dev/blog/towards-continuous-performance-regression-testing>
    - JsonUnit
      - *simplifies JSON comparison*
      - AssertJ, hamcrest oder Spring MockMvc
      - <https://github.com/lukas-krecan/JsonUnit>
- **TestNG**
  - <http://testng.org/doc>
- **EqualsVerifier**
  - *verify whether the contract for the equals and hashCode methods in a class is met*
  - <https://github.com/jqno/equalsverifier>


## Mock
- **Mockito**
  - <https://site.mockito.org>
  - <https://github.com/mockito/mockito>
  - Modul für JUnit
  - ab v3.4.0 auch statische Methoden: <https://asolntsev.github.io/en/2020/07/11/mockito-static-methods>
- **Powermock**
  - <https://github.com/powermock/powermock>
  - *PowerMock is a Java framework that allows you to unit test code normally regarded as untestable... For example final classes and methods cannot be used, private methods sometimes need to be protected or unnecessarily moved to a collaborator, static methods should be avoided completely and so on simply because of the limitations of existing frameworks...*
  - <https://github.com/powermock/powermock/wiki/Getting-Started>
  - Module für EasyMock und Mockito ("PowerMockito") (PowerMock kann nur zusammen mit einer dieser Libs verwendet werden)
  - Module für Junit (3 & 4) und TestNG
  - Snippets
    - nur eine einzige statische Methode einer Klasse mocken, die restlichen belassen:
    ```java
    PowerMockito.stub(PowerMockito.method(TheClass.class, "someStaticMethod", Mockito.any())).toReturn("my return value");
    ```
- **easymock**
  - <http://easymock.org>
- **jmock**
  - <http://jmock.org>
- **jmockit**
  - <https://jmockit.github.io>
- **system rules**
  - "mocks" java.lang.System
  - <https://www.baeldung.com/java-system-rules-junit>
- **jimfs**
  - *An in-memory file system for Java 7+*
  - <https://github.com/google/jimfs>
- <u>HTTP/API</u>
  - **wiremock**
    - mit Junit4-Rule
    - <http://wiremock.org/docs/getting-started>
  - **pact**
    - mit Junit-Rule
- <u>Datum & Zeit</u>
  - <http://blog.tremblay.pro/2021/01/mocking-clock.html>


## Generierung von Testdaten
- **Mockneat**
  - <https://www.mockneat.com>
  - Zufallsgenerator für Primitivwrapper, Emailadressen, Namen, Adressen, ...
- **easy-random**
  - <https://github.com/j-easy/easy-random>
  - früher: benas/random-beans
  - Für eigene Klassen
  - Hat auch Modul, womit Bean-Validation-Annotationen berücksichtigt werden
  - Hat faker-Randomizer (dependency: java-faker)
  - Unterstützt (manche) Collections nicht, z.B. `EnumSet`. Dafür gibt es die `EasyRandomParameters`:
    ```java
    class Person {
      Address address;
    }
    class Address {
      Street street;
    }
    class Street {
      String name;
    }
    ``` 
  - *The library will recursively populate all the object graph*
- **Java Faker**
  - <https://github.com/DiUS/java-faker>
  - Namen, Telefon, IBAN, ...
- **beanmother**
  - generiert Zufallsobjekte anhand yaml-template
  - <https://github.com/keepcosmos/beanmother>
- **jqwik**
  - <https://jqwik.net>


## REST
- **rest-assured**
  - *Java DSL for easy testing of REST services*
  - <https://github.com/rest-assured/rest-assured>
  - Modul für Spring: <https://github.com/rest-assured/rest-assured/wiki/Usage#spring-support>


## Integration
- **Testcontainers**
  - <http://testcontainers.org>


## Assertations & Matchers
- **Hamcrest**
  - <http://hamcrest.org/JavaHamcrest>
- **JsonPath**
- **AssertJ**
  - <http://joel-costigliola.github.io/assertj>
  - fluent API
- **truth**
  - *Fluent assertions*
  - <https://github.com/google/truth/>


## Coverage
- **JaCoCo**
  - <https://www.eclemma.org/jacoco>


## Benchmarks, Performance
- → Junit/JfrUnit
- **JMH**
  - <http://openjdk.java.net/projects/code-tools/jmh>
  - <https://github.com/Valloric/jmh-playground>
  - <https://www.retit.de/continuous-benchmarking-with-jmh-and-junit>
- **caliper**
  - <https://github.com/google/caliper> *620
- **quickperf**
  - *quickly evaluate and improve some performance-related*
  - Annotationen für `@Test`-Methoden
  - *configure test-jvm* (xmx, xms, jvm-options)
  - *measure & dump heap*
  - <https://github.com/quick-perf/quickperf>


## Async
- <https://github.com/akullpp/awesome-java#asynchronous>
- **awaitility**
  - <http://www.awaitility.org>
  - *Awaitility is a DSL that allows you to express expectations of an asynchronous system in a concise and easy to read manner. For example:*
    ```java
    @Test
    public void updatesCustomerStatus() throws Exception {
        // Publish an asynchronous event:
        publishEvent(updateCustomerStatusEvent);
        // Awaitility lets you wait until the asynchronous operation completes:
        await().atMost(5, SECONDS).until(customerStatusIsUpdated());
        ...
    }
    ```
  - <https://www.baeldung.com/awaitlity-testing>


## Microservices
- **Arquillian**
  - <http://arquillian.org>


## Architektur
- **ArchUnit**
  - <https://github.com/TNG/ArchUnit>
  - Regeln festlegen, z.B. dass
    - Paket x keine Klassen aus Paket y importieren darf
    - Schicht x (z.B. 'persistence') nur von Schicht y (z.B. 'service') benutzt werden darf
    - Klassennamen im Paket 'dto' mit 'DTO' enden müssen
    - alle Klassen mit Annotation '@Controller' die Annotation '@RequestMapping' haben müssen
    - öffentliche Methoden in @Controller-Klassen mit @RequestMapping annotiert sein müssen
    - *flag usage of outdated apis* (?) (util.Calendar)
    - eigene
  - Integration mit JUnit
  - Tutorials
    - <https://blogs.oracle.com/javamagazine/unit-test-your-architecture-with-archunit>
    - <https://www.baeldung.com/java-archunit-intro>


## Mutation
- **pitest**
  - <https://github.com/hcoles/pitest>


## Chaos
- **perses**
  - <https://github.com/nicolasmanic/perses> *35


## Test-Generatoren
- **EvoSuite**
  - *Generation of JUnit 4 tests for the selected classes*
  - <https://www.evosuite.org/evosuite>
  - <https://github.com/EvoSuite/evosuite>
- **Randoop**
  - *unit test generator for Java. It automatically creates unit tests for your classes, in JUnit format.*
  - <https://randoop.github.io/randoop>
