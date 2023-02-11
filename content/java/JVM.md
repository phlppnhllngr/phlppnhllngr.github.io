---
tags: [Notebooks/Java]
title: JVM
created: '2020-07-13T08:53:13.664Z'
modified: '2021-07-28T08:03:50.841Z'
parent: Java
---

# JVM

## Parameter, Flags
- **JAVA_OPTS**
  - Env-Var
  - *JAVA_OPTS is a convention used by Apache Tomcat and some other apps*
- **_JAVA_OPTIONS**
  - *_JAVA_OPTIONS trumps command-line arguments, which in turn trump JAVA_TOOL_OPTIONS*
  - *_JAVA_OPTIONS is Oracle specific. IBM JVM is using IBM_JAVA_OPTIONS instead*
  - nicht offiziell dokumentiert
- **JAVA_TOOL_OPTIONS**
  - Env-Var
  - <https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/envvars002.html>
    - *In many environments the command line is not readily accessible to start the application with necessary command-line options. This often arises with applications that use embedded VMs, or where the startup is deeply nested in scripts. In these environments the JAVA_TOOL_OPTIONS environment variable can be useful to augment a command line.*
    - *When JAVA_TOOL_OPTIONS is defined, a message is always echoed to stdout, like "Picked up JAVA_TOOL_OPTIONS ..."*
- **classpath**
  - spezifiziert Classpath
  - alias `cp`
  - siehe auch `-Djava.class.path`, `CLASSPATH`-Env-Var, `Class-Path`-Manifest-Eintrag
- **client, server**
  - `java -server ...`
  - *The JDK includes two flavors of the VM -- a client-side offering, and a VM tuned for server applications*
  - *Although the Server and the Client VMs are similar, the Server VM has been specially tuned to maximize peak operating speed. It is intended for executing long-running server applications, which need the fastest possible operating speed more than a fast start-up time or smaller runtime memory footprint.*
  - *The Client VM compiler serves as an upgrade for both the Classic VM and the just-in-time (JIT) compilers used by previous versions of the JDK. The Client VM offers improved run time performance for applications and applets. The Java HotSpot Client VM has been specially tuned to reduce application start-up time and memory footprint, making it particularly well suited for client environments. In general, the client system is better for GUIs.*
  - *A 64-bit capable JDK currently ignores this option and instead uses the Java Hotspot Server VM. The Sun/Oracle 64 builds did not even ship with a client JVM.*
  - wie es bestimmt wird: siehe <https://developers.redhat.com/articles/2022/04/19/best-practices-java-single-core-containers#the_jvm_as_a_dynamic_execution_platform>
- **agentlib**
  - `-agentlib:jdwp=transport=dt_socket,server=n,suspend=y,address=localhost:<port>`
  - für Debugging 

### -D
- **sun.net.client.defaultConnectTimeout, sun.net.client.defaultReadTimeout**
  - *Modern applications use numerous protocols (i.e. SOAP, REST, HTTP, HTTPS, JDBC, RMI, etc.) to connect with remote applications. Sometimes remote applications might take a long time to respond. Sometimes they may not respond at all. If you don’t have proper timeout settings, and if remote applications don’t respond fast enough, then your application threads/resources will get stuck.*
  - *You can pass these two powerful timeout networking properties at the JVM level that can be globally applicable to all protocol handlers that uses java.net.URLConnection*
  - *By default, values for these two properties are -1, which means no timeout is set*
  - `-Dsun.net.client.defaultConnectTimeout=2000 -Dsun.net.client.defaultReadTimeout=2000`
  - beeinflusst offenbar nur URLConnection, aber nicht java.net.http.HttpClient
- **user.timezone**
  - *you might be using java.util.Date or java.util.Calendar objects. These objects, by default, pick up time zone information from the underlying operating system. This will become a problem if your application is running in a distributed environment.*
  - `-Duser.timezone=US/Eastern`
- **user.language**
- **user.country**
- **java.endorsed.dirs**
  - *From time to time it is necessary to update the Java platform in order to incorporate newer versions of standards that are created outside of the Java Community Process (Endorsed Standards), or in order to update the version of a technology included in the platform to correspond to a later standalone version of that technology (Standalone Technologies). The Endorsed Standards Override Mechanism provides a means whereby later versions of classes and interfaces that implement Endorsed Standards or Standalone Technologies may be incorporated into the Java Platform.*
  - *If no value is set for java.endorsed.dirs, then Oracle's implementation of the Java platform looks for JAR files in a default standard location: Microsoft Windows: <java-home>\lib\endorsed / Solaris or Linux: <java-home>/lib/endorsed* 
  - *With the exception of packages listed here and the technologies listed in the Standalone Technologies section below, no other packages from the Java SE platform API specification may be overridden (...) javax.rmi.CORBA, org.w3c.dom, org.xml.sax, org.omg.CosNaming, (...)*
  - <https://docs.oracle.com/javase/8/docs/technotes/guides/standards/>
- **java.ext.dirs** -> Extension Mechanism
- **file.encoding**
  - `-Dfile.encoding=UTF-8`
- **javax.net.debug**
  - für http-Tracing  
  - `-Djavax.net.debug=all`
  - <https://colinpaice.blog/2020/04/05/using-java-djavax-net-debug-to-examine-data-flows-including-tls/>
