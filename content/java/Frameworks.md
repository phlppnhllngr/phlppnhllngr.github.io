---
tags: [Notebooks/Java]
title: Frameworks
created: '2019-02-14T20:27:43.061Z'
modified: '2021-08-15T11:55:31.908Z'
parent: Java
---

# Frameworks
- [Techempower Benchmarks](https://www.techempower.com/benchmarks/#section=data-r20&hw=ph&test=fortune&l=zik0vz-sf)
- [Quarkus vs Micronaut, 02/2020](https://www.reddit.com/r/java/comments/ey5szi/quarkus_vs_micronaut_a_feature_and_performance/)
- <https://web-frameworks-benchmark.netlify.app/result?l=java> <br/><br/>
- **dropwizard**
  - *framework for developing ops-friendly, high-performance, RESTful web services.*
  - *Dropwizard uses the Jetty HTTP library to embed an incredibly tuned HTTP server directly into your project. Instead of handing your application off to a complicated application server, Dropwizard projects have a main method which spins up an HTTP server.*
  - <https://www.dropwizard.io/>
- **vertx**
  - <https://vertx.io/>
  - <https://github.com/eclipse-vertx/vert.x> *9800
  - sehr performant
  - polyglot (jvm & js)
- **vaadin**
  - <https://vaadin.com/>
- **quarkus**
  - <https://github.com/quarkusio/quarkus> *4.2k
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
  - <https://github.com/tipsy/javalin> *3100
- **light4j**
  - *A fast, lightweight and cloud-native microservices framework.*
  - Packaging: Jar
  - <https://github.com/networknt/light-4j> *3.4k
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
  - <https://github.com/perwendel/spark/> *8500
- **play**
  - *Integrated HTTP server (Akka HTTP or Netty)*
  - <https://www.playframework.com>
  - <https://github.com/playframework/playframework> *11000
- **eclipse microprofile**
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
  - <https://github.com/jooby-project/jooby> *1.4k
- **helidon**
  - *cloud-native, open‑source set of Java libraries for writing microservices that run on a fast web core powered by Netty.*
  - *supports two programming models*
    - *Helidon MP: MicroProfile 3.3*
    - *Helidon SE: a small, functional style API.*
    - *In either case your application is just a Java SE program.*
  - *supports GraalVM Native Image so you can compile your Helidon application into a small-footprint native executable. Or you can package your application as a jlink image or a traditional application JAR.*
  - *Helidon requires Java 11 (or newer) and Maven.*
  - <https://helidon.io/>
  - <https://github.com/oracle/helidon> *1.8k
- **blade**
  - *Based on Java8 + Netty4 to create a lightweight, high-performance, simple and elegant Web framework*
  - ```java
    public static void main(String[] args) {
      Blade.of().get("/", ctx -> ctx.text("Hello Blade")).start();
    }
    ```
  - <https://github.com/lets-blade/blade> *5.2k
- **Armeria**
  - *your go-to microservice framework for any situation. You can build any type of microservice leveraging your favorite technologies, including gRPC, Thrift, Kotlin, Retrofit, Reactive Streams, Spring Boot and Dropwizard.*
  - <https://github.com/line/armeria> *3.5k
- **restlet**
  - *REST API framework for Java*
  - *powerful routing and filtering capabilities, unified client and server Java API*
  - <https://github.com/restlet/restlet-framework-java>
- **ratpack**
  - *Lean & powerful HTTP apps* 
  - *built on the Netty event-driven networking engine* 
  - <https://github.com/ratpack/ratpack> 


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
