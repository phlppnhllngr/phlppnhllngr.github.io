---
title: Container
parent: Java
---

# Container

## Base-Images
- adoptopenjdk/openjdk11
- gcr.io/distroless/java11-debian11
- openjdk
- registry.access.redhat.com/ubi8/openjdk-11-runtime
  <br/>user.home = /home/jboss
  ```Dockerfile
  FROM registry.access.redhat.com/ubi8/openjdk-11-runtime:1.14-5
  WORKDIR /deployments
  COPY dependency/* libs/
  COPY classes classes
  EXPOSE 8080 8082
  HEALTHCHECK --interval=10s --timeout=2s --start-period=10s --retries=2 \
      CMD curl --silent --fail http://localhost:8080/health || exit 1
  ENTRYPOINT [ "java", \
      "-XX:MaxRAMPercentage=75", \
      "-XX:+UseParallelGC", \
      "-cp", \
      "libs/*:classes/", \
      "-Duser.timezone=Europe/Berlin", \
      "-Dfile.encoding=UTF-8", \
      "com.example.Application" \
  ]
  ```
- <https://hub.docker.com/r/bellsoft/liberica-openjdk-alpine>
  <br/>user.home = /root
  ```Dockerfile
  FROM bellsoft/liberica-openjdk-alpine:11.0.17-7
  WORKDIR /app
  COPY dependency/* libs/
  COPY classes classes
  EXPOSE 8080 8082
  HEALTHCHECK --interval=10s --timeout=2s --start-period=10s --retries=2 \
      CMD wget --no-verbose --tries=1 --spider http://localhost:8080/health || exit 1
  ENTRYPOINT [ "java", \
      "-XX:MaxRAMPercentage=75", \
      "-XX:+UseParallelGC", \
      "-cp", \
      "libs/*:classes/", \
      "-Duser.timezone=Europe/Berlin", \
      "-Dfile.encoding=UTF-8", \
      "com.example.Application" \
  ]
  ```
- <https://hub.docker.com/r/bellsoft/liberica-openjre-alpine>
- <https://hub.docker.com/r/bellsoft/liberica-runtime-container>
- eclipse-temurin
- <https://hub.docker.com/_/amazoncorretto>


## Tipps
- statt der JVM- sollten die Container-Limits (RAM, CPU) gesetzt werden [1]
- *By default, the JVM heap gets 25% of the container’s memory* [1]
- *By default, a container has no resource constraints* (-> Docker: `--cpus`, `--memory`)
- *As of Java 8u191, the JVM is pretty “container aware” by default and interprets CPU share allocation correctly* [1] (auch Memory)
- "fat jars" sollten nicht in Containern deployed werden, da die Dependencies sich kaum ändern und jedes Mal neu mitkopiert werden müssen (jib maven plugin berücksichtigt dies).<br/> *With a fat-jar, all your dependencies get bundled with your own code, in one jar, which then docker puts in a single layer. This means that if your dependencies are 200mb, you will need another 200mb for each code change, and each build.*<br/> Evtl. hat z. B. hat eine 0815-Spring-Boot-App hat nur wenig "eigenen" Code, aber 60mb Deps und 10mb Resources. Deps und Resources sollten stattdessen eigene Layer bekommen:<br/>
  OS -> JRE -> Deps -> Resources -> Code [2]
