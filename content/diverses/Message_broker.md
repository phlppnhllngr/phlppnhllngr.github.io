---
title: Message Broker
parent: Diverses
---

# Message Broker
- **AsyncAPI**
  - *allows you to create machine-readable definitions of your asynchronous APIs* 
  - <https://www.asyncapi.com/> 

## Tools
- **Apache Kafka**
  - *Kafka is different from JMS systems such as ActiveMQ. Kafka has less features than ActiveMQ, as the stress has been put on performances.*
  - *Kafka uses its own non-standard protocol and clients*
  - *Apache Kafka focuses on a pub/sub model, maintaining a separate log/topic from which consumers read from offsets. Kafka is also built for the cloud, with high-throughput a core consideration.*
  - *The chief difference with kafka is storage, <mark>it saves data ... Normally in message queues, the messages are removed after subscribers have confirmed their receipt</mark>.*
  - *Another thing different about kafka is that the topics are ordered (by date they were added). Not all message queues guarantee this.*
  - <https://old.reddit.com/r/programming/comments/11pedkt/supercharge_your_kafka_clusters_with_consumer/.compact>
  - **UI for Apache Kafka**
    - <https://github.com/provectus/kafka-ui>
- **chronicle-queue**
  - *Chronicle Queue is designed to out-perform its rivals such as Kafka.*
  - <https://github.com/OpenHFT/Chronicle-Queue>
- **RabbitMQ**
  - *It supports: AMQP 0-9-1, AMQP 1.0, RabbitMQ Stream Protocol, MQTT 3.1.1, STOMP 1.0 through 1.2*
  - *not a JMS provider but includes a plugin needed to support the JMS Queue and Topic messaging models*
  - *Message Durability: Messages are not lost once stored in RabbitMQ.*
  - *Message Acknowledgements: Consumers send acknowledgments to producers after successfully consuming a message.*
  - <https://www.rabbitmq.com>
  - <https://github.com/rabbitmq>
  - <https://github.com/rabbitmq/rabbitmq-server> <img loading="lazy" src="https://img.shields.io/github/stars/rabbitmq/rabbitmq-server?style=flat-square"/>
  - <https://github.com/rabbitmq/rabbitmq-java-client> <img loading="lazy" src="https://img.shields.io/github/stars/rabbitmq/rabbitmq-java-client?style=flat-square"/>
  - [HN - SQL Maxis: Why We Ditched RabbitMQ and Replaced It with a Postgres Queue](https://news.ycombinator.com/item?id=35526846)
- **ActiveMQ**
  - standalone oder embedded
  - JMS Provider
  - *supports a relatively large number of transport protocols, including OpenWire, STOMP, MQTT, AMQP, REST, and WebSockets.*
  - <https://en.wikipedia.org/wiki/Apache_ActiveMQ>
- **ActiveMQ Artemis**
  - *The overall objective for working toward feature parity between ActiveMQ 5.x and Artemis is for Artemis to eventually become ActiveMQ 6.x."*
  - *a more modern implementation because, ironically, it has a smaller feature set.*
  - <https://github.com/apache/activemq-artemis> <img loading="lazy" src="https://img.shields.io/github/stars/apache/activemq-artemis?style=flat-square"/>
  - <https://developers.redhat.com/articles/2021/06/30/implementing-apache-activemq-style-broker-meshes-apache-artemis>
  - <https://www.predic8.de/apache-artemis-vergleich-kafka-activemq.htm> (2018)
    - *Web Konsole für das Management des Artemis wird von einem integrierten Jetty Web Server bereitgestellt*
    - *Für das Zwischenspeichern von Nachrichten bietet Artemis die zwei Optionen: Ablage der Nachrichten in einer Dateisystem oder über JDBC in einer Datenbank.*
    - *Mit Artemis lassen sich verschiedene Cluster Konfigurationen und Topologien realisieren um Lastverteilung und/oder Ausfallsicherheit zu erreichen.*
    - Vergleich mit ActiveMQ, Kafka
- **RocketMQ**
  - *distributed messaging and streaming platform* 
  - *Multiple messaging protocols like gRPC, MQTT, JMS and OpenMessaging* 
  - <https://github.com/apache/rocketmq> <img loading="lazy" src="https://img.shields.io/github/stars/apache/rocketmq?style=flat-square"/>
- **Pulsar**
  - *distributed pub-sub messaging platform*
  - <https://github.com/apache/pulsar>
- **Redis**
  - *that while Redis can be used as a message queue, it’s not a traditional message queue system like RabbitMQ or Apache Kafka* 
  - ~~*does not provide advanced features such as publish-subscribe, message acknowledgment, or message persistence* ~~
  - <https://redis.io/docs/manual/pubsub/>
    - *Messages sent by other clients to these channels will be pushed by Redis to all the subscribed clients. Subscribers receive the messages in the order that the messages are published.*
  - <https://www.educba.com/rabbitmq-vs-redis/>
    - *It supports only the pub-sub mechanism.*
    - *It doesn’t guarantee the delivery of each message.*
  - *Mostly, RabbitMQ outperforms Redis and guarantees message delivery with the help of message durability and acknowledgments*
- **BullMQ**
  - *Message Queue and Batch processing for NodeJS and Python based on Redis* 
  - <https://github.com/taskforcesh/bullmq> 
- **NATS**
  - *messaging system for cloud native applications, IoT messaging, and microservices architectures* 
  - *the basic NATS platform is a simple pub-sub transport system that offers only TCP reliability* 
  - *NATS JetStream offers persistence with "at-least-once" and "exactly-once" (within a time window) delivery.*
  - *NATS offers three primary modes of message exchange.*
    - *Publish/Subscribe semantics delivers messages to all subscribers of a topic.*
    - *Request/Reply messaging sends requests via topics and routes responses back to the requestor.*
    - *Subscribers can also join message queue groups when they subscribe to a topic. Messages sent to the associated topic are only delivered to one subscriber in the queue group.*
  - Clients für viele Sprachen, u. A. Java
  - <https://nats.io/>
  - <https://www.baeldung.com/nats-java-client>
  - <https://news.ycombinator.com/item?id=36820544>
- **Postgres**
  - LISTEN/NOTIFY
  - <https://www.baeldung.com/spring-postgresql-message-broker>
  - <https://gist.github.com/cpursley/c8fb81fe8a7e5df038158bdfe0f06dbb#message-queues>
  - <https://leontrolski.github.io/postgres-as-queue.html>
  - HN
    - [Choose Postgres queue technology](https://news.ycombinator.com/item?id=37636841)
    - [Postgres as queue, 02/2024](https://news.ycombinator.com/item?id=39315833)
    - [Show HN: PgQueuer – Transform PostgreSQL into a Job Queue](https://news.ycombinator.com/item?id=41284703)
  - <https://github.com/pgmq/pgmq> - *Like AWS SQS and RSMQ but on Postgres.*
- **BlazingMQ**
  - <https://github.com/bloomberg/blazingmq> <img loading="lazy" src="https://img.shields.io/github/stars/bloomberg/blazingmq?style=flat-square"/>
  - <https://bloomberg.github.io/blazingmq/docs/introduction/comparison/> 

## Vergleiche
- <https://www.conduktor.io/blog/comparing-apache-kafka-activemq-and-rabbitmq/>
- <https://docs.nats.io/nats-concepts/overview/compare-nats>
- [HN - RabbitMQ vs Kafka, Okt 2023](https://news.ycombinator.com/item?id=37574552)



