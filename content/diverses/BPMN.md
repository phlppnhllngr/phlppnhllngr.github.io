---
title: BPMN
parent: Diverses
---

# BPMN
- Business Process Model and Notation
- *standard for business process modeling that provides a graphical notation for specifying business processes in a Business Process Diagram (BPD),[3] based on a flowcharting technique very similar to activity diagrams from Unified Modeling Language (UML)*
- *BPMN has been maintained by the Object Management Group (OMG)*

## Frameworks & Tools
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
- **bpmn-js**
  - *View and edit BPMN 2.0 diagrams in the browser.*
  - <https://github.com/bpmn-io/bpmn-js>

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