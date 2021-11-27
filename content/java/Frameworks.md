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
<br/><br/>
- **dropwizard**
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
  - <https://code.quarkus.io/> (wie spring-starter)
- **micronaut**
  - <http://micronaut.io/>
  - https://github.com/micronaut-projects/
  - https://github.com/micronaut-projects/micronaut-core *2600
  - https://github.com/micronaut-projects/micronaut-data
- **javalin**
  - <https://javalin.io/>
  - *very lightweight web framework*
  - <https://github.com/tipsy/javalin> *3100
- **light4j**
  - <https://github.com/networknt/light-4j> *2400
- **spark**
  - http://sparkjava.com/
  - "tiny", keine Annotationen, kein Xml, Kotlin & Java
  - https://github.com/perwendel/spark/ *8500
- **play**
  - https://www.playframework.com
  - https://github.com/playframework/playframework *11000
- **eclipse microprofile**
  - <https://start.microprofile.io/>
- **jooby**
  - <https://jooby.io/>
  - <https://github.com/jooby-project/jooby>
- **helidon**
  - <https://github.com/oracle/helidon> *1.8k
- **blade**
  - <https://github.com/lets-blade/blade> *5.2k


## Business Process
- **Flowable**
  - (asynchrone) Geschäftsprozesse abbilden
  - <https://www.flowable.org/>
  - <https://www.youtube.com/watch?v=43_OLrxU3so> (SpringDeveloper 1/2019)
- **Activiti**
  - <https://github.com/Activiti/Activiti>
- **camunda**
  - <https://github.com/camunda/camunda-bpm-platform>
  - zeebe
    - *Distributed Workflow Engine for Microservices Orchestration*
    - <https://github.com/camunda-cloud/zeebe>
- **Axon**
  - *for event-driven microservices*
  - <https://axoniq.io/>
- **Drools**
  - *rule engine, DMN engine and complex event processing (CEP) engine*
  - <https://github.com/kiegroup/drools> *3.7k


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
  - mit Spring: <https://reflectoring.io/spring-camel/>
- **Spring Integration**
  - [Spring/Integration](@note/Modul Integration.md)
  - ca. 20 Connectors
- **MuleESB**
  - Mule ist zusätzlich ein ESB = Enterprise Service Bus
  - closed source, CPAL-Lizenz
