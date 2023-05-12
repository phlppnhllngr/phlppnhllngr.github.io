---
title: Dies & das
parent: Java
---

# Dies & das
- <https://github.com/akullpp/awesome-java>
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
  - <https://blog.frankel.ch/hacking-third-party-api-jvm/>
  - Beispiele für classpath shadowing, reflection, agent, aop
- **Kotlin**
  - <https://kotlinlang.org/>
- **Class Data Sharing**
  - <https://docs.oracle.com/en/java/javase/14/vm/class-data-sharing.html>
  - [Performance auf der JVM: Überblick über CDS, AppCDS und AOT](https://entwickler.de/java/fast-and-furious-001)
  - AppCDS
    - Application Class-Data Sharing
    - *helps reduce the startup time for Java programming language applications, in particular smaller applications, as well as reduce footprint.*
    - *allows a set of classes to be pre-processed into a shared archive file that can then be memory-mapped at runtime to reduce startup time which can also reduce dynamic memory footprint when multiple JVMs share the same archive file.*
    - <https://simonis.github.io/cl4cds/> - *tool which helps exploring the new Application Class Data Sharing (AppCDS) feature in OpenJDK 10*
    - <https://www.baeldung.com/java-10-performance-improvements#application-class-data-sharing>
    - <https://www.morling.dev/blog/building-class-data-sharing-archives-with-apache-maven/>
    - <https://github.com/ionutbalosin/faster-jvm-start-up-techniques/blob/main/app-dynamic-cds-hotspot/README.md>
    - <https://github.com/SvenWoltmann/application-cds-demo>
- **Project Leyden**
  - <https://blogs.oracle.com/javamagazine/post/java-leyden-static-images>
    - *plans to address Java’s slow startup time and slow time to peak performance via static images*
    - *A static image is a standalone program, derived from an application and a JDK, which runs that application — and no other.*
    - *We will lean heavily on existing components of the JDK including the HotSpot JVM, the C2 compiler, application class-data sharing (CDS), and the jlink linking tool.*
- **CRaC**
  - Coordinated Restore at Checkpoint
  - <https://foojay.io/today/how-to-run-a-java-application-with-crac-in-a-docker-container/>
    - *developed by Azul to solve the problem of "slow" startup times of the Java Virtual Machine in a microservice environment.*
    - *When the JVM runs your application code, it does things like interpreting, compiling and optimizing code to make your application run as fast as possible under the given workload. This is great but can take some time and especially when you run short lived microservices you don't want to wait until the JVM has produced the most optimized code.*
    - *The checkpoint-restore mechanism is nothing new and most of you already know and use it daily. If you work on your laptop and close the lid, the operating systems detects that an stores it's current state to disk. Once you open up the lid again, the operating system restores the saved state from disk.
  CRaC provides the same mechanism but for the JVM and your running application.*
- **assert**
  - <https://www.baeldung.com/java-assert>


## Bytecode-Manipulation, Agents, Instrumentation
- *Instrumentation is the process of adding extra code at runtime to an existing codebase in order to measure timings of different operations.*
- **HotswapAgent**
  - *Java unlimited redefinition of classes at runtime.*
  - *Each application framework (Spring, Hibernate, Logback, ...) needs a special reloading mechanism to keep up-to-date after class redefinition (e.g. Hibernate configuration reload after new entity class is introduced). Hotswap agent works as a plugin system and is shipped preconfigured with all major framework plugins. It is easy to write your custom plugin even as part of your application.*
  - <https://github.com/HotswapProjects/HotswapAgent> 
- **Agents**
  - premain, class-redefinition, ...
  - <https://jaxenter.de/james-bond-laesst-gruessen-28256>
  - <https://dzone.com/articles/jvm-advent-calendar-a-beginners-guide-to-java-agen> (01/2020)
  - hotpatch-for-apache-log4j2: <https://github.com/corretto/hotpatch-for-apache-log4j2> - *injects a Java agent into a running JVM process (...) will attempt to patch the lookup() method of all loaded org.apache.logging.log4j.core.lookup.JndiLookup instances*
  - <https://ivanyu.me/blog/2017/11/04/java-agents-javassist-and-byte-buddy/>
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
