---
title: Dies & das
parent: Java
---

# Dies & das
- <https://github.com/akullpp/awesome-java>
- <https://blog.frankel.ch/hacking-third-party-api-jvm/>
  - Beispiele für Classpath Shadowing, Reflection, Agent, AOP, Javassist
- <https://blog.frankel.ch/monkeypatching-java/>
  - java.lang.reflect.Proxy
  - Agents
  - AOP (AspectJ)
  - Java Compiler Plugins
  - <https://old.reddit.com/r/java/comments/16l57gg/monkeypatching_in_java/>
- **JNI**
  - Java Native Interface
  - *bridge between the bytecode running in our JVM and the native code*
  - <https://www.baeldung.com/jni>
  - neuere Alternative: foreign linker api, jextract (jdk15)
- **JNA**
  - <https://github.com/java-native-access/jna>
  - *JNA provides Java programs easy access to native shared libraries without writing anything but Java code - no JNI or native code is required*
- **Process API**
  - <https://www.baeldung.com/java-lang-processbuilder-api>
- **Reflection**
  - Proxies
    - <https://www.baeldung.com/java-dynamic-proxies>
- **AnnotationProcessing API** (compiler)
  - <https://old.reddit.com/r/java/comments/y24k1z/build_your_own_framework_using_an_annotation/.compact> 
- **sun.misc.Unsafe**
  - <https://www.javacodegeeks.com/2013/12/the-infamous-sun-misc-unsafe-explained.html>
  - <http://mishadoff.com/blog/java-magic-part-4-sun-dot-misc-dot-unsafe/>
  - <https://www.baeldung.com/java-unsafe>
  - Objekt erzeugen ohne Konstruktoraufruf: `allocateInstance(Class<T> clazz)`
- **JavaPoet**
  - *Java API for generating .java source files*
  - <https://github.com/square/javapoet>
  - <https://www.baeldung.com/java-poet>
- **ServiceLoader**
  - <https://www.logicbig.com/tutorials/core-java-tutorial/java-se-api/service-loader.html>
- **Kotlin**
  - <https://kotlinlang.org/>
- **Project Leyden**
  - <https://blogs.oracle.com/javamagazine/post/java-leyden-static-images>
    - *plans to address Java’s slow startup time and slow time to peak performance via static images*
    - *A static image is a standalone program, derived from an application and a JDK, which runs that application — and no other.*
    - *We will lean heavily on existing components of the JDK including the HotSpot JVM, the C2 compiler, application class-data sharing (CDS), and the jlink linking tool.*
- **assert**
  - <https://www.baeldung.com/java-assert>
- **Attach API**
  - *provides a mechanism to attach to a Java virtual machine*
  - <https://docs.oracle.com/javase/8/docs/technotes/guides/attach/>
- **jattach**
  - *utility to send commands to a JVM process via Dynamic Attach mechanism.*
  - *All-in-one jmap + jstack + jcmd + jinfo functionality in a single tiny program.*
  - *No installed JDK required, works with just JRE. Supports Linux containers.*
  - *This is the lightweight native version of HotSpot Attach API*
  - *Supported commands:<br/>
load : load agent library<br/>
threaddump : dump all stack traces (like jstack)<br/>
dumpheap : dump heap (like jmap)<br/>
jcmd : execute jcmd command
...*
  - <https://github.com/jattach/jattach>


## Bytecode-Manipulation, Agents, Instrumentation
- *Instrumentation is the process of adding extra code at runtime to an existing codebase in order to measure timings of different operations.*
- **HotswapAgent**
  - *Java unlimited redefinition of classes at runtime.*
  - *Each application framework (Spring, Hibernate, Logback, ...) needs a special reloading mechanism to keep up-to-date after class redefinition (e.g. Hibernate configuration reload after new entity class is introduced). Hotswap agent works as a plugin system and is shipped preconfigured with all major framework plugins. It is easy to write your custom plugin even as part of your application.*
  - <https://github.com/HotswapProjects/HotswapAgent> 
- **Agents**
  - Static
    - *statically load the agent using `-javaagent` parameter at JVM startup*
    - *need to define `premain` method*
  - Dynamic
    - *can be injected [into a running JVM] with HotSpot Attach API. Run the following snippet with $JAVA_HOME/lib/tools.jar on the class path. `VirtualMachine vm = VirtualMachine.attach(PID)` ...*
    - *need to declare an `agentmain(String, Instrumentation)` method which is executed upon attachment within the target VM*
    - *can however use a library like byte-buddy-agent which contains different implementations for different VMs. An attachment can be done using: ByteBuddyAgent.attach("my.jar", "my-pid");
