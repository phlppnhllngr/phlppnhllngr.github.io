---
title: JMS
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
-> Diverses/Message queue (RabbitMQ, ActiveMQ, RocketMQ)
- Amazon SQS JMS Client
- Websphere MQ (standalone oder embedded)
