---
title: Event queue
parent: Diverses
---

# Event queue
- **Apache Kafka**
  - *Kafka is different from JMS systems such as ActiveMQ. Kafka has less features than ActiveMQ, as the stress has been put on performances.*
  - *Kafka uses its own non-standard protocol and clients*
  - *Apache Kafka focuses on a pub/sub model, maintaining a separate log/topic from which consumers read from offsets. Kafka is also built for the cloud, with high-throughput a core consideration.*
  - *The chief difference with kafka is storage, <mark>it saves data ... Normally in message queues, the messages are removed after subscribers have confirmed their receipt</mark>.*
  - *Another thing different about kafka is that the topics are ordered (by date they were added). Not all message queues guarantee this.*
  - **UI for Apache Kafka**
    - <https://github.com/provectus/kafka-ui>
- **chronicle-queue**
  - *Chronicle Queue is designed to out-perform its rivals such as Kafka.*
  - <https://github.com/OpenHFT/Chronicle-Queue>