This attaches the agent contained in my.jar onto the Java process with id my-id.* 
  - <https://jaxenter.de/james-bond-laesst-gruessen-28256>
  - <https://dzone.com/articles/jvm-advent-calendar-a-beginners-guide-to-java-agen> (01/2020)
  - hotpatch-for-apache-log4j2: <https://github.com/corretto/hotpatch-for-apache-log4j2> - *injects a Java agent into a running JVM process (...) will attempt to patch the lookup() method of all loaded org.apache.logging.log4j.core.lookup.JndiLookup instances*
  - <https://ivanyu.me/blog/2017/11/04/java-agents-javassist-and-byte-buddy/>
  - <https://www.baeldung.com/java-instrumentation>
  - <https://www.youtube.com/watch?v=ZrGOv44iTC8> - *The Java Agent: Modifying Bytecode at Runtime to Protect Against Log4J • Joe Beeton • GOTO 2022*
- -> Java/Libs/Reflection & Bytecode


## Rule Engines (JSR 94)
- <https://www.oracle.com/technical-resources/articles/javase/javarule.html>
- <https://www.baeldung.com/java-rule-engines>
- Impls
  - Easy Rules
    - <https://github.com/j-easy/easy-rules>
  - Drools → Frameworks/Business Process
  - Evrete
    - *lightweight alternative to the Drools Rule Engine*
    - <https://www.baeldung.com/java-evrete-rule-engine>


## Scripting
- **single file** (java 11+)
  - unterstützt "shebang"; `#!/usr/local/bin/java --source 11`
  - <https://www.baeldung.com/java-single-file-source-code>
- **jshell** (java 9+)
  - tryjshell
    - <https://www.tryjshell.org/>
- **jbang**
  - *run self-contained source-only Java programs*
  - *be able to run java from anywhere without any or very minimal setup*
  - *Automatic fetching of any dependency*
  - *Java will automatically be downloaded when needed.*
  - <https://github.com/jbangdev/jbang>
  - <https://www.javaadvent.com/2021/12/jbang-gift-that-keeps-on-giving.html>
  - <http://www.mastertheboss.com/java/jbang-vs-jshell/>
- **beanshell**
  - <https://github.com/beanshell/beanshell>
- **JavaFiddle**
  - <https://javafiddle.leaningtech.com/> 


## Dokumentation
- **java2uml**
  - <http://www.java2uml.com/>
  - macht per drag-and-drop aus Java-Klassen UML-Diagramme


## i18n
- **java.util.ResourceBundle**
  - ResourceBundle.getBundle liefert ein PropertyResourceBundle. Dieses ResourceBundle geht intern davon aus, dass die .properties-Datei
    ISO-8859-1-formatiert ist. Bei einer UTF-8-formatierten Datei braucht es einen Workaround: <https://stackoverflow.com/questions/4659929/how-to-use-utf-8-in-resource-properties-with-resourcebundle>
  - List- und PropertyResourceBundle sind thread-safe
  - getBundle liefert gecachte Instanzen (Caching ist konfigurierbar)
  - <https://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html>
  - → Libs/YamlResourceBundle
- **java.text.MessageFormat**
  - <https://docs.oracle.com/javase/7/docs/api/java/text/MessageFormat.html>
- **localizer**
  - *Type-safe localization message acces*
  - ```java
    // messages.properties: foo=error at {0} with {1}
    // =>
    public static String foo(Object arg1, Object arg2) { ... }
    ```
  - Maven-Plugin
  - <https://github.com/kohsuke/localizer>


## Datum & Zeit
- -> Diverses/Datum & Zeit
- <u>Zeitstempel</u>
  - **java.time.Instant**
  - **System.currentTimeMillis()**
  - **java.sql.Timestamp**
    - *A thin wrapper around java.util.Date that allows the JDBC API to identify this as an SQL TIMESTAMP value*
    - ´Timestamp(long time)` *Constructs a Timestamp object using a milliseconds time value.*
    - `Instant toInstant()`
    - <https://docs.oracle.com/javase/8/docs/api/java/sql/Timestamp.html>
   
## File
- java.nio.file.Files
- RandomAccessFile
- MapedByteBuffer & FileChannel (Memory-mapped file)
   - <https://bito.ai/resources/java-memory-mapped-file-java-explained/>
   - <https://medium.com/@trunghuynh/java-nio-using-memory-mapped-file-to-load-big-data-into-applications-5058b395cc9d>
   - <https://medium.com/globant/memory-mapped-files-and-mappedbytebuffers-in-java-4e5819605b20>
- ByteBuffer
  - <https://www.baeldung.com/java-bytebuffer>
- java.util.Scanner
