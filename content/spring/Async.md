---
tags: [Notebooks/Spring]
title: Async
created: '2021-04-19T15:56:15.501Z'
modified: '2021-07-11T10:21:44.406Z'
parent: Spring
---

# Async

## Klassen
- *If you do not define an `Executor` bean, Spring creates a `SimpleAsyncTaskExecutor` and uses that.*
- **@Async(bean?)**
  - bean = Name der `Executor`-@Bean
  - Return-Types: void, Future, CompletableFuture
  - *if the return type is void, exceptions will not be propagated to the calling thread*
  - AsyncUncaughtExceptionHandler (I)
- **@EnableAsync**
  - *switches on Spring’s ability to run @Async methods in a background thread pool*
- **interface AsyncConfigurer**
  - `Executor getAsyncExecutor()`
    - dieser Executor wird anwendungsweit der Default-Threadpool für Methoden mit `@Async`
- **ThreadPoolTaskExecutor**
  - [java docs](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/concurrent/ThreadPoolTaskExecutor.html)
  - intern: ThreadPoolExecutor
- **ResponseBodyEmitter**
  - *handles async responses*
  - *we can sidestep needing to use CompleteableFutures, more complicated asynchronous promises, or use of the @Async annotation*
- **SseEmitter**
  - *subclass of ResponseBodyEmitter and provides additional Server-Sent Event (SSE) support out-of-the-box.*
- **StreamingResponseBody**
  - <https://technicalsand.com/streaming-data-spring-boot-restful-web-service/>
    - Beispiele
       - text data
       - json
       - file: txt, pdf, csv; You will see a file immediately get downloaded and the streaming response keeps on writing on that file.
       - audio, video


## Docs
- <https://www.baeldung.com/spring-async>
- <https://www.baeldung.com/spring-mvc-sse-streams>
- <https://spring.io/guides/gs/async-method/>
