---
tags: [Notebooks/Diverses]
title: Logging
created: '2020-03-23T21:02:43.094Z'
modified: '2021-09-05T12:33:12.581Z'
parent: Diverses
---

# Logging
- → Devops/APM, Tracing
- <https://www.reddit.com/r/programming/comments/nq7l8v/logging_is_important>

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
  - *log aggregation system, native support in Grafana*
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
