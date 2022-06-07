---
tags: [Notebooks/Java]
title: JMS
created: '2019-02-05T12:06:23.052Z'
modified: '2021-07-03T14:06:39.914Z'
grand_parent: Java
parent: Enterprise
---

# JMS
- *"Jakarta Messaging", formerly "Java Message Service", is an API that provides the facility to create, send and read messages. It provides loosely coupled, reliable and asynchronous communication.*
- Current version: 3.0 (11/2020)
- *two types of messaging domains in JMS*
  - *Point-to-Point Messaging Domain*
    - *one message is delivered to <mark>one receiver only</mark>*
    - *<mark>Queue</mark> is used as a message oriented middleware (MOM)*
    - *The Queue is responsible to hold the message until receiver is ready.*
    - *Ist kein Empfänger verfügbar, kann die Nachricht optional gespeichert werden und potentielle Empfänger können sie jederzeit später abholen.*
  - *Publisher/Subscriber Messaging Domain*
    - *one message is delivered to all the <mark>subscribers</mark> (Broadcasting)*
    - *<mark>Topic</mark> is used as a message oriented middleware that is responsible to hold and deliver messages.*
    - *Wird die Nachricht nicht konsumiert, weil kein Empfänger sich an das Topic angemeldet hat, dann ist dies unerheblich.*
- <https://en.wikipedia.org/wiki/Jakarta_Messaging>
- <https://www.javatpoint.com/jms-tutorial>

## Providers
- RabbitMQ
   - <https://www.rabbitmq.com/>
   - <https://github.com/rabbitmq> 
- ActiveMQ
  - standalone oder embedded
  - *There's another broker under the ActiveMQ umbrella code-named Artemis. (...) was donated from the JBoss community to the Apache ActiveMQ community in 2015. Artemis is the "next generation" broker from ActiveMQ and will ultimately become the next major version of ActiveMQ.*
  - <https://en.wikipedia.org/wiki/Apache_ActiveMQ> 
- Amazon SQS JMS Client
- Websphere MQ (standalone oder embedded)
- RocketMQ
  - *distributed messaging and streaming platform* 
  - *Multiple messaging protocols like gRPC, MQTT, JMS and OpenMessaging* 
  - <https://github.com/apache/rocketmq> 
