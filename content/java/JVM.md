---
tags: [Notebooks/Java]
title: JVM
created: '2020-07-13T08:53:13.664Z'
modified: '2021-07-28T08:03:50.841Z'
parent: Java
---

# JVM

## Diverses
- sun.net.client.defaultConnectTimeout & sun.net.client.defaultReadTimeout
  - *Modern applications use numerous protocols (i.e. SOAP, REST, HTTP, HTTPS, JDBC, RMI, etc.) to connect with remote applications. Sometimes remote applications might take a long time to respond. Sometimes they may not respond at all. If you don’t have proper timeout settings, and if remote applications don’t respond fast enough, then your application threads/resources will get stuck.*
  - *You can pass these two powerful timeout networking properties at the JVM level that can be globally applicable to all protocol handlers that uses java.net.URLConnection*
  - *By default, values for these two properties are -1, which means no timeout is set*
  - `-Dsun.net.client.defaultConnectTimeout=2000 -Dsun.net.client.defaultReadTimeout=2000`
  - beeinflusst offenbar nur URLConnection, aber nicht java.net.http.HttpClient
- user.timezone
  - *you might be using java.util.Date or java.util.Calendar objects. These objects, by default, pick up time zone information from the underlying operating system. This will become a problem if your application is running in a distributed environment.*
  - `-Duser.timezone=US/Eastern`
- user.language
- `user.country`


## Memory

### Heap
- Xms
  - *initial memory allocation (heap)*
  - `-Xms256m`
  - *has no default value*
- Xmx
  - *max heap, eg `-Xmx2048m`*
  - *typically has a default value of 256 MB / default value will depend on platform and amount of memory available in the system*

#### PermGen
- permanent generation
- `-XX:MaxPermSize`
- *store class and method info, interned strings*
- *does not exist anymore since java 8 → metaspace*

### Metaspace
- *not part of heap*
- *native memory / process memory*
- *max size specified by `-XX:MaxMetaspaceSize`, default: effectively infinite*
- *only limited by host os => loading lots of classes or interned strings can bring down not just the application, but the entire host (server)*
- *Metaspace is the region where JVM’s metadata definitions, such as class definitions, method definitions, will be stored. By default, the amount of memory that can be used to store this metadata information is unlimited (i.e. limited by your container or machine’s RAM size).*

### Stack
- *local primitives and local object refs*
- *each thread has its own private stack*
- *default stack size is usually 1MB on 64bit machines*
- *configure stack size with `-Xss` and `-XX:ThreadStackSize`*

### GC
- <https://dzone.com/articles/interesting-garbage-collection-patterns>
- <https://www.reddit.com/r/java/comments/qlxopy/how_to_choose_the_best_java_garbage_collector/.compact>

#### Caveats
- *The GC is unable to clear static fields unless the class that owns it is unloaded, which only happens if the Classloader that called it is garbage collected.*
- *Unclosed system resources: The GC indirectly frees up files since classes like FileInputStream are written such that if an instance is garbage collected, the ‘close()’ method will be called first. This way, unclosed system resources don’t always pose a risk, so a lot of developers tend to look over them.*
- *Unclosed connections: Like with unclosed resources, unclosed database or network connections can lead to significant memory use if not unloaded.*


## Container
- statt der JVM- sollten die Container-Limits (RAM, CPU) gesetzt werden [1]
- *By default, the JVM heap gets 25% of the container’s memory* [1]
- *As of Java 8u191, the JVM is pretty “container aware” by default and interprets CPU share allocation correctly* [1] (auch Memory)
- "fat jars" sollten nicht in Containern deployed werden, da die Dependencies sich kaum ändern und jedes Mal neu mitkopiert werden müssen (jib maven plugin berücksichtigt dies).<br/> *With a fat-jar, all your dependencies get bundled with your own code, in one jar, which then docker puts in a single layer. This means that if your dependencies are 200mb, you will need another 200mb for each code change, and each build.*<br/> Evtl. hat z. B. hat eine 0815-Spring-Boot-App hat nur wenig "eigenen" Code, aber 60mb Deps und 10mb Resources. Deps und Resources sollten stattdessen eigene Layer bekommen:<br/>
  OS -> JRE -> Deps -> Resources -> Code [2]
- JRE-Größe reduzieren mit jlink (strip debug, no headers, no man pages, compress, ...) und jdeps
- *always make sure you allocate at least 25% more memory to your container (i.e. ‘-m’) than your heap size value* [3]
- *if you are running only your Java application within the container, then set initial heap size (...) to the same size as max heap size.* [3]
- Quellen
  - [1, 31.10.19](https://www.ccampo.me/java/docker/containers/kubernetes/2019/10/31/java-in-a-container.html)
  - [2, 10.2019](https://www.reddit.com/r/java/comments/dhr2tn/dont_put_fat_jars_in_docker_images/)
  - [3, 11.2020](https://blog.gceasy.io/2020/11/05/best-practices-java-memory-arguments-for-containers/)

### Environment & JVM-properties
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
  The main problem with it is that with this approach you application won't receive the sigterm so in case of graceful shutdown it won't work for you (you will find more about the problem here if you are not aware about that)*
  *If you want customize the java opts on docker environments use JAVA_TOOL_OPTIONS environment property and ENTRYPOINT ["java", ...] With this property you can declare your expected options even in Dockerfile like:
  ENV JAVA_TOOL_OPTIONS "-XX:MaxRAMPercentage=80"*
  <https://stackoverflow.com/a/58355963/8972265>
