---
title: JVM
parent: Java
---

# JVM

## Parameter, Flags
- [VM Options Explorer](https://chriswhocodes.com/)
- **JAVA_OPTS**
  - Env-Var
  - *JAVA_OPTS is a convention used by Apache Tomcat and some other apps*
- **_JAVA_OPTIONS**
  - *_JAVA_OPTIONS trumps command-line arguments, which in turn trump JAVA_TOOL_OPTIONS*
  - *_JAVA_OPTIONS is Oracle specific. IBM JVM is using IBM_JAVA_OPTIONS instead*
  - nicht offiziell dokumentiert
- **JVM_ARGS**
  - Liberty
- **JAVA_TOOL_OPTIONS**
  - Env-Var
  - <https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/envvars002.html>
    - *In many environments the command line is not readily accessible to start the application with necessary command-line options. This often arises with applications that use embedded VMs, or where the startup is deeply nested in scripts. In these environments the JAVA_TOOL_OPTIONS environment variable can be useful to augment a command line.*
    - *When JAVA_TOOL_OPTIONS is defined, a message is always echoed to stdout, like "Picked up JAVA_TOOL_OPTIONS ..."*
- **JDK_JAVA_OPTIONS**
  - jdk 9+
  - gewinnt gegen java_tool_options
  - verliert gegen Command-Line-Args
  - im Gegensatz zu JAVA_TOOL_OPTIONS nur für `java`, nicht für `javac` oder `jar`
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
- **agentlib:jdwp**
  - für Debugging
  - `-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=<port>`
  - *It is not required to add the `address` parameter. If not provided the agent is selecting a random port number*
  - *For remote debugging one should run program with `*` in address: `address=*:<port>`*
  - *`suspend=y` : if 'y', tell the JVM to wait until debugger is attached to begin execution, otherwise (if 'n'), starts execution right away*
- **noverify**
  - *The JVM checks the byte code of the compile classes it is about to load to see that it is well behaved. This is an essential step for executing untrusted code. Unfortunately this takes time and for a very large application this may increase the startup time quite a bit. The "-noverify" flag turns this off.*
  - deprecated seit Java 13: *Users who need to run without startup verification can use AppCDS to archive their classes. The classes are verified during archiving and avoid verification at runtime.*
- **enableassertions**
  - alias `-ea`
- **disableassertions**
  - alias `-da`

### -D
- **sun.net.client.defaultConnectTimeout, sun.net.client.defaultReadTimeout**
  - *Modern applications use numerous protocols (i.e. SOAP, REST, HTTP, HTTPS, JDBC, RMI, etc.) to connect with remote applications. Sometimes remote applications might take a long time to respond. Sometimes they may not respond at all. If you don’t have proper timeout settings, and if remote applications don’t respond fast enough, then your application threads/resources will get stuck.*
  - *You can pass these two powerful timeout networking properties at the JVM level that can be globally applicable to all protocol handlers that uses java.net.URLConnection*
  - *By default, values for these two properties are -1, which means no timeout is set*
  - `-Dsun.net.client.defaultConnectTimeout=2000 -Dsun.net.client.defaultReadTimeout=2000`
  - beeinflusst offenbar nur URLConnection, aber nicht java.net.http.HttpClient
- **sun.zip.disableMemoryMapping**
  - true/false
  - entfernt in Java 9
- **sun.stdout.encoding**
- **sun.stderr.encoding**
- **user.timezone**
  - *you might be using java.util.Date or java.util.Calendar objects. These objects, by default, pick up time zone information from the underlying operating system. This will become a problem if your application is running in a distributed environment.*
  - `-Duser.timezone=US/Eastern`
- **user.language**
- **user.country**
- **java.endorsed.dirs**
  - *From time to time it is necessary to update the Java platform in order to incorporate newer versions of standards that are created outside of the Java Community Process (Endorsed Standards), or in order to update the version of a technology included in the platform to correspond to a later standalone version of that technology (Standalone Technologies). The Endorsed Standards Override Mechanism provides a means whereby later versions of classes and interfaces that implement Endorsed Standards or Standalone Technologies may be incorporated into the Java Platform.*
  - *If no value is set for java.endorsed.dirs, then Oracle's implementation of the Java platform looks for JAR files in a default standard location: Microsoft Windows: `<java-home>\lib\endorsed` / Solaris or Linux: `<java-home>/lib/endorsed`* 
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
  - *Keystore debugging, debugging for the PKIX, ...*
- **java.net.preferIPv4Stack**

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
- **log**
  - `-Xlog:gc:file=gc.txt`
  - `-Xlog:class+load:file=/path/to/classload.log`
- **mx**
  - `-Xmx64M`
- **ms**
  - `-Xms64M`
- **ss**
  - *set thread stack size*
  - *The stack is used to hold return addresses, function/method call arguments, etc.*
  - `-Xss256k`
  - *StackOverflowError: the stack size is greater than the limit*
  - `java -XX:+PrintFlagsFinal -version | grep ThreadStackSize` um den Wert rauszufinden
  - Default ist 1024k (*depends on your architecture and what not*)
  - *-XX:ThreadStackSize option means the same as -Xss*
  - <https://www.baeldung.com/jvm-configure-stack-sizes>
- **verify**
  - `-Xverify:none`
  - siehe -noverify
- **quickstart**
  - nur OpenJ9
  - *causes the JIT compiler to run with a subset of optimizations, which can improve the performance of short-running applications*

#### XX
- <https://www.baeldung.com/jvm-advanced-options>
- -XX = non-standard
- -XX:+Foo / -XX:-Foo für Boolean-Flags, -XX:Foo=Bar für Werte
<br/><br/>
- **ActiveProcessorCount**
  - `-XX:ActiveProcessorCount=<number>`
  - wirkt sich aus auf `Runtime.getRuntime().availableProcessors()` und damit ggf. auf Größen von best. Threadpools
- **+/-DebugNonSafepoints**
- **+/-ExitOnOutOfMemoryError**
  - *When you enable this option, the JVM exits on the first occurrence of an out-of-memory error. It can be used if you prefer restarting an instance of the JVM rather than handling out of memory errors.*
- **GCTimeRatio**
  - `-XX:GCTimeRatio=nnn`
  - *A hint to the virtual machine that it's desirable that not more than 1 / (1 + nnn) of the application execution time be spent in the collector.*
  - *By default the value is 99, meaning the application should get at least 99 times as much time as the collector. That is, the collector should run for not more than 1% of the total time.*
- **+/-HeapDumpOnOutOfMemoryError**
  - *tells the Java HotSpot VM to generate a heap dump when an allocation from the Java heap or the permanent generation cannot be satisfied*
- **HeapDumpPath**
  - *By default the heap dump is created in a file called java_pid.hprof in the working directory of the VM, as in the example above. You can specify an alternative file name or directory with the -XX:HeapDumpPath= option.*
  - *the JVM will NOT overwrite an existing heap dump in the HeapDumpPath, you'll see something similar to "Unable to create /tmp/java_pidpid.hprof: File exists" in your standard out*
  - `-XX:HeapDumpPath=/foo/bar`
- **InitialRAMPercentage**
- **MaxDirectMemorySize**
  - `MaxDirectMemorySize=10M` 
- **MaxMetaspaceSize**
  - `-XX:MaxMetaspaceSize=121289K`
- **MaxRAM**
  - *this parameter overrides the actual amount of physical RAM when calculating the heap limits basing on ergonomics*
  - *If `-Xmx?`  is set, `MaxRAM` is never used. Otherwise the maximum heap size is estimated as `MaxHeapSize = MaxRAM * MaxRAMPercentage / 100% (default MaxRAMPercentage=25)`*
  - *Note that this flag does not prevent JVM from allocating more memory than its value, but rather gives a hint "I know my physical RAM limit is X, please allocate within X", so JVM will share this value between Java heap and native memory. But if e.g. your application has native memory leak or classloader leak, then this limit will be reached anyway.*
- **MaxRAMFraction**
  - deprecated für `MaxRAMPercentage`
- **MaxRAMPercentage**
    - Default = 25
    - `Xmx = cgroup_mem_limit * MaxRAMPercentage / 100`
    - *If you set a value for `-Xmx` , the `-XX:MaxRAMPercentage` option is ignored.*
- **MaxJavaStackTraceDepth**
  - zur Laufzeit ändern: <https://gist.github.com/apangin/8a26a026efab87c5778fb89706f5712a>
- **MaxPermSize**
  - `-XX:MaxPermSize=64M`
- **NativeMemoryTracking**
  - *The Native Memory Tracking (NMT) is a Java HotSpot VM feature that tracks internal memory usage for a Java HotSpot VM.*
  - `NativeMemoryTracking=summary/detail/off`
  - *Enabling NMT causes a 5%-10% performance overhead*
  - <https://docs.oracle.com/en/java/javase/18/troubleshoot/diagnostic-tools.html#GUID-1F53A50E-86FF-491D-A023-8EC4F1D1AC77>
- **+/-PrintFlagsFinal**
  - *The PrintFlagsFinal flag, however, does not show all possible tuning flags. For instance, to also see diagnostic tuning flags, we should add the UnlockDiagnosticVMOptions flag*
- **+/-PrintNMTStatistics**
  - *obtain last memory usage data at VM exit when Native Memory Tracking is enabled*
  - `-XX:+UnlockDiagnosticVMOptions -XX:+PrintNMTStatistics`
  - <https://docs.oracle.com/javase/8/docs/technotes/guides/vm/nmt-8.html>
- **ReservedCodeCacheSize**
  - `-XX:ReservedCodeCacheSize=64M` 
- **showSettings:vm**
- **+/-StackTraceInThrowable**
- **+/-ShowCodeDetailsInExceptionMessages**
- **StartFlightRecording**
  - aktiviert JFR
  - `-XX:StartFlightRecording`
  - Options
    - dumponexit=true/false
    - filename=/path/to/file.jfr
- **+/-ShowHiddenFrames**
  - *enables or disables the display of generated hidden MethodHandle frames in a stack trace*
- **TieredCompilation**
  - *disable tiered compilation*  
- **TieredStopAtLevel**
  - beeinflusst Verhalten des JIT-Compilers
  - Levels
    - 0
      - Interpreted Code
      - <https://www.baeldung.com/jvm-tiered-compilation#1-level-0--interpreted-code>
    - 1
      - Limited C1 Compiled Code
      - auf Level 1 setzen für schnelle Startup-Zeit und weniger Memory (ggf. auf Kosten Throughput)
    - 2
    - 3
    - 4
  - `-XX:TieredStopAtLevel=1`
- **+/-UseStringDeduplication**
- **+/-UseBiasedLocking**
- **+/-UseParallelGC**
- **+/-UnlockDiagnosticVMOptions**
  - *The PrintFlagsFinal flag, however, does not show all possible tuning flags. For instance, to also see diagnostic tuning flags, we should add the UnlockDiagnosticVMOptions flag*
- **+/-UnlockExperimentalVMOptions**
  - *unlocks experimental JVM features. These features may be unstable and are therefore not available by default, so this flag is required to make them available.*
- **+/-UseContainerSupport**
  - *Starting from Java 10, this parameter (which is enabled by default) is used to make the JVM take the container memory limits into account when allocating the heap size, not the host machine configuration. This option was backported to Java 8.* 
  - *UseCGroupMemoryLimitForHeap VM option has been removed in JDK 11 and replaced with UseContainerSupport*

## Memory
- <https://www.baeldung.com/java-memory-beyond-heap>
- <https://dac.digital/netflix-on-java-a-non-heap-application-for-video-streaming>
  - Off-heap, ByteBuffer (im TB Bereich)
- *Besides heap, you have thread stacks, meta space, JIT code cache, native shared libraries and the off-heap store (direct allocations).*

### Heap
- *Bigger heap: the full GC will be longer. But it will occur less frequently. Smaller heap: the full GC will be quicker but will occur more frequently.*
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
- *The permanent space is where the classes, methods, internalized strings, and similar objects used by the VM are stored and never deallocated (hence the name).*
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
- *Peak "CodeCache" usage is often during application startup, going from 192 MB to 64 MB saves a lot of memory which can be used as heap. Applications that have a lot of active code during runtime (e.g. a web-application with a lot of endpoints) may need more "CodeCache". If "CodeCache" is too low, your application will use a lot of CPU without doing much (this can also manifest during startup: if "CodeCache" is too low, your application can take a very long time to startup).*

### Symbol
- *The JVM uses the Symbol area to store symbols such as field names, method signatures, and interned strings*
  
### Arena
- *This is unrelated to glibc arenas. In HotSpot, Arena is a structure for fast native memory allocation*
  
### Other
- *Every other memory usage that can't be categorized in the native memory area falls in this section. As an example, DirectByteBuffer usage is indirectly visible in this part.*

### GC
- <https://dzone.com/articles/interesting-garbage-collection-patterns>
- <https://www.reddit.com/r/java/comments/qlxopy/how_to_choose_the_best_java_garbage_collector/.compact>
- <https://www.virtuozzo.com/company/blog/tuning-garbage-collector-java-memory-usage-optimization/>

#### Caveats
- *The GC is unable to clear static fields unless the class that owns it is unloaded, which only happens if the Classloader that called it is garbage collected.*
- *Unclosed system resources: The GC indirectly frees up files since classes like FileInputStream are written such that if an instance is garbage collected, the ‘close()’ method will be called first. This way, unclosed system resources don’t always pose a risk, so a lot of developers tend to look over them.*
- *Unclosed connections: Like with unclosed resources, unclosed database or network connections can lead to significant memory use if not unloaded.*

#### Releasing memory back to OS
- *The HotSpot JVM does release memory back to the OS, but does so reluctantly since resizing the heap is expensive and it is assumed that if you needed that heap once you'll need it again.*
- *In general shrinking ability and behavior depends on the chosen garbage collector, the JVM version*
- *The JVM does release back memory under some circumstances, but (for performance reasons) this does not happen whenever some memory is garbage collected. It also depends on the JVM, OS, garbage collector etc.*
- *JDK 8 and earlier: There are no explicit options for prompt memory reclamation in these versions but you can make the GC more aggressive in general by setting `-XX:GCTimeRatio=19 -XX:MinHeapFreeRatio=20 -XX:MaxHeapFreeRatio=30` which will allow it to spend more CPU time on collecting and constrain the amount of allocated-but-unused heap memory after a GC cycle. If you're using a concurrent collector you can also set `-XX:InitiatingHeapOccupancyPercent=N` with N to some low value to let the GC run concurrent collections almost continuously, which will consume even more CPU cycles but shrink the heap sooner. This generally is not a good idea, but on some types of machines with lots of spare CPU cores but short on memory it can make sense. If you're using G1GC note that it only gained the ability to yield back unused chunks in the middle of the heap with jdk8u20, earlier versions were only able to return chunks at the end of the heap which put significant limits on how much could be reclaimed. If you're using a collector with a default pause time goal (e.g. CMS or G1) you can also relax that goal to place fewer constraints on the collector, or you can switch go the parallel collector to prioritize footprint over pause times. To verify that shrinking occurs or to diagnose why a GC decides not to shrink you can use GC Logging with `-XX:+PrintAdaptiveSizePolicy` may also provide insight, e.g. when the JVM tries to use more memory for the young generation to meet some goals.*
- *JDK 9 Added the `-XX:-ShrinkHeapInSteps` option which can be be used to apply the shrinking caused by the options mentioned in the previous section more aggressively. For logging `-XX:+PrintAdaptiveSizePolicy` has been replaced with `-Xlog:gc+ergo`*
- *JDK 12 introduced the option to enable prompt memory release for G1GC via the `G1PeriodicGCInterval`, again at the expense of some additional CPU. The JEP also mentions similar features in Shenandoah and the OpenJ9 VM.*
- *Since Java 12, G1 does this [shrinking] automatically if the application is idle. I recommend using these options combined with the above suggestion for a very compact resident process size: `-XX:+UseG1GC -XX:MaxHeapFreeRatio=30 -XX:MinHeapFreeRatio=10`*
- *ZGC released in 13 java and it can return unused heap memory to the operating system*
- <https://www.baeldung.com/gc-release-memory>


## Extension Mechanism
- `java.ext.dirs`
- *standard, scalable way to make custom APIs available to all applications running on the Java platform*
- *all applications using that JRE (or potentially all applications on the host) can see the same classes without need to explicitly specify them on the classpath*


## CDS & AppCDS

### Class-Data Sharing (CDS)
- <https://docs.oracle.com/en/java/javase/14/vm/class-data-sharing.html>
- [Performance auf der JVM: Überblick über CDS, AppCDS und AOT](https://entwickler.de/java/fast-and-furious-001)
- **share**
  - Für Class-Data Sharing (!= AppCDS). CDS existiert seit Java 5.
  - *erlaubt einen Dump der internen Repräsentation der beim Start geladenen [JRE-]Klassen in eine Datei [Windows: %JAVA_HOME%/bin/server/classes.jsa, Linux: lib/server/classes.jsa], die dann bei jedem Start der JVM, gesteuert über den JVM-Parameter `-Xshare:[on|off|auto|dump]`, geladen wird und das Laden der JARs überflüssig macht.*
  - `Xshare:dump`
    - erzeugt die Datei   
  - `Xshare:on`
    - *While class data sharing is enabled by default on JDK 12 and newer, explicitely enforcing it will ensure an error is raised if something is wrong, e.g. a mismatch of Java versions between building and using the archive*
    - *for testing purposes only. It may cause the VM to unexpectedly exit during start-up when the CDS archive cannot be used (for example, when certain VM parameters are changed, or when a different JDK is used). This option should not be used in production environments.*
    - benutzt die Datei
  - `Xshare:off`
  - `Xshare:auto`
    - *The default; enable class data sharing when jsa file is available*
  - <https://dev.java/learn/jvm/cds-appcds/>
- **SharedArchiveFile**
  - `-XX:SharedArchiveFile=/path/to/classes.jsa`
  - *specifies the path of the shared archive used with Class Data Sharing*
  - *When this option is used together with `-Xshare:dump` and `-XX:SharedClassListFile` then the JVM generates a new shared class data archive file at the path specified with -XX:SharedArchiveFile, using the list of classes specified by -XX:SharedClassListFile*
  - *When this option is used with `-Xshare:auto` or `-Xshare:on`, then the specified path is used to load the shared class data archive file to increase the startup speed of the Java application.*
- **DumpLoadedClassList**
  - `-XX:DumpLoadedClassList=/path/to/classes.lst`
  - *It produces an output file that lists the classes that were loaded during the execution of an application. Note that this option must be used together with -Xshare:off*
  - *The output class list can then be passed to -XX:SharedClassListFile to generate a shared class data archive for the application’s classes, which can substantially improve subsequent startup times of the application*
- **SharedClassListFile**
  - `-XX:SharedClassListFile=/path/to/classes.lst`

### Application Class-Data Sharing (AppCDS)
- *helps reduce the startup time for Java programming language applications, in particular smaller applications, as well as reduce footprint.*
- *allows a set of classes to be pre-processed into a shared archive file that can then be memory-mapped at runtime to reduce startup time which can also reduce dynamic memory footprint when multiple JVMs share the same archive file.*
- <https://simonis.github.io/cl4cds/> - *tool which helps exploring the new Application Class Data Sharing (AppCDS) feature in OpenJDK 10*
- <https://www.baeldung.com/java-10-performance-improvements#application-class-data-sharing>
- <https://www.morling.dev/blog/building-class-data-sharing-archives-with-apache-maven/>
- <https://github.com/ionutbalosin/faster-jvm-start-up-techniques/blob/main/app-dynamic-cds-hotspot/README.md>
- <https://github.com/SvenWoltmann/application-cds-demo>
- JDK 10
  - `+/-UseAppCDS` 
    - *made obsolete in JDK 11, expired in JDK 12* 
- JDK 12
  - Default CDS Archive
- JDK 13
  - Dynamic CDS Archive
  - `-XX:ArchiveClassesAtExit`
    - *Triggers creation of a AppCDS archive at the given location upon application shutdown*
    - *Only loaded classes will be added to the archive. As classloading on the JVM happens lazily, you must invoke some functionality in your application in order to cause all the relevant classes to be loaded.*
    - ```
      java -XX:ArchiveClassesAtExit=app-cds.jsa -jar your-app.jar
      java -Xlog:cds=debug:file=cds.log -Xshare:on -XX:SharedArchiveFile=app-cds.jsa -jar your-app.jar
      ```
- JDK 19
  - Autogenerate CDS Archive
    - `java -XX:+AutoCreateSharedArchive -XX:SharedArchiveFile=app.jsa -cp app.jar App`
    - *The specified archive file will be created if it does not exist, or if it was generated by a different JDK version.*
- Reihenfolge class loading: bootstrap, extensions, classpath
