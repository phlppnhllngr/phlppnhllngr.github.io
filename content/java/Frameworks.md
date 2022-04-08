---
tags: [Notebooks/Java]
title: Frameworks
created: '2019-02-14T20:27:43.061Z'
modified: '2021-08-15T11:55:31.908Z'
parent: Java
---

# Frameworks
- [Techempower Benchmarks](https://www.techempower.com/benchmarks/#section=data-r20&hw=ph&test=fortune&l=zik0vz-sf)
- [Quarkus vs Micronaut, 02/2020](https://www.reddit.com/r/java/comments/ey5szi/quarkus_vs_micronaut_a_feature_and_performance/) <br/><br/>
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
- **micronaut**
  - <http://micronaut.io/>
  - projects
    - <https://github.com/micronaut-projects/>
    - core
      - <https://github.com/micronaut-projects/micronaut-core> *2600
    - data
      - *database access toolkit that uses Ahead of Time (AoT) compilation to pre-compute queries for repository interfaces that are then executed by a thin, lightweight runtime layer.*
      - <https://github.com/micronaut-projects/micronaut-data>
    - servlet
      - *Provides integration between Micronaut and the Servlet API*
      - *provides support for replacing the Netty-based HTTP server that comes with the Micronaut framework with either Jetty, Tomcat, or Undertow*
      - *for users who*
        - *want to use Micronaut but the target deployment environment is based on Servlets*
        - *prefer the thread per connection model of the Servlet API over the Event Loop model provided by the default Netty-based HTTP server*
        - *have existing Servlets and/or Filters that they wish to combine with Micronaut.*
      - wenig Docs
      - <https://micronaut-projects.github.io/micronaut-servlet/latest/guide/>
      - <https://github.com/micronaut-projects/micronaut-servlet>
    - http-client
      - *By default, Micronaut’s HTTP client is configured to support HTTP 1.1. To enable support for HTTP/2, set the supported HTTP version in configuration*
      - <https://guides.micronaut.io/latest/micronaut-http-client.html>
    - maven-plugin
      - <https://github.com/micronaut-projects/micronaut-maven-plugin>
  - <https://micronaut.io/launch> (wie Spring initializer)
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


## Business Process
- BPMN
  - Busniness Process Model and Notation
  - *standard for business process modeling that provides a graphical notation for specifying business processes in a Business Process Diagram (BPD),[3] based on a flowcharting technique very similar to activity diagrams from Unified Modeling Language (UML)*
  - *BPMN has been maintained by the Object Management Group (OMG)*
- **Flowable**
  - (asynchrone) Geschäftsprozesse abbilden
  - <https://www.flowable.org/>
  - <https://www.youtube.com/watch?v=43_OLrxU3so> (SpringDeveloper 1/2019)
- **Activiti**
  - <https://github.com/Activiti/Activiti>
- **Axon**
  - *for event-driven microservices*
  - <https://axoniq.io/>
- **Drools**
  - *rule engine, DMN engine and complex event processing (CEP) engine*
  - <https://github.com/kiegroup/drools> *3.7k

### Camunda
- basiert auf Activiti

#### Camunda Platform
- *Components: Camunda Platform provides a rich set of components centered around the BPM lifecycle.*
  - *Process Implementation and Execution*
    - *Camunda Engine - The core component responsible for executing BPMN 2.0 processes.*
    - *REST API - The REST API provides remote access to running processes.*
    - *Spring, CDI Integration - Programming model integration that allows developers to write Java Applications that interact with running processes.*
  - *Process Design*
    - *Camunda Modeler - A standalone desktop application that allows business users and developers to design & configure processes.*
  - *Process Operations*
    - *Camunda Engine - JMX and advanced Runtime Container Integration for process engine monitoring.*
    - *Camunda Cockpit - Web application tool for process operations.*
    - *Camunda Admin - Web application for managing users, groups, and their access permissions.*
  - *Human Task Management*
    - *Camunda Tasklist - Web application for managing and completing user tasks in the context of processes.*
  - *And there's more...*
    - [bpmn.io](https://bpmn.io) - *Toolkits for BPMN, CMMN, and DMN in JavaScript (rendering, modeling)*
    - [Community Extensions](https://docs.camunda.org/manual/current/introduction/extensions/) - *Extensions on top of Camunda Platform provided and maintained by our great open source community*
- Architektur
  - *can be deployed in different scenarios*
  - Embedded Process Engine
    - *In this case, the process engine is added as an application library to a custom application. This way, the process engine can easily be started and stopped with the application lifecycle.* 
    - Spring Boot App
      - <https://docs.camunda.org/manual/latest/user-guide/spring-boot-integration/> 
  - Shared, Container-Managed Process Engine
    - *In this case, the process engine is started inside the runtime container (Servlet Container, Application Server, …). The process engine is provided as a container service and can be shared by all applications deployed inside the container.*
    - <https://docs.camunda.org/manual/latest/installation/full/>
    - Tomcat
    - Wildfly
    - WebSphere
      - <https://docs.camunda.org/manual/latest/installation/full/was/> 
    - WebLogic
  - Standalone (Remote) Process Engine Server
    - *In this case, the process engine is provided as a network service. Different applications running on the network can interact with the process engine through a remote communication channel. The easiest way to make the process engine accessible remotely is to use the built-in REST API.* 
  - <https://docs.camunda.org/manual/current/introduction/architecture/> 
- Distributionen
  - Platform Run (zip)
    - *a pre-packaged, lightweight distribution of the Camunda Platform. Camunda Platform Run is easy to configure and does not require Java knowledge.* 
    - Camunda Open Source Community Edition
    - Wrapper um Spring Boot mit embedded Tomcat
    - <https://docs.camunda.org/manual/current/user-guide/camunda-bpm-run/>
    - [Tutorial: How to Get Started With Camunda Run](https://www.youtube.com/watch?v=l-sCUKQZ44s&list=PLJG25HlmvsOUnCziyJBWzcNh7RM5quTmv)
  - Tomcat
  - Docker
    - Camunda Platform Run
    - Camunda Platform (Tomcat)
    - Enterprise Edition 
    - <https://docs.camunda.org/manual/current/installation/docker/> 
  - Platform Initializer
    - Generator für Spring Boot Projekt  
    - <https://start.camunda.com>
- <https://docs.camunda.org/manual/current>
- <https://github.com/camunda/camunda-bpm-platform>

#### Camunda Cloud
- <https://docs.camunda.io/>
- Komponenten (<https://docs.camunda.io/docs/components/>)
  - Zeebe
    - *the process automation engine powering Camunda Cloud*
    - *provides visibility into and control over business processes that span multiple microservices*
    - <https://github.com/camunda/zeebe>
    - <https://github.com/camunda-community-hub/spring-zeebe> (Spring Boot Starter)
  - ...  
- self-managed
  - *Self-Managed is free forever with non-production usage of Operate, Tasklist, and Optimize* [1] 
  - <https://docs.camunda.io/docs/self-managed/overview/>
  - 1: <https://camunda.com/platform/faq>
- Migration Guide
  - <https://docs.camunda.io/docs/guides/migrating-from-Camunda-Platform/>
  - *the workflow engine in Camunda Cloud is always a remote resource for your application, while the embedded engine mode is not supported*

#### Camunda Modeler
- <https://camunda.com/products/camunda-platform/modeler/>


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
