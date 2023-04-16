---
title: Message queue
parent: Diverses
---

# Message queue
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
  - impl AMQP
  - *not a JMS provider but includes a plugin needed to support the JMS Queue and Topic messaging models*
  - <https://www.rabbitmq.com>
  - <https://github.com/rabbitmq>
  - [HN - SQL Maxis: Why We Ditched RabbitMQ and Replaced It with a Postgres Queue](https://news.ycombinator.com/item?id=35526846)
- **ActiveMQ**
  - standalone oder embedded
  - JMS Provider
  - *supports a relatively large number of transport protocols, including OpenWire, STOMP, MQTT, AMQP, REST, and WebSockets.*
  - <https://en.wikipedia.org/wiki/Apache_ActiveMQ>
- **ActiveMQ Artemis**
  - *The overall objective for working toward feature parity between ActiveMQ 5.x and Artemis is for Artemis to eventually become ActiveMQ 6.x."*
  - *a more modern implementation because, ironically, it has a smaller feature set.*
  - <https://github.com/apache/activemq-artemis>
  - <https://developers.redhat.com/articles/2021/06/30/implementing-apache-activemq-style-broker-meshes-apache-artemis>
  - <https://www.predic8.de/apache-artemis-vergleich-kafka-activemq.htm> (2018)
    - *Web Konsole für das Management des Artemis wird von einem integrierten Jetty Web Server bereitgestellt*
    - *Für das Zwischenspeichern von Nachrichten bietet Artemis die zwei Optionen: Ablage der Nachrichten in einer Dateisystem oder über JDBC in einer Datenbank.*
    - *Mit Artemis lassen sich verschiedene Cluster Konfigurationen und Topologien realisieren um Lastverteilung und/oder Ausfallsicherheit zu erreichen.*
    - Vergleich mit ActiveMQ, Kafka
- **RocketMQ**
  - *distributed messaging and streaming platform* 
  - *Multiple messaging protocols like gRPC, MQTT, JMS and OpenMessaging* 
  - <https://github.com/apache/rocketmq>
- **Pulsar**
  - *distributed pub-sub messaging platform*
  - <https://github.com/apache/pulsar>

## Vergleiche
- <https://www.conduktor.io/blog/comparing-apache-kafka-activemq-and-rabbitmq/>

