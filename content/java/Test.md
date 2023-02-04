---
title: Test
parent: Java
---

# Test
- <https://phauer.com/2019/modern-best-practices-testing-java>
- <https://github.com/akullpp/awesome-java#testing>


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
- **To String Verifier**
  - *provides an easy and convenient way to test the toString method on your class*
  - *It is very easy to add a new field to your class and forget to update the toString method. Without tests in place, you won’t know something is missing until you are sitting looking through logs or debugging your application and by that time its already too late.*
  - <https://github.com/jparams/to-string-verifier>


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
  - <https://github.com/jmockit/jmockit1>
- **system rules**
  - "mocks" java.lang.System
  - <https://www.baeldung.com/java-system-rules-junit>
- **system lambda**
  - *collection of functions for testing code that uses java.lang.System* 
  - <https://github.com/stefanbirkner/system-lambda> 
- <u>File sytem</u>
  - **jimfs**
    - *An in-memory file system for Java 7+*
    - <https://github.com/google/jimfs>
  - **memoryfilesystem**
    - <https://github.com/marschall/memoryfilesystem>
  - **Commons Virtual File System**
    - <https://commons.apache.org/proper/commons-vfs/index.html> 
- <u>HTTP/API</u>
  - **wiremock**
    - mit Junit4-Rule
    - <http://wiremock.org/docs/getting-started>
  - **pact**
    - mit Junit-Rule
- <u>Datum & Zeit</u>
  - <http://blog.tremblay.pro/2021/01/mocking-clock.html>
- <u>Email</u>
  - **Wiser**
    - für jakarta.mail 
    - <https://www.youtube.com/watch?v=JVPHSdHViMg&t=325s>  


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
- **Data Faker**
  - *a modern and more up to date port of Javafaker*
  - <https://www.reddit.com/r/java/comments/rvuyf7/datafaker_an_alternative_to_using_production_data/>
  - <https://github.com/datafaker-net/datafaker/>
- **beanmother**
  - generiert Zufallsobjekte anhand yaml-template
  - <https://github.com/keepcosmos/beanmother>
- **jqwik**
  - <https://jqwik.net>
- **Instancio**
  - *library for creating fully populated objects for your unit tests*
  - *Instead of manually setting up test data:*
    ```java
    Address address  = new Address();
    address.setStreet("street");
    address.setCity("city");
    //...
    Person person = new Person();
    person.setFirstName("first-name");
    person.setLastName("last-name");
    person.setAge(22);
    person.setGender(Gender.MALE);
    person.setAddress(address);
    //...
    ```
    *You can simply do the following:*
    ```java
    Person person = Instancio.create(Person.class);
    ```
    *This one-liner returns a fully-populated person, including nested objects and collections. The object is populated with random data that can be reproduced in case of test failure.*
  - <https://github.com/instancio/instancio/>
- **Fixture Monkey**
  - *generate test instances including edge cases automatically*
  - <https://github.com/naver/fixture-monkey>


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
- **AssertJ-DB**
  - *provides assertions to test values in a database*
  - `assertThat(table).row(1).value().isEqualTo("foo")`
  - <https://github.com/assertj/assertj-db>


## Coverage
- **JaCoCo**
  - <https://www.eclemma.org/jacoco>


