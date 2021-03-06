---
tags: [Notebooks/Java]
title: Logging
created: '2019-02-20T20:37:28.471Z'
modified: '2021-09-05T12:20:34.910Z'
parent: Java
---

# Logging
→ Diverses/Logging

## Libs
- <https://github.com/akullpp/awesome-java#logging>
<br/>
- **JUL** (java.util.logging)
- **System.Logger** (JDK 9+)
- **SLF4J**
  - <https://www.slf4j.org/>
  - bridging
    - Hat spezielle Erweiterungen (libs; “bridges”), um das Logging von Drittbibliotheken auf den eigenen Logger umzuleiten.
    - bei JUL können zusätzl. Schritte notwendig sein (<https://stackoverflow.com/questions/9117030/jul-to-slf4j-bridge>)
- **Logback**
  - <https://logback.qos.ch/index.html>
  - terse-logback
    - <https://tersesystems.github.io/terse-logback/>
    - *collection of Logback extensions*
  - custom appenders
    - <https://www.baeldung.com/custom-logback-appender>
  - async
    - https://stackoverflow.com/questions/30041842/logback-logging-synchronous-or-asynchronous
    - *you can make any Appender asynchronous much easier (by simply wrapping it in an AsyncAppender) than if all Appender implementations would have to manage the asynchronicity on their own.*
- **Logbook**
  - <https://github.com/zalando/logbook>
  - *extensible Java library for HTTP request and response logging*
  - Integration mit Spring, Servlet, ...
- **Log4j 1**
  - appenders
    - SMTP
      - throttling: <https://github.com/reaktor/log4j-email-throttle>
- **Log4j 2**
- **Flogger**
  - <https://github.com/google/flogger>
  - fluent API
  - Features: rate limits, ...
- **Apache Commons Logging**
  - <https://commons.apache.org/proper/commons-logging/>
- **JCL** (Jakarta Commons Logging)
- **Tracee**
  - <http://www.tracee.io/>
- **pl4j**
  - "pretty logger for java"
  - *slf4j decorator than enables pretty printing on the console using ANSI formatting through jansi*
  - *built around the concept of Markers. This means that you can only use logback as an implementation*
  - <https://github.com/ludovicianul/pl4j>
- **jansi**
  - *Implements ANSI escape colorization*
  - Windows & Linux
  - <https://github.com/fusesource/jansi>
- **tinylog**
  - *lightweight logging framework for Java, Kotlin, Scala, and Android*
  - *is significantly faster than other logging frameworks, as can be seen in the [benchmark](https://tinylog.org/v2/benchmark/).* 
  - <https://github.com/tinylog-org/tinylog> 


## Mapped Diagnostic Context (MDC)
- <https://www.baeldung.com/mdc-in-log4j-2-logback>
  - *MDC = map-like structure with pieces of information that are accessible to the appender when the log message is actually written*
- <https://dzone.com/articles/mdc-better-way-of-logging-1>
  - Use case: Alle Logs mit "user_id" und/oder "request_id" versehen
  - *MDC manages contextual information on a per-thread basis*
- 4 statische Methoden: put, get, remove, clear
- log4j 1 & 2
- slf4j
  - logback
    - <http://logback.qos.ch/manual/mdc.html>
