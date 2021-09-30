---
tags: [Notebooks/Java]
title: Dies & das
created: '2019-02-14T20:40:29.485Z'
modified: '2021-06-04T09:01:00.378Z'
parent: Java
---

# Dies & das
- **JNI**
  - Java Native Interface
  - *bridge between the bytecode running in our JVM and the native code*
  - https://www.baeldung.com/jni
  - neuere Alternative: foreign linker api, jextract (jdk15)
- **JNA**
  - https://github.com/java-native-access/jna
  - *JNA provides Java programs easy access to native shared libraries without writing anything but Java code - no JNI or native code is required*
- **Process API**
  - https://www.baeldung.com/java-lang-processbuilder-api
- **Reflection**
  - Proxies
    - https://www.baeldung.com/java-dynamic-proxies
- **Bytecode-Manipulation**
  - HotswapAgent
  - ByteBuddy
    - *high level byte code manipulation, built on top of ASM*
    - auch als Agent erhältlich
    - https://bytebuddy.net/
    - Bsp: http interceptor: https://httptoolkit.tech/blog/how-to-intercept-debug-java-http/
  - cglib
- **Agents**
  - premain, class-redefinition, ...
  - https://jaxenter.de/james-bond-laesst-gruessen-28256
  - https://dzone.com/articles/jvm-advent-calendar-a-beginners-guide-to-java-agen (01/2020)
- **Instrumentation**
  - *Instrumentation is the process of adding extra code at runtime to an existing codebase in order to measure timings of different operations.*
- **AOP**
- **AnnotationProcessing API** (compiler)
  - [Das Annotation Processing API - Use Cases und Best Practices](@attachment/Praesentationen/2019-nn-gunnar_morling-das_annotation_processing_api_-_use_cases_und_best_practices-praesentation.pdf)
- **sun.misc.Unsafe**
  - https://www.javacodegeeks.com/2013/12/the-infamous-sun-misc-unsafe-explained.html
  - http://mishadoff.com/blog/java-magic-part-4-sun-dot-misc-dot-unsafe/
  - Objekt erzeugen ohne Konstruktoraufruf: `allocateInstance(Class<T> clazz)`
- **JavaPoet**
  - *Java API for generating .java source files*
  - https://github.com/square/javapoet
- **ServiceLoader**
  - https://www.logicbig.com/tutorials/core-java-tutorial/java-se-api/service-loader.html
- [https://blog.frankel.ch/hacking-third-party-api-jvm/](https://blog.frankel.ch/hacking-third-party-api-jvm/)
  - Beispiele für classpath shadowing, reflection, agent, aop