## Benchmarks, Performance
- → Junit/JfrUnit
- **JMH**
  - <http://openjdk.java.net/projects/code-tools/jmh>
  - <https://github.com/openjdk/jmh/tree/master/jmh-samples>
  - <https://github.com/Valloric/jmh-playground>
    - *Setting [jmh] up (especially with Gradle) and learning how to use it can be a bit difficult; hopefully this repo makes this process easier for others.*
    - *The absolute best way to learn how to use JMH is to read through the official JMH samples. All of them are included in this repo.*
    - *Does NOT use the jmh-gradle-plugin which is confusing, brittle and difficult to use correctly.*
    - *Benchmarking pitfalls to be aware of. JMH tips & tricks*
  - <https://www.retit.de/continuous-benchmarking-with-jmh-and-junit>
  - <https://www.baeldung.com/java-microbenchmark-harness>
  - <https://medium.com/javarevisited/understanding-java-microbenchmark-harness-or-jmh-tool-5b9b90ccbe8d> (03/2021)
    - Maven
    - org.openjdk.jmh.runner.options.Options, org.openjdk.jmh.runner.Runner 
    - Benchmark modes (`@BenchmarkMode(value = Mode)`)
      - Throughput/thrpt (default)
        - *This is used to measure the number of times a method is executed at a certain time. Normally its output unit is the number of outputs per second.* 
      - AverageTime/avgt
        - *The AverageTime measures the average time it takes for your benchmark method to be executed* 
      - SampleTime/sample
        - *Runs by continuously calling methods, and randomly samples the time needed for the call. This mode automatically adjusts the sampling frequency but may omit some pauses which missed the sampling measurement. This mode is time-based, and it will run until the iteration time expires.* 
      - SingleShotTime/ss
        - *This measures the time for a single operation. Use this when you want to account for the cold start time also.* 
      - All/all
    - Fork (`@Fork(value = int, jvmArgs = String[], warmups = int)`)
      - *It is also called a trail. A trail contains a set of warmups and iterations.*
      - *By default JHM forks a new java process for each trial (set of iterations). This is required to defend the test from previously collected “profiles” – information about other loaded classes and their execution information. For example, if you have 2 classes implementing the same interface and test the performance of both of them, then the first implementation (in order of testing) is likely to be faster than the second one (in the same JVM), because JIT replaces direct method calls to the first implementation with interface method calls after discovering the second implementation.*
      - *The JVM optimizes an application by creating a profile of the application's behavior. The fork is created to reset this profile. Otherwise, running:*
      ```
      benchmarkFoo();
      benchmarkBar();
      ```
      *might result in different measurements than*
      ```
      benchmarkBar();
      benchmarkFoo();
      ```
      - *This annotation may be put at Benchmark method to have effect on that method only, or at the enclosing class instance to have the effect over all Benchmark methods in the class. This annotation may be overridden with the runtime options.* 
    - Warmup (`@Warmup(iterations = int, time = int, timeUnit = TimeUnit)`) 
      - *JMH roughly does few runs of a given benchmark but it discards the results. That constitutes the warmup phase, and its role is to allow the JVM to perform any class loading, compilation to native code, and caching steps it would normally do in a long-running application before starting to collect actual results. it is recommended that the benchmark is run with some warmups then only it executes the actual run.*
      - Default: 5 iterations
    - Iteration (`@Measurement(iterations = int, time = int, timeUnit = TimeUnit)`)
    - State (`@State(value = Scope)`)
      - *Suppose you want to initialize some variables that your benchmark code needs, but which you do not want to be part of the code your benchmark measures. Such variables are called “state” variables. State variables are declared in special state classes, and an instance of that state class can then be provided as a parameter to the benchmark method.*
    - Setup (`@Setup`) & TearDown (`@TearDown`)
      - *The @Setup annotation tells JMH that this method should be called to setup the state object before it is passed to the benchmark method. The @TearDown annotation tells JMH that this method should be called to clean up ("tear down") the state object after the benchmark has been executed.*
    - Parameters (`@Param(value = String[])`)  
    - Output (`@OutputTimeUnit(value = TimeUnit)`)
  - <https://mkyong.com/java/java-jmh-benchmark-tutorial/>
    - *There are two ways to run the JMH benchmark, uses Maven or run it via a JMH Runner class directly.*  
- **caliper**
  - *tool for measuring Java code performance, primarily focused on microbenchmarks.* 
  - <https://github.com/google/caliper> *620
  - <https://github.com/google/caliper/wiki>
  - <https://github.com/google/caliper/tree/master/caliper-examples/src/main/java>
- **quickperf**
  - *quickly evaluate and improve some performance-related*
  - Annotationen für `@Test`-Methoden (z. B. @MeasureHeapAllocation, @ExpectSelect (sql))
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
- **jQAssistant**
  - *allows the definition and validation of project specific rules on a structural level*
  - *Example use cases:*
    - *Enforce naming conventions, e.g. EJBs, JPA entities, test classes, packages, Maven modules etc.*
    - *Validate dependencies between modules of your project*
    - *Separate API and implementation packages*
    - *Detect common problems like cyclic dependencies or tests without assertions*
  - <https://jqassistant.org/>

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
- **spock**
  - <https://github.com/spockframework/spock> 


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
