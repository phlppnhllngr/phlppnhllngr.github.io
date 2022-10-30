---
tags: [Notebooks/Java]
title: JDK
created: '2019-02-21T16:00:15.322Z'
modified: '2021-07-29T06:10:52.572Z'
parent: Java
---

# JDK
<img src="https://opensource.com/sites/default/files/2022-03/jdk.jpg" loading="lazy"/><br/><br/>
- The Java Version Almanac - <https://javaalmanac.io/>
- <https://endoflife.date/java>

## Distributionen
- **OpenJDK**
    - Der Begriff meint zum einen das Open-Source-Repository mit dem Java-Quellcode, zum anderen die Distribution (Builds/Binaries) von Oracle (“Oracle OpenJDK”). Hier gibt es keinen Support und nach 6 Monaten (Release neue Version) keine weiteren Updates, auch nicht für "LTS"-Versionen (hierzu siehe unten).
- **OracleJDK**
    - OpenJDK mit ein paar Erweiterungen. Kostenpflichtig ab Java 12. Längerer Support für LTS-Versionen. Es gibt Lizenzen für Entwickler oder persönlichen Gebrauch, kommerzielle Verwendung ist hier aber ausgeschlossen.
    - LTS
        - *Oracle's stated opinion is that there's nothing special about LTS releases, and they merely correspond to an Oracle support product and should not be significant to anyone who is not a paying customer that buys support from Oracle.*
- **Andere OpenJDK Distributionen**
    - mit LTS-Support, zum Teil kostenpflichtig
    - Amazon Corretto (kostenlos, Updates für 8 bis 2023, 11 ab April 19 und bis 2024)
    - IBM
    - Red Hat
    - ~~AdoptOpenJDK~~ Adoptium
        - *The Adoptium Working Group promotes and supports (...) runtimes and associated technology for use across the Java ecosystem. <mark>Eclipse Temurin</mark> is the name of the OpenJDK distribution from Adoptium.* 
        - [https://adoptium.net/](https://adoptium.net/)
    - ...


## Upgrade guides
- [Oracle JDK Migration Guide](https://docs.oracle.com/en/java/javase/17/migrate/getting-started.html)
- <https://blogs.oracle.com/javamagazine/post/its-time-to-move-your-applications-to-java-17-heres-why-and-heres-how>


## /jdk/bin
- **jcmd** (java diagnostic command tool)
    - <https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr006.html>
    - *The jcmd utility is used to send diagnostic command requests to the JVM, where these requests are useful for controlling Java Flight Recordings, troubleshoot, and diagnose JVM and Java Applications.*
    - *it must be used on the same machine on which JVM is running*
- **jinfo**
- **jmap**
- **jlink**
    ```
    # Führt zu "java: not found" in 2. Stage, daher corretto:
    # FROM adoptopenjdk/openjdk11:jdk-11.0.11_9-alpine as jre-builder

    FROM amazoncorretto:11-alpine3.16 as jre-builder

    WORKDIR /build

    COPY target/classes classes

    COPY target/dependency/* libs/

    RUN $JAVA_HOME/bin/jdeps \
        --ignore-missing-deps \
        --multi-release 11 \
        --print-module-deps  \
        --recursive \
        --class-path=libs/* \
        --module-path=libs/* \
        ./classes \
        > jre-deps.info

    RUN $JAVA_HOME/bin/jlink \
        --verbose \
        --add-modules $(cat jre-deps.info) \
        --strip-debug \
        --no-man-pages \
        --no-header-files \
        --compress=2 \
        --output /custom-jre


    FROM alpine:3.16.2

    COPY --from=jre-builder /custom-jre /jre

    WORKDIR /app

    COPY target/classes classes

    COPY target/dependency/* libs/

    ENV JAVA_TOOL_OPTIONS "-XX:MaxRAMPercentage=75"

    ENTRYPOINT [ "/jre/bin/java", \
        "-cp", \
        "libs/*:classes/", \
        "com.example.Main" \
    ]
    ```

    - <https://www.morling.dev/blog/smaller-faster-starting-container-images-with-jlink-and-appcds/>
    - <https://medium.com/hotels-com-technology/honey-i-shrank-the-java-image-9f737aef8963>
    - <https://blog.wolt.com/engineering/2022/05/13/how-to-reduce-jvm-docker-image-size/>
    - <https://blogs.oracle.com/javamagazine/post/containerizing-apps-with-jlink>
    - <https://levelup.gitconnected.com/java-developing-smaller-docker-images-with-jdeps-and-jlink-d4278718c550>
- **jmod**
- **jimage**
- **jdeps**
- **jstat**
- **javap**
- **jstack**
    - *attaches to the specified process or core file and prints the stack traces of all threads that are attached to the virtual machine, including Java threads and VM internal threads, and optionally native stack frames. The utility also performs deadlock detection.*
- **jmc** (java mission control)
    - *contains a plugin that allows us to visualize the data collected by JFR*
      <br/><img src="https://download.oracle.com/technology/products/missioncontrol/updatesites/base/5.2.0/eclipse/images/screen-capture-01-large.png" loading="lazy"/>
- **jfr** (java flight recorder)
    - *collects information about the events in a Java Virtual Machine (JVM) during the execution of a Java application*
    - *is a tool for collecting diagnostic and profiling data about a running Java application. It is integrated into the Java Virtual Machine (JVM)*
    - *low overhead, continuous monitoring*
    - *not a standalone tool*
    - *activate it in two ways: when starting a Java application or
      passing diagnostic commands of the jcmd tool when a Java application is already running*
    - <https://github.com/flight-recorder/health-report>
    - <https://www.javaadvent.com/2021/12/keep-your-sql-in-check-with-flight-recorder-jmc-agent-and-jfrunit.html>
    - Übersicht jfr events: <https://bestsolution-at.github.io/jfr-doc/>
    - Custom events (jdk.jfr api; java 9+): <https://www.morling.dev/blog/rest-api-monitoring-with-custom-jdk-flight-recorder-events/>
    - <https://blogs.oracle.com/javamagazine/java-flight-recorder-and-jfr-event-streaming-in-java-14>
    - <https://www.baeldung.com/java-flight-recorder-monitoring>
    - <https://cryostat.io/> - *JFR for Containerized Java Applications*
  - **jconsole**
    - *The JConsole graphical user interface is a monitoring tool that complies to the Java Management Extensions (JMX) specification. JConsole uses the extensive instrumentation of the Java Virtual Machine (Java VM) to provide information about the performance and resource consumption of applications running on the Java platform.*
    - <https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html>
    <br/><img src="https://docs.oracle.com/javase/8/docs/technotes/guides/management/figures/overviewtab.gif" loading="lazy" />
