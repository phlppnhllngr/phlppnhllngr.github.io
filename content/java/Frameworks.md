---
title: Frameworks
parent: Java
---

# Frameworks
- Techempower Benchmarks
  - [Ergebnisse](https://www.techempower.com/benchmarks/#section=data-r20&hw=ph&test=fortune&l=zik0vz-sf)
  - [github](https://github.com/TechEmpower/FrameworkBenchmarks/tree/master/frameworks/Java)
- [Quarkus vs Micronaut, 02/2020](https://www.reddit.com/r/java/comments/ey5szi/quarkus_vs_micronaut_a_feature_and_performance/)
- <https://web-frameworks-benchmark.netlify.app/result?l=java> <br/><br/>
- **dropwizard**
  - *framework for developing ops-friendly, high-performance, RESTful web services.*
  - *Dropwizard uses the Jetty HTTP library to embed an incredibly tuned HTTP server directly into your project. Instead of handing your application off to a complicated application server, Dropwizard projects have a main method which spins up an HTTP server.*
  - <https://www.dropwizard.io/>
- **vertx**
  - reactive
  - polyglot (jvm & js)
  - <https://vertx.io/>
  - <https://github.com/eclipse-vertx/vert.x> <img loading="lazy" src="https://img.shields.io/github/stars/eclipse-vertx/vert.x?style=flat-square">
- **vaadin**
  - <https://vaadin.com/>
- **quarkus**
  - <https://github.com/quarkusio/quarkus> <img loading="lazy" src="https://img.shields.io/github/stars/quarkusio/quarkus?style=flat-square">
  - *Container First framework for writing Java applications.*
  - <https://code.quarkus.io/> (wie spring-initializer)
- **javalin**
  - <https://javalin.io/>
  - *very lightweight web framework*
  - ```java
    import io.javalin.Javalin;

    public class HelloWorld {
        public static void main(String[] args) {
            Javalin app = Javalin.create().start(7070);
            app.get("/", ctx -> ctx.result("Hello World"));
        }
    }
    ```
  - <https://github.com/tipsy/javalin> <img loading="lazy" src="https://img.shields.io/github/stars/tipsy/javalin?style=flat-square">
- **light4j**
  - *A fast, lightweight and cloud-native microservices framework.*
  - Packaging: Jar
  - <https://github.com/networknt/light-4j> <img loading="lazy" src="https://img.shields.io/github/stars/networknt/light-4j?style=flat-square">
- **spark**
  - <http://sparkjava.com/>
  - "tiny", keine Annotationen, kein Xml, Kotlin & Java
  - ```java
    import static spark.Spark.*;

    public class HelloWorld {
        public static void main(String[] args) {
            get("/hello", (req, res) -> "Hello World");
        }
    }
    ```
  - <https://github.com/perwendel/spark/> <img loading="lazy" src="https://img.shields.io/github/stars/perwendel/spark?style=flat-square">
- **play**
  - *Integrated HTTP server (Akka HTTP or Netty)*
  - <https://www.playframework.com>
  - <https://github.com/playframework/playframework> <img loading="lazy" src="https://img.shields.io/github/stars/playframework/playframework?style=flat-square">
- **microprofile**
  - *aims to optimize Enterprise Java for the Microservices architecture*
  - *based on a subset of Jakarta EE WebProfile APIs*
  - *A MicroProfile application is portable and should run in any compliant MicroProfile runtime [Open Liberty, TomEE, ...]*
  - <https://microprofile.io/>
  - <https://www.baeldung.com/eclipse-microprofile>
  - <https://start.microprofile.io/>
- **jooby**
  - ```java
    import io.jooby.Jooby;

    public class App extends Jooby {

      {
        get("/", ctx -> "Welcome to Jooby!");
      }

      public static void main(String[] args) {
        runApp(args, App::new);
      }
    }
    ```
  - <https://jooby.io/>
  - <https://github.com/jooby-project/jooby> <img loading="lazy" src="https://img.shields.io/github/stars/jooby-project/jooby?style=flat-square">
- **helidon**
  - *cloud-native, open‑source set of Java libraries for writing microservices that run on a fast web core powered by Netty.*
  - *supports two programming models*
    - *Helidon MP: MicroProfile 3.3*
    - *Helidon SE: a small, functional style API.*
    - *In either case your application is just a Java SE program.*
  - *supports GraalVM Native Image so you can compile your Helidon application into a small-footprint native executable. Or you can package your application as a jlink image or a traditional application JAR.*
  - *Helidon requires Java 11 (or newer) and Maven.*
  - <https://helidon.io/>
  - <https://github.com/oracle/helidon> <img loading="lazy" src="https://img.shields.io/github/stars/oracle/helidon?style=flat-square">
  - Helido Nima (Níma)
    - *a Java 19 (currently early access) based implementation of a server designed for Java Virtual Threads (product of Project Loom)* 
    - *the first microservices framework based on virtual threads*
    - *The Helidon Níma web server intends to replace Netty in the Helidon ecosystem*
    - *will be a part of the next major Helidon release which is currently planned at the end of 2023*
    - *Prior to Helidon Nima, developers would have a choice to use Helidon MP and write JAX-RS applications, or if they needed a higher level of performance and throughput they could use Helidon SE and write reactive based services. However, the reactive based services are more complex to write, maintain, and debug.*
    - *Development with Helidon Níma is much easier as it follows a simplified programming model with (almost) unlimited virtual threading resources available. The JVM takes care of the optimizations.*
    - <https://medium.com/helidon/helidon-n%C3%ADma-helidon-on-virtual-threads-130bb2ea2088> 12.09.22
      - Features
      - Getting Started 
- **blade**
  - *Based on Java8 + Netty4 to create a lightweight, high-performance, simple and elegant Web framework*
  - ```java
    public static void main(String[] args) {
      Blade.of().get("/", ctx -> ctx.text("Hello Blade")).start();
    }
    ```
  - <https://github.com/lets-blade/blade> <img loading="lazy" src="https://img.shields.io/github/stars/lets-blade/blade?style=flat-square">
- **Armeria**
  - *your go-to microservice framework for any situation. You can build any type of microservice leveraging your favorite technologies, including gRPC, Thrift, Kotlin, Retrofit, Reactive Streams, Spring Boot and Dropwizard.*
  - <https://github.com/line/armeria> <img loading="lazy" src="https://img.shields.io/github/stars/line/armeria?style=flat-square">
- **restlet**
  - *REST API framework for Java*
  - *powerful routing and filtering capabilities, unified client and server Java API*
  - <https://github.com/restlet/restlet-framework-java> <img loading="lazy" src="https://img.shields.io/github/stars/restlet/restlet-framework-java?style=flat-square">
- **ratpack**
  - *Lean & powerful HTTP apps* 
  - *built on the Netty event-driven networking engine* 
  - <https://github.com/ratpack/ratpack> <img loading="lazy" src="https://img.shields.io/github/stars/ratpack/ratpack?style=flat-square">
- **RestExpress**
  - *Uses Netty for HTTP, Jackson for JSON, Metrics for metrics, properties files for configuration.*
  - *Sub-projects and plugins enable, NoSQL, Swagger, Auth0, HAL integration, etc.* 
  - <https://github.com/RestExpress/RestExpress> <img loading="lazy" src="https://img.shields.io/github/stars/RestExpress/RestExpress?style=flat-square">
- **ActiveJ**
  - *asynchronous IO with the efficient event loop, NIO, promises, streaming, and CSP. Alternative to Netty, RxJava, Akka, and others* 
  - <https://github.com/activej/activej> <img loading="lazy" src="https://img.shields.io/github/stars/activej/activej?style=flat-square">


## Enterprise Integration
<details>
    <summary>Patterns</summary>
    <img loading="lazy" src="https://static.packt-cdn.com/products/9781787126992/graphics/Insert-Image_03_10.png"/>
</details>

- **Apache Camel**
  - <http://camel.apache.org/>
  - hohe Anzahl an Connectors (~200)
  - *Camel empowers you to define routing and mediation rules in a variety of domain-specific languages, including a Java-based Fluent API, Spring or ...
Apache Camel uses URIs to work directly with any kind of Transport or messaging model such as HTTP, JMS, ..., as well as pluggable Components and Data Format options. Apache Camel is a small library with minimal dependencies for easy embedding in any Java application. Apache Camel lets you work with the same API regardless which kind of Transport is used - so learn the API once and you can interact with all the Components provided out-of-box.*
  - Übersicht Komponenten: <https://github.com/apache/camel/blob/master/components/readme.adoc>
  - mit Spring: <https://reflectoring.io/spring-camel/>, [Spring Tips: Apache Camel](https://www.youtube.com/watch?v=-KupcZ3bA-Y)
- **Spring Integration**
  - [Spring/Integration](@note/Modul Integration.md)
  - ca. 20 Connectors
- **MuleESB**
  - Mule ist zusätzlich ein ESB = Enterprise Service Bus
  - closed source, CPAL-Lizenz
- **Alpakka** -> Java/Libs/Async/Reactive 
