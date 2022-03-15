---
tags: [Notebooks/Java]
title: Dies & das
created: '2019-02-14T20:40:29.485Z'
modified: '2021-06-04T09:01:00.378Z'
parent: Java
---

# Dies & das
- [https://github.com/akullpp/awesome-java](https://github.com/akullpp/awesome-java)
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
    - https://www.baeldung.com/java-dynamic-proxies
- **Bytecode-Manipulation**
  - HotswapAgent
    - *Java unlimited redefinition of classes at runtime.*
    - *Each application framework (Spring, Hibernate, Logback, ...) needs a special reloading mechanism to keep up-to-date after class redefinition (e.g. Hibernate configuration reload after new entity class is introduced). Hotswap agent works as a plugin system and is shipped preconfigured with all major framework plugins. It is easy to write your custom plugin even as part of your application.*
    - <https://github.com/HotswapProjects/HotswapAgent> 
  - ByteBuddy
    - *high level byte code manipulation, built on top of ASM*
    - auch als Agent erhältlich
    - <https://bytebuddy.net/>
    - Beispiele
      - http interceptor: <https://httptoolkit.tech/blog/how-to-intercept-debug-java-http/>
      - log4j-jndi-be-gone: <https://github.com/nccgroup/log4j-jndi-be-gone> - *A Byte Buddy Java agent-based fix for CVE-2021-44228, the log4j 2.x "JNDI LDAP" vulnerability.*
  - cglib
    - *high level API to generate and transform Java byte code.*
    - *IMPORTANT NOTE: cglib is unmaintained and does not work well (or possibly at all?) in newer JDKs, particularly JDK17+. If you need to support newer JDKs, we will accept well-tested well-thought-out patches... but you'll probably have better luck migrating to something like ByteBuddy.* 
    - <https://github.com/cglib/cglib> 
    - <https://www.baeldung.com/cglib> 
  - javassist
    - *makes Java bytecode manipulation simple. It is a class library for editing bytecodes in Java; it enables Java programs to define a new class at runtime and to modify a class file when the JVM loads it.*
    - *Unlike other similar bytecode editors, Javassist provides two levels of API: source level and bytecode level.*
    - *If the users use the source- level API, they can edit a class file without knowledge of the specifications of the Java bytecode. The whole API is designed with only the vocabulary of the Java language. You can even specify inserted bytecode in the form of source text; Javassist compiles it on the fly.*
    - *On the other hand, the bytecode-level API allows the users to directly edit a class file as other editors.* 
    - <https://github.com/jboss-javassist/javassist> *3.4k
- **Agents**
  - premain, class-redefinition, ...
  - <https://jaxenter.de/james-bond-laesst-gruessen-28256>
  - <https://dzone.com/articles/jvm-advent-calendar-a-beginners-guide-to-java-agen> (01/2020)
  - hotpatch-for-apache-log4j2: <https://github.com/corretto/hotpatch-for-apache-log4j2> - *injects a Java agent into a running JVM process (...) will attempt to patch the lookup() method of all loaded org.apache.logging.log4j.core.lookup.JndiLookup instances*
  - <https://ivanyu.me/blog/2017/11/04/java-agents-javassist-and-byte-buddy/>
- **Instrumentation**
  - *Instrumentation is the process of adding extra code at runtime to an existing codebase in order to measure timings of different operations.*
- **AOP**
- **AnnotationProcessing API** (compiler)
- **sun.misc.Unsafe**
  - <https://www.javacodegeeks.com/2013/12/the-infamous-sun-misc-unsafe-explained.html>
  - <http://mishadoff.com/blog/java-magic-part-4-sun-dot-misc-dot-unsafe/>
  - Objekt erzeugen ohne Konstruktoraufruf: `allocateInstance(Class<T> clazz)`
- **JavaPoet**
  - *Java API for generating .java source files*
  - <https://github.com/square/javapoet>
  - <https://www.baeldung.com/java-poet>
- **ServiceLoader**
  - <https://www.logicbig.com/tutorials/core-java-tutorial/java-se-api/service-loader.html>
- [https://blog.frankel.ch/hacking-third-party-api-jvm/](https://blog.frankel.ch/hacking-third-party-api-jvm/)
  - Beispiele für classpath shadowing, reflection, agent, aop
- **Kotlin**
  - [https://kotlinlang.org/](https://kotlinlang.org/)


## Rule Engines (JSR 94)
- <https://www.oracle.com/technical-resources/articles/javase/javarule.html>
- <https://www.baeldung.com/java-rule-engines>
- Impls
  - Easy Rules
    - https://github.com/j-easy/easy-rules
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
    - https://www.tryjshell.org/
- **jbang**
  - *run self-contained source-only Java programs*
  - *be able to run java from anywhere without any or very minimal setup*
  - *Automatic fetching of any dependency*
  - *Java will automatically be downloaded when needed.*
  - <https://github.com/jbangdev/jbang>
  - <https://www.javaadvent.com/2021/12/jbang-gift-that-keeps-on-giving.html>
- **beanshell**
  - <https://github.com/beanshell/beanshell>


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
