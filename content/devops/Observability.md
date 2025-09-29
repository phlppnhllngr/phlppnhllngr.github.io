---
title: 'Observability'
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
  - *represents requests and consists of multiple spans* 
  - *A trace ID helps to connect log events in one service and log events in another service*
  - *Service 1 is called and generates the trace ID “1234”. It then calls Services 2 and 3, propagating the same trace ID to them, so that they can add the same trace ID to their log events, making it possible to connect log events across all services by searching for a specific trace ID*
  - <https://reflectoring.io/structured-logging/>
- **Span**
  - *represents single operation in a request*
  - *contains name, time, log message, metadata* 
  - *For each outgoing request, Service 1 also creates a unique “span ID”. While a trace spans the whole request/response cycle of Service 1, a span only spans the request/response cycle between one service and another.*
- **Context**
  - *immutable object contained in the span data*
  - *identifies the request uniquely*


## Tools
- **hyperping** 💰
  - <https://hyperping.io/>
  - uptime monitoring
- **pingdom** 💰
- **uptimeRobot**
  - <https://uptimerobot.com/>
  - freemium
- **uptime-kuma**
  - *a self-hosted monitoring tool like "Uptime Robot".*
  - *Monitoring uptime for HTTP(s) / TCP / Ping / DNS Record*
  - *Fancy, Reactive, Fast UI/UX*
  - <https://github.com/louislam/uptime-kuma>
- **Gatus**
  - *developer-oriented health dashboard*
  - <https://github.com/TwiN/gatus>
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
  - <https://github.com/prometheus/prometheus> <img loading="lazy" src="https://img.shields.io/github/stars/prometheus/prometheus?style=flat-square"/>
  - metrics
  - *<mark>open-source</mark> systems monitoring and alerting toolkit*
  - docker-compose:
    ```yaml
    version: '3.8'
    services:
      grafana:
        image: grafana/grafana-oss:latest
        restart: unless-stopped
        ports:
          - "3000:3000"
        links:
          - prometheus
        volumes:
          - /foo:/var/lib/grafana
      prometheus:
        image: prom/prometheus:latest
        restart: unless-stopped
        volumes:
          - ./prometheus.yml:/etc/prometheus/prometheus.yml
          - /bar/:/prometheus
        ports:
          - "9090:9090"
    ```

    prometheus.yml

    ```yaml
    global:
      scrape_interval: 15s 
    scrape_configs:
      # Prometheus itself
      # This uses the static method to get metrics endpoints
      - job_name: "prometheus"
        honor_labels: true
        static_configs:
          - targets: ["localhost:9090"]
      - job_name: "some-app"
        scrape_interval: 5s
        static_configs:
          - targets: ["host.docker.internal:8080"] # "Instance" im Grafana-Dashboard mit ID 4701 ("JVM-Micrometer")
            labels:
              application: some-app # Label ist zwingend erforderlich für Grafana-Dashboard mit ID 4701 ("JVM-Micrometer")
        metrics_path: /prometheus
    ```

- **grafana**
  - <https://grafana.com/>
  - <https://github.com/grafana/grafana> <img loading="lazy" src="https://img.shields.io/github/stars/grafana/grafana?style=flat-square"/>
  - *allows you to query, visualize, alert on and understand your metrics no matter where they are stored*
  - *supports over 30 open source and commercial data sources.*
- **splunk** 💰
  - <https://www.splunk.com/>
- **Apache Skywalking**
  - <https://github.com/apache/skywalking> <img loading="lazy" src="https://img.shields.io/github/stars/apache/skywalking?style=flat-square"/>
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
  - <https://github.com/errbit/errbit> <img loading="lazy" src="https://img.shields.io/github/stars/errbit/errbit?style=flat-square"/>
- **honeycomb** 💰
  - <https://www.honeycomb.io/>
- **datadog**
  - <https://www.datadoghq.com/>
- **HyperDX**
  - *observability platform unifying session replays, logs, metrics, traces and errors*
  - *open source and developer-friendly alternative to Datadog and New Relic*
  - <https://github.com/hyperdxio/hyperdx> <img loading="lazy" src="https://img.shields.io/github/stars/hyperdxio/hyperdx?style=flat-square"/>
- **Elastic APM**
  - <https://www.elastic.co/apm>
