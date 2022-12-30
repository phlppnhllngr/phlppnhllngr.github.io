---
tags: [Notebooks/DevOps]
title: 'Observability'
created: '2019-02-28T20:30:32.613Z'
modified: '2021-09-05T12:32:43.703Z'
parent: DevOps
---

# Observability
- APM
  - application performance monitoring/management
- Observability
  - Metrics, Tracing, Logs
- <https://haydenjames.io/observability-plus-20-observability-software-vendors/>


## Tracing
- → Diverses/Logging
- <https://opentracing.io/docs/overview/what-is-tracing/>
- **Trace**
  - *A trace ID helps to connect log events in one service and log events in another service*
  - *Service 1 is called and generates the trace ID “1234”. It then calls Services 2 and 3, propagating the same trace ID to them, so that they can add the same trace ID to their log events, making it possible to connect log events across all services by searching for a specific trace ID*
  - <https://reflectoring.io/structured-logging/>
- **Span**
  - *For each outgoing request, Service 1 also creates a unique “span ID”. While a trace spans the whole request/response cycle of Service 1, a span only spans the request/response cycle between one service and another.*


## Tools
- **hyperping** 💰
  - <https://hyperping.io/>
  - uptime monitoring
- **pingdom** 💰
- **uptimeRobot**
  - <https://uptimerobot.com/>
  - freemium
- **uptime kuma**
  - *a self-hosted monitoring tool like "Uptime Robot".*
  - *Monitoring uptime for HTTP(s) / TCP / Ping / DNS Record*
  - *Fancy, Reactive, Fast UI/UX*
  - <https://github.com/louislam/uptime-kuma>
- **NewRelic** 💰
  - <https://newrelic.com/>
  - *supports applications developed in Java, Scala, Ruby, Python, PHP, .NET, and Node.js*
- **scout** 💰
  - <https://scoutapp.com/>
- **rollbar** 💰
  - <https://rollbar.com/>
- **sentry**
  - <https://sentry.io/>
  - *open-source application monitoring platform*
  - Error-Reporting für diverse Sprachen (java; logback, spring, ..., js; browser / node, ...)
  - <mark>self-hosted</mark> (https://docs.sentry.io/server/) oder Cloud
- **prometheus**
  - <https://prometheus.io/>
  - <https://github.com/prometheus/prometheus>
  - metrics
  - *<mark>open-source</mark> systems monitoring and alerting toolkit*
- **grafana**
  - <https://grafana.com/>
  - <https://github.com/grafana/grafana> ⭐31k
  - *allows you to query, visualize, alert on and understand your metrics no matter where they are stored*
  - *supports over 30 open source and commercial data sources.*
- **splunk** 💰
  - <https://www.splunk.com/>
- **Apache Skywalking**
  - <https://github.com/apache/skywalking>
  - *designed for microservices, cloud native and container-based architectures / monitoring, tracing, diagnosing capabilities for distributed system in Cloud Native architecture*
- **bugsnag** 💰
  - <https://www.bugsnag.com/>
  - *Automated error monitoring, reporting, alerting, and diagnostic capture for mobile, web, and backend apps*
  - Integration für zahlreiche Sprachen und Frameworks, u. A. Spring (Boot)
- **pagerduty** 💰
  - <https://www.pagerduty.com/>
- **airbrake** 💰
  - Error Monitoring, Performance Monitoring, Deploy Tracking
  - <https://airbrake.io/>
- **errbit**
  - *open source error catcher that's Airbrake API compliant*
  - <https://github.com/errbit/errbit> *4.2k
- **honeycomb** 💰
  - <https://www.honeycomb.io/>
- **datadog**
  - <https://www.datadoghq.com/>
- **Elastic APM**
  - <https://www.elastic.co/apm>
- **jaeger**
  - tracing
  - <https://github.com/jaegertracing/jaeger> *13.2k
- **zipkin**
  - tracing
  - <https://github.com/openzipkin/zipkin> *14.2k
- **lightstep** 💰
  - <https://lightstep.com/>
- **opentelemetry**
  - <https://opentelemetry.io/>
  - <https://github.com/open-telemetry>
  - *provides a single set of APIs, libraries, agents, and collector services to capture distributed traces and metrics from your application. You can analyze them using Prometheus, Jaeger, and other observability tools.*
  - Libs, SDKs und Tools um Metriken, Traces und Logs vendor-unabhängig/-übergreifend zu sammeln
  - kein Backend enthalten, d.h. man braucht zusätzlich einen separaten Service, der das Gesammelte aufnimmt
  - <https://www.dynatrace.com/news/blog/what-is-opentelemetry/>
  <img src="https://dt-cdn.net/wp-content/uploads/2020/07/OT.png" loading="lazy">
- **signoz**
  - *helps developers monitor their applications & troubleshoot problems, an open-source alternative to DataDog, NewRelic, etc.*
  - *We support OpenTelemetry as the library which you can use to instrument your applications. So any framework and language supported by OpenTelemetry is also supported by SigNoz.*
  - <https://github.com/SigNoz/signoz> *4.4k
- **statsd**
  - *Daemon for easy but powerful stats aggregation*
  - *A network daemon that runs on the Node.js platform and listens for statistics, like counters and timers, sent over UDP or TCP and sends aggregates to one or more pluggable backend services (e.g., Graphite).* 
  - <https://github.com/statsd/statsd>
- **Promscale**
  - *a unified metric and trace observability backend for Prometheus, Jaeger and OpenTelemetry built on PostgreSQL and TimescaleDB*
  - *Unlike other observability backends, it has a simple and easy-to-manage architecture with just two components: the Promscale Connector and the Promscale Database (PostgreSQL with the TimescaleDB and Promscale extensions)*
  - <https://github.com/timescale/promscale>
- **Uptrace**
  - *APM tool with support for distributed tracing, metrics, and logs*
  - *You can use it to monitor applications and set up automatic alerts to receive notifications via email, Slack, Telegram, and more*
  - *uses OpenTelelemetry to collect data and ClickHouse database to store it. ClickHouse is the only dependency.* 
  - <https://github.com/uptrace/uptrace>
- **VictoriaMetrics**
  - *fast, cost-effective monitoring solution and time series database*
  - *can be used as long-term storage for Prometheus. can be used as a drop-in replacement for Prometheus in Grafana, because it supports Prometheus querying API. can be used as a drop-in replacement for Graphite in Grafana, because it supports Graphite API.*
  - *consists of a single small executable without external dependencies*
  - <https://github.com/VictoriaMetrics/VictoriaMetrics> 