- **java.security.debug**

#### Proxy
- **http(s).proxyHost**
  - `-Dhttp.proxyHost=example.com`
- **http(s).proxyPort**
  - `-Dhttp.proxyPort=1234`
- **http(s).nonProxyHosts**
  - `-Dhttp.nonProxyHosts=localhost|127.0.0.1|*.foo.com|example.com|...`
- **http(s).proxyUser**
- **http(s).proxyPassword**
- **java.net.useSystemProxies**
  - `-Djava.net.useSystemProxies=true`

#### JMX (remote)
```
-Dcom.sun.management.jmxremote=true
-Dcom.sun.management.jmxremote.port=8989
-Dcom.sun.management.jmxremote.rmi.port=8989
-Dcom.sun.management.jmxremote.authenticate=false
-Dcom.sun.management.jmxremote.ssl=false
-Djava.rmi.server.hostname=localhost (docker)
-Dcom.sun.management.jmxremote.local.only=false
```
  
### -X, -XX

#### X
- **share**
  - `Xshare:dump`
  - `Xshare:on`
    - *While class data sharing is enabled by default on JDK 12 and newer, explicitely enforcing it will ensure an error is raised if something is wrong, e.g. a mismatch of Java versions between building and using the archive*
- **log**
  - `-Xlog:gc:file=gc.txt`
  - `-Xlog:class+load:file=/path/to/classload.log`

#### XX
- -XX = non-standard
- -XX:+Foo / -XX:-Foo für Boolean-Flags, -XX:Foo=Bar für Werte
<br/><br/>
- **+/-PrintFlagsFinal**
- **+/-UseContainerSupport**
  - *Starting from Java 10, this parameter (which is enabled by default) is used to make the JVM take the container memory limits into account when allocating the heap size, not the host machine configuration. This option was backported to Java 8.*  
- **MAXRamPercentage**
- **InitialRAMPercentage**
- **showSettings:vm**
- **+/-StackTraceInThrowable**
- **+/-UseStringDeduplication**
- **+/-UseBiasedLocking**
- **+/-UseParallelGC**
- **+/-UnlockDiagnosticVMOptions**
- **+/-DebugNonSafepoints**
- **+/-UseAppCDS**
  - *made obsolete in JDK 11, expired in JDK 12*
- **SharedArchiveFile**
  - `-XX:SharedArchiveFile=/path/to/classes.jsa`
- **+/-ShowCodeDetailsInExceptionMessages**
- **DumpLoadedClassList**
  - `-XX:DumpLoadedClassList=/path/to/classes.lst`
- **ArchiveClassesAtExit*
  - *Triggers creation of a AppCDS archive at the given location upon application shutdown*
  - *Only loaded classes will be added to the archive. As classloading on the JVM happens lazily, you must invoke some functionality in your application in order to cause all the relevant classes to be loaded.*
  - `ArchiveClassesAtExit=/path/to/app-cds.jsa`  
- **SharedClassListFile**
  - `-XX:SharedClassListFile=/path/to/classes.lst`
  

## Memory
- <https://www.baeldung.com/java-memory-beyond-heap>

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
- *metadata for classes. When a class is loaded, the JVM allocates the metadata of the class, which is its runtime representation, into Metaspace. Whenever the class loader and all its classes are removed from the heap, then their allocation in Metaspace can be considered to be freed by GC.*
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
  
### Code cache
- *The Just-In-Time (JIT) compiler stores its output in the code cache area. A JIT compiler compiles bytecode to native code for frequently executed sections, aka Hotspots.*
- *The goal of the tiered compilation is (...) to have both fast startup times and good long-term performance. Tiered compilation increases the amount of code that needs to be cached in memory by up to four times. Since Java 8, this is enabled by default for JIT, although we still can disable tiered compilation.*

### GC
- <https://dzone.com/articles/interesting-garbage-collection-patterns>
- <https://www.reddit.com/r/java/comments/qlxopy/how_to_choose_the_best_java_garbage_collector/.compact>

#### Caveats
- *The GC is unable to clear static fields unless the class that owns it is unloaded, which only happens if the Classloader that called it is garbage collected.*
- *Unclosed system resources: The GC indirectly frees up files since classes like FileInputStream are written such that if an instance is garbage collected, the ‘close()’ method will be called first. This way, unclosed system resources don’t always pose a risk, so a lot of developers tend to look over them.*
- *Unclosed connections: Like with unclosed resources, unclosed database or network connections can lead to significant memory use if not unloaded.*

### Symbol
- *The JVM uses the Symbol area to store symbols such as field names, method signatures, and interned strings*
  
### Arena
  
### Other
- *Every other memory usage that can't be categorized in the native memory area falls in this section. As an example, DirectByteBuffer usage is indirectly visible in this part.*


## Extension Mechanism
- `java.ext.dirs`
- *standard, scalable way to make custom APIs available to all applications running on the Java platform*
- *all applications using that JRE (or potentially all applications on the host) can see the same classes without need to explicitly specify them on the classpath*
- Reihenfolge class loading: bootstrap, extensions, classpath
- entfernt in Java 9