- **jaeger**
  - tracing
  - <https://github.com/jaegertracing/jaeger> <img loading="lazy" src="https://img.shields.io/github/stars/jaegertracing/jaeger?style=flat-square"/>
- **zipkin**
  - tracing
  - <https://github.com/openzipkin/zipkin> <img loading="lazy" src="https://img.shields.io/github/stars/openzipkin/zipkin?style=flat-square"/>
- **lightstep** 💰
  - <https://lightstep.com/>
- **opentelemetry**
  - <https://opentelemetry.io/>
  - <https://github.com/open-telemetry>
  - *provides a single set of APIs, libraries, agents, and collector services to capture distributed traces and metrics from your application. You can analyze them using Prometheus, Jaeger, and other observability tools.*
  - Libs, SDKs und Tools um Metriken, Traces und Logs vendor-unabhängig/-übergreifend zu sammeln
  - kein Backend enthalten, d.h. man braucht zusätzlich einen separaten Service, der das Gesammelte aufnimmt
  - [HN - OpenTelemetry in 2023](https://news.ycombinator.com/item?id=37295097)
  - <https://www.dynatrace.com/news/blog/what-is-opentelemetry/>
  <img src="https://dt-cdn.net/wp-content/uploads/2020/07/OT.png" loading="lazy">
  - docker-otel-lgtm
    - *An OpenTelemetry backend in a Docker image* 
    - *backend for OpenTelemetry that's intended for development, demo, and testing environments*
    - beinhaltet Grafana, Loki (Logs DB), Prometheus (Metrics DB), Tempo (Traces DB), Pyroscope (Profiling DB)
    - <https://github.com/grafana/docker-otel-lgtm>
    - [Fireship LGTM-Stack](https://www.youtube.com/watch?v=1X3dV3D5EJg)
- **signoz**
  - *helps developers monitor their applications & troubleshoot problems, an open-source alternative to DataDog, NewRelic, etc.*
  - *We support OpenTelemetry as the library which you can use to instrument your applications. So any framework and language supported by OpenTelemetry is also supported by SigNoz.*
  - <https://github.com/SigNoz/signoz> <img loading="lazy" src="https://img.shields.io/github/stars/SigNoz/signoz?style=flat-square"/>
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
- **Keep**
  - *Simple Alerting tool*
  - <https://github.com/keephq/keep>
- **tempo**
  - *easy-to-use and high-scale distributed tracing backend. Tempo is cost-efficient, requiring only object storage to operate, and is deeply integrated with Grafana, Prometheus, and Loki.*
  - *Tempo is Jaeger, Zipkin, Kafka, OpenCensus and OpenTelemetry compatible. It ingests batches in any of the mentioned formats, buffers them and then writes them to Azure, GCS, S3 or local disk. As such it is robust, cheap and easy to operate!* 
  - <https://github.com/grafana/tempo>
- **Pyroscope**
  - *continuous profiling platform*
  - *Debug performance issues down to a single line of code*
  - Unterstützte Langs: Go, Java (via async-profiler), Python, Ruby, NodeJs, .NET, Rust 
  - <https://github.com/grafana/pyroscope>
- **Hertzbeat**
  - <https://github.com/apache/hertzbeat> <img loading="lazy" src="https://img.shields.io/github/stars/apache/hertzbeat?style=flat-square"/>
- **Coroot**
  - *open-source APM & Observability tool, a DataDog and NewRelic alternative*
  - *Metrics, logs, traces, and profiles are gathered automatically by using eBPF* 
  - <https://github.com/coroot/coroot>
- **DeepFlow**
  - *eBPF-powered observability & zero-code distributed tracing* 
  - <https://github.com/deepflowio/deepflow> <img loading="lazy" src="https://img.shields.io/github/stars/deepflowio/deepflow?style=flat-square"/>
- **OneUptime**
  - *complete open-source observability platform* 
  - <https://github.com/OneUptime/oneuptime>
- **OpenObserve**
  - *observability platform built specifically for logs, metrics, traces, analytics, RUM (Real User Monitoring - Performance, Errors, Session Replay)* 
  - <https://github.com/openobserve/openobserve> <img loading="lazy" src="https://img.shields.io/github/stars/openobserve/openobserve?style=flat-square"/>
