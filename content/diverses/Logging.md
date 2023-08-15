---
title: Logging
parent: Diverses
---

# Logging
- → Devops/APM, Tracing
- <https://www.reddit.com/r/programming/comments/nq7l8v/logging_is_important>
- [zen and the art of logging](https://www.lelanthran.com/chap10/content.html) - 2023-08-02
- *One pattern I've used before - in a Java app with an RDBMS, create an error table, and every unexpected Java exception gets logged to that table. Then have a system to match problems in that table to known errors, or flag new ones for analysis.*
- *Request logging should be done by an application gateway; it will do a more honest job of it. In applications, don't log anything except:*
  - *application startup and shutdown (at INFO level)*
  - *occurrences that indicate a bug in the system logging (at ERROR level)*
  - *occurrences that indicate a bug in another of your systems (at WARN level)*
- *The answer to "but don't we want to know when..." arguments should always be, "If it's that important, emit it as a metric or store it in an appropriate datastore." Anything logged at WARN or ERROR should be something that can be addressed by fixing code*

## Structured Logging
- <https://www.innoq.com/en/blog/structured-logging/>

## Log Viewer/Aggregator
- **LogNavigator**
  - <https://github.com/fbaligand/lognavigator> ⭐15 (21.3.19: letzter Commit vor 2 Jahren)
  - *Navigate into your logs with the comfort of a web interface. LogNavigator is a web application, made in java, which lets you browse your logs, wherever they are.*
- **log.io**
  - *Real-time log monitoring in your browser*
  - *Harvesters watch log files for changes, send new log messages to the server via TCP, which broadcasts to web clients via socket.io.*
  - node_module
  - <http://logio.org/>
  - <https://github.com/NarrativeScience/Log.io> ⭐4000
- **graylog**
  - *Free and open source log management*
  - gelf = Graylog Extended Log Format
  - <https://www.graylog.org/>
  - <https://github.com/Graylog2/graylog2-server> ⭐5.8k
  - Docker: <https://docs.graylog.org/en/latest/pages/installation/docker.html>
  - Zuerst muss man in der Admin-UI unter "system" ein oder mehrere "inputs" anlegen. Danach sind die empfangenen Messages unter "all messages" oder in einem der definierten "streams" zu sehen.
  - query mit AND: `foo="bar" AND (baz="qux")`
  - logger appender
    - logstash-gelf
      - *for all major logging frameworks*
      - <https://github.com/mp911de/logstash-gelf> ⭐372
    - logback
      - <https://github.com/osiegmar/logback-gelf> ⭐157
    - log4j
      - <https://github.com/t0xa/gelfj> ⭐183
- **loggly**
  - <https://www.loggly.com/>
  - free & paid tiers
  - Integration für viele Sprachen und Frameworks
  - <mark>cloud only</mark>
  - email alerts, graphs, jira integration, ...
- **logz.io**
  - <https://logz.io/>
  - *Monitoring based on ELK & Grafana*
  - free & paid tiers
- **sentry** → DevOps/Observability
- **loki**
  - *Loki is a multi-tenant log aggregation system inspired by Prometheus.
It is cost effective, easy to operate and allows viewing logs directly in Grafana.*
  - Um Container-Logs anzugreifen, gibt es einen Logging driver für Docker
  - <https://github.com/grafana/loki>
- **Apache Chainsaw**
  - *GUI-based Log viewer*
  - <details>
      <img src="https://logging.apache.org/chainsaw/2.x/images/chainsaw-1.jpg" loading="lazy"/>
    </details>
  - <https://logging.apache.org/chainsaw/2.x/>
- **Otros Log Viewer**
  - Features
    - *Loading logs from remote servers*
    - *Tailing logs from local disk and sftp*
    - *Decompressing "gziped" logs on the fly*
    - *Pluginable log highlightings*
    - ...
  - <https://github.com/otros-systems/otroslogviewer>


## Elastic (ELK) Stack
- **elasticsearch**
  - <https://github.com/elastic/elasticsearch>
  - FOSS-Alternative: [opensearch](https://github.com/opensearch-project/OpenSearch)
    - <https://github.com/opensearch-project/OpenSearch-Dashboards>
- **logstash**
- **kibana**
