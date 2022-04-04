---
tags: [Notebooks/Java]
title: Graal
created: '2021-02-14T15:24:51.328Z'
modified: '2021-05-17T14:17:22.063Z'
parent: Java
---

# Graal
- <https://www.graalvm.org/>
- <https://github.com/oracle/graal>
- *a high-performance multilingual runtime*
- *possible to mix multiple programming languages in a single application*
- java, js, ruby, ...
- <https://www.graalvm.org/reference-manual/native-image/>
- <https://www.graalvm.org/docs/getting-started/#native-images>
- <https://medium.com/graalvm/graalvm-quick-reference-b8d1dfe24241>
- <Docker
  - <https://blogs.oracle.com/developers/building-cross-platform-native-images-with-graalvm>
  - <https://www.graalvm.org/docs/getting-started/container-images/>


## native-image
<img src="https://miro.medium.com/max/1000/1*_DVpea8yyxx39T4cLCTquQ.png" loading="lazy"/>
- AoT-compiled => native Anwendung
- *These performance benefits come from precompiling the code of your application ahead-of-time and initializing some classes of the application in advance. So when the applications starts — it is ready to do useful work and doesn’t need the infrastructure for dealing with bytecode loading, interpretation, compiling it with the just-in-time compiler and so on.
Most importantly though, the executables built with Native Image are standalone and don’t depend on the JVM for the execution because the necessary runtime components, like the garbage collector, are built into the same binary. Also, because of the inclusion of the preinitialized heap data and the compiled code of the whole applications, the binaries are typically larger than the JAR files.*
- native-image nimmt app.jar, deps.jar, rt.jar, führt eine Analyse durch und entfernt ungebrauchten Code, und erzeugt dann ein native executable (mit graal-compiler)
- läuft dann nicht im JVM, sondern in einer embedded "Substrate VM" (gc, thread scheduler, ...)
- wenn die `glibc`-Implementierung ("GNU C Library") der Build-Maschine eine andere ist, als die der Maschine, auf das Image läuft, muss mit `--static` compiled werden (Bsp.: oracle/graalvm-docker für Build, alpine-docker für App)
- hat Limitationen (Reflection, static initializers, ...)
  - <https://www.graalvm.org/reference-manual/native-image/Limitations/>
  - <https://github.com/oracle/graal/blob/master/substratevm/BuildConfiguration.md>
    - <https://github.com/oracle/graal/blob/master/substratevm/BuildConfiguration.md#assisted-configuration-of-native-image-builds>
  - Reflection
    - Graal versucht beim Compilen rauszufinden, welche Klassen per Reflection verwendet werden. Wenn das nicht gelingt, muss man selbst konfigurieren
    - <https://github.com/oracle/graal/blob/master/substratevm/Reflection.md>
    - ```json
      {
        "name" : "java.lang.Class",
        "allDeclaredConstructors" : true,
        "allPublicConstructors" : true,
        "allDeclaredMethods" : true,
        "allPublicMethods" : true,
        "allDeclaredClasses" : true,
        "allPublicClasses" : true
      },
      {
        "name" : "java.lang.String",
        "fields" : [
          { "name" : "value", "allowWrite" : true },
          { "name" : "hash" }
        ],
        "methods" : [
          { "name" : "<init>", "parameterTypes" : [] },
          { "name" : "<init>", "parameterTypes" : ["char[]"] },
          { "name" : "charAt" },
          { "name" : "format", "parameterTypes" : ["java.lang.String", "java.lang.Object[]"] }
        ]
      }
    ```
  - Resources
    - bei Resources gibt es keine automatische Erkennung. Alle müssen manuell/explizit genannt werden (aber: siehe assisted configuration oben).
    - in den Beispielen werden die glob-patterns z.B. als "*/test.txt$" angegeben (Datei in src/main/resources), was aber anscheinend nur funktioniert: "test.txt"
    - <https://github.com/oracle/graal/blob/master/substratevm/Resources.md>
- nur Java 8 & 11 (Stand 06/20)
- Tools
  - Maven-Plugin → Java/Maven
  - graalvm dashboard
    - *web-based visualization tool to help make sense of the information on methods compilation, reachability, class usability, profiling data, preinitialized heap data and the static analysis results. In other words, you can monitor what classes, packages, and preinitialized objects fill up the executable, see how much space certain package occupies, and what classes objects take most of the heap. All this data is very helpful at understanding how to optimize the application to make its binary even smaller.* (<https://medium.com/graalvm/making-sense-of-native-image-contents-741a688dab4d>)
    - <https://www.graalvm.org/docs/tools/dashboard/?ojr=dashboard>
  - Liberica Native Image Kit
    - *utility for making native images for the JVM, letting you compile applications to executables using the GraalVM native-image compiler.*
    - *why just not use the GraalVM toolkit directly? As with Spring Native, NIK in essence is a layer over GraalVM which makes interfacing with it much easier by taking care of the necessary configuration out of the box.*
    - <https://www.i-programmer.info/news/80-java/15284-making-graalvm-based-executables-easy.html>