- JRE-Größe reduzieren mit jlink (strip debug, no headers, no man pages, compress, ...) und jdeps
- *always make sure you allocate at least 25% more memory to your container (i.e. ‘-m’) than your heap size value. Besides heap space your application needs space for Java threads, Garbage collection, metaspace, native memory, socket buffers. All these components require additional memory outside allocated heap size. Besides that, other small processes (like APM agents, splunk scripts, etc.) will also require memory.* [3]
- *if you are running only your Java application within the container, then set initial heap size (...) to the same size as max heap size.* [3]
- Quellen
  - [1, 31.10.19](https://www.ccampo.me/java/docker/containers/kubernetes/2019/10/31/java-in-a-container.html)
  - [2, 10.2019](https://www.reddit.com/r/java/comments/dhr2tn/dont_put_fat_jars_in_docker_images/)
  - [3, 11.2020](https://blog.gceasy.io/2020/11/05/best-practices-java-memory-arguments-for-containers/)
- <https://www.reddit.com/r/java/comments/u349h2/containerize_your_java_applications_a_guide_for/>
- <https://www.reddit.com/r/java/comments/u70j8l/java_17_whats_new_in_openjdks_container_awareness/>
- <https://www.reddit.com/r/java/comments/u7057f/running_java_in_singlecore_containers/>
- <https://www.baeldung.com/ops/docker-jvm-heap-size>
- <https://developers.redhat.com/articles/2022/04/19/best-practices-java-single-core-containers>
- <https://developers.redhat.com/blog/2017/04/04/openjdk-and-containers>
- <https://learn.microsoft.com/en-us/azure/developer/java/containers/overview>
  - *The JVM has heuristics to determine the number of "available processors" based on CPU quota, which can dramatically influence the performance of Java applications.*
  - *The memory allocated to the container itself and the size of the heap area for the JVM are as important as the processors. These factors will determine the behavior of the garbage collector (GC) and the overall performance of the system.*
  - *The JVM has default ergonomics with pre-defined values that are based on number of available processors and amount of memory in the system*
  - *If you don't know how much memory to allocate, a good starting point is 4 GB.*
  - *Allocate 75% of container memory for the JVM heap.* (`-XX:MaxRAMPercentage=75`)
  - *For most general-purpose microservice applications, start with the Parallel GC.*
  - *For any GC other than SerialGC, we recommend two or more vCPU cores. We don't recommend selecting anything less than 1 vCPU core on containerized environments. If you don't know how many cores to start with, a good choice is 2 vCPU cores.*
- [Containerize your Java applications for Kubernetes](https://learn.microsoft.com/en-us/azure/developer/java/containers/kubernetes)
  - Set CPU requests and limits
  - Set memory request and limits
- [Secrets of Performance Tuning Java on Kubernetes - (Bruno Borges - Microsoft), 09/22](https://vimeo.com/748031919)
- Kubernetes: *As a general rule, requests.memory should be equal to limits.memory. Then, instead of using Xms and Xmx, I like to use XX:MaxRAMPercentage=75*
- *many of the concurrent benefits from the default G1 garbage collector on recent Java virtual machines (JVMs) vanish when running with fewer than two cores. All those single-core instances may as well be using the serial collector—and paying the performance cost of that—but many probably don’t even know it.*
  

## Environment & JVM-properties
- Env-Vars sollten/können keine "." enthalten;
  NICHT möglich (docker-compose.yml):
  ```yml
  environment:
   x.y=foo
  ```
  möglich:
  Dockerfile:
  ```Dockerfile
  ENV JAVA_OPTS="-Dx.y=foo -Da.b=bar"
  ```
  oder
  ```Dockerfile
  CMD java -Xmx1024m -Dx.y=foo -Da.b=bar app.jar
  ```
  docker run:
  ```sh
  docker run -e JAVA_OPTS="-Dx.y=foo -Da.b=bar" -e KEY=VALUE
  ```
  docker-compose:
  ```yml
  environment:
   JAVA_OPTS: "-Dx.y=foo -Da.b=bar"
  ```
- *You shouldn't use java $JAVA_OPTS with ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS"]
  <br/>
  The main problem with it is that with this approach you application <mark>won't receive the sigterm</mark> so in case of graceful shutdown it won't work for you (you will find more about the problem here if you are not aware about that)*
  *If you want customize the java opts on docker environments use JAVA_TOOL_OPTIONS environment property and ENTRYPOINT ["java", ...] With this property you can declare your expected options even in Dockerfile like:
  ENV JAVA_TOOL_OPTIONS "-XX:MaxRAMPercentage=80"*
  <https://stackoverflow.com/a/58355963/8972265>
