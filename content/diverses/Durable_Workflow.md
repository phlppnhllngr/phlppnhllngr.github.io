---
title: Durable Workflow
parent: Diverses
---

# Durable Workflow
{: .no_toc }

## Inhalt
{: .no_toc }
- TOC
{:toc}

## Tools
- **Temporal**
  - Workflows & Scheduling
  - für länger laufende Prozesse
  - *Eliminate complex error or retry logic, avoid callbacks, and ensure that every workflow you start, completes. Temporal delivers durable execution for your services and applications.*
  - SDKs für Java, Go, Python, TS, JS, PHP
  - einfache Installation (nur ein Binary)
  - <https://github.com/temporalio/temporal> <img loading="lazy" src="https://img.shields.io/github/stars/temporalio/temporal?style=flat-square"/>
  - <https://www.youtube.com/@Temporalio>
  - <https://www.baeldung.com/java-temporal-workflow-engine>
- **restate**
  - vs Temporal: <https://news.ycombinator.com/item?id=40660568> 
  - Java SDK: <https://github.com/restatedev/sdk-java> 
  - <https://github.com/restatedev/restate> <img loading="lazy" src="https://img.shields.io/github/stars/restatedev/restate?style=flat-square"/>
- **Inngest**
  - *Inngest is an event-driven durable execution platform that allows you to run fast, reliable code on any platform, without managing queues, infra, or state.*
  - *Write functions in TypeScript, Python or Go to power background and scheduled jobs, with steps built in. We handle the backend infra, queueing, scaling, concurrency, throttling, rate limiting, and observability for you.*
  - <https://github.com/inngest/inngest> <img loading="lazy" src="https://img.shields.io/github/stars/inngest/inngest?style=flat-square"/>
  - <https://www.inngest.com/docs/self-hosting>
- **Openjob**
  - *distributed and high-performance task scheduling framework that supports multiple cronjob, delay task, workflow, lightweight distributed computing, unlimited horizontal scaling, with high scalability and fault tolerance. Also has permission management, powerful alarm monitoring, and support multiple languages*
  - <https://github.com/open-job/openjob> <img loading="lazy" src="https://img.shields.io/github/stars/open-job/openjob?style=flat-square"/>
- **airflow**
  - <https://github.com/apache/airflow> <img loading="lazy" src="https://img.shields.io/github/stars/apache/airflow?style=flat-square"/>
  - docker compose: <https://airflow.apache.org/docs/apache-airflow/2.5.1/docker-compose.yaml>
  - *programmatically author, schedule, and monitor workflows*
  - Python
- **DolphinScheduler**
  - *extensible workflow scheduler platform with powerful DAG visual interfaces, dedicated to solving complex job dependencies in the data pipeline and providing various types of jobs available out of box.*
  - <https://github.com/apache/dolphinscheduler> <img loading="lazy" src="https://img.shields.io/github/stars/apache/dolphinscheduler?style=flat-square"/>
- **Hatchet**
  - *platform for running background tasks, built on top of Postgres.*
  - *built on a durable task queue that enqueues your tasks and sends them to your workers at a rate that your workers can handle. Hatchet will track the progress of your task and ensure that the work gets completed*
  - *it can be used as a queue, a DAG-based orchestrator, a durable execution engine, or all three*
  - <https://github.com/hatchet-dev/hatchet> <img loading="lazy" src="https://img.shields.io/github/stars/hatchet-dev/hatchet?style=flat-square"/>
- **openworkflow**
  - *TypeScript framework for building durable, resumable workflows. Supports Node.js and Bun.* 
  - <https://github.com/openworkflowdev/openworkflow>
  - <https://old.reddit.com/r/javascript/comments/1r18ld3/i_built_openworkflow_a_lightweight_alternative_to/>
- **conductor**
  - *event driven agentic workflow engine providing durable and highly resilient execution engine for applications and AI Agents*
  - <https://github.com/conductor-oss/conductor> <img loading="lazy" src="https://img.shields.io/github/stars/conductor-oss/conductor?style=flat-square"/>

### basierend auf Postgres
- **DBOS**
  - *provides lightweight durable workflows built on top of Postgres*
  - *DBOS workflows make your program durable by checkpointing its state in Postgres*
  - Library; kein externer Service notwendig
  - Java, Python, TS, Go
  - <https://github.com/dbos-inc/dbos-transact-java> <img loading="lazy" src="https://img.shields.io/github/stars/hatchet-dev/hatchet?style=flat-square"/>
  - Vergleich mit Temporal, Airflow: <https://docs.dbos.dev/why-dbos#dbos-vs-other-systems>
  - [Show HN: DBOS Java – Postgres-Backed Durable Workflows, 11/2025](https://news.ycombinator.com/item?id=45920156)
  - [HN: Building durable workflows on Postgres (dbos.dev), 05/2026](https://news.ycombinator.com/item?id=48313530)
- **absurd**
  - *the simplest durable execution workflow system you can think of. It's entirely based on Postgres and nothing else.* 
  - <https://github.com/earendil-works/absurd> <img loading="lazy" src="https://img.shields.io/github/stars/earendil-works/absurd>?style=flat-square"/>
- **pg_durable**
  - <https://github.com/microsoft/pg_durable>
  - <https://news.ycombinator.com/item?id=48414367>
- **PgQue**
  - <https://github.com/NikolayS/pgque>  
