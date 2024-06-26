---
title: Build
parent: Java
---

# Build

## Annotation Processors, Compiler Plugins
- <https://github.com/gunnarmorling/awesome-annotation-processing>
- **jabel**
  - <https://github.com/bsideup/jabel>
  - *unlock Javac 12+ syntax when targeting Java 8*
  - Plugins für: Maven, Gradle, IntelliJ
- **Lombok**
  - <http://projectlombok.org>
  - <https://old.reddit.com/r/java/comments/170gdha/how_does_the_lombok_magic_work_underneath/>
- **manifold**
  - <https://github.com/manifold-systems/manifold>
  - xml/json/yaml-to-code, extension methods, operator overloading, metric unit expressions, type-safe reflection, type-safe equals(@self), number range, string templates, type-safe properties, ...
  - Plugins für IntelliJ IDEA and Android Studio


## Gradle
- <https://gradle.org>

### gradlew
  - *The recommended way to execute any Gradle build is with the help of the Gradle Wrapper. The Wrapper is a script that invokes a declared version of Gradle, downloading it beforehand if necessary. As a result, developers can get up and running with a Gradle project quickly without having to follow manual installation processes*
  - *the wrapper is downloaded once and added to source code repository*
  - <https://docs.gradle.org/current/userguide/gradle_wrapper.html>

### Plugins
- **Lombok**
- **Checkstyle**
  - <https://docs.gradle.org/current/userguide/checkstyle_plugin.html>
  - für Gradle 2.3: [https://docs.gradle.org/2.3/userguide/checkstyle_plugin.html](h)
- **FindBugs**
  - <https://docs.gradle.org/current/userguide/findbugs_plugin.html>
  - für Gradle 2.3: <https://docs.gradle.org/2.3/userguide/findbugs_plugin.html>
  - Html- statt Xml-Report: <https://stackoverflow.com/questions/15406469/how-to-generate-html-output-using-gradle-findbugs-plugin>
- **SpotBugs**
  - <https://spotbugs.readthedocs.io/en/stable/gradle.html>
  - erfordert Gradle 4+
- **application**
  - <https://docs.gradle.org/current/userguide/application_plugin.html>
  - *facilitates creating an executable JVM application. It makes it easy to start the application locally during development, and to package the application as a TAR and/or ZIP including operating system specific start scripts.*
  - *also implicitly applies the Java plugin*
  - *also implicitly applies the Distribution plugin*
  - Tasks
    - <https://docs.gradle.org/current/userguide/application_plugin.html#sec:application_tasks>
- **distribution**
- **jakartaee-migration**
  - <https://github.com/nebula-plugins/gradle-jakartaee-migration-plugin>
- **java**
  - <https://docs.gradle.org/current/userguide/java_plugin.html#java_plugin>
  - *adds Java compilation along with testing and bundling capabilities*
  - Tasks
    - <https://docs.gradle.org/current/userguide/java_plugin.html#sec:java_tasks>
- **modernizer**
  - *detecting use of legacy APIs which modern Java versions supersede*
  - <https://github.com/andygoossens/gradle-modernizer-plugin>
- **spring-boot**
  - <https://docs.spring.io/spring-boot/docs/current/gradle-plugin/reference/htmlsingle>
  - *generated "plain" artifacts: non-runnable*
- **task-tree**
  - *adds a 'taskTree' task that prints task dependency tree*
  - <https://github.com/dorongold/gradle-task-tree>
- **war**
  - <https://docs.gradle.org/current/userguide/war_plugin.html>
  - *extends the Java plugin to add support for assembling web application WAR files*
- **Kradle**
  - *sets up your Kotlin/JVM (or Java) project in no time*
  - *Bootstrap new projects, Run static code analysis, Run vulnerability scans, Create Docker images, ...*
  - <https://github.com/mrkuz/kradle#feature-java> 


## bld
- *allows you to write your build logic in pure Java*
- Plugin für Intellij
- <https://github.com/rife2/rife2/wiki/What-Is-Bld>
- <https://rife2.com/bld>


## Diverse
- **Proguard**
  - Shrinker und Obfuscator
  - <https://www.guardsquare.com/en/products/proguard>
- **Bazel**
- **R8**
  - <https://r8.googlesource.com/r8>
  - *a Proguard replacement for whole-program optimization, shrinking and minification*
- <https://www.reddit.com/r/java/comments/mql549/comparing_modernday_container_image_builders_jib>
  - jib, buildpacks, docker
- **Eclipse Transformer**
  - *The core problem that is introduced by Jakarta EE 9 is the renaming of package prefixes from javax to jakarta for APIs and properties. To solve this problem, the Open Liberty development team created the Eclipse Transformer.*
  - *you can use the Eclipse Transformer to update applications, test classes, and server configurations.*
  - <https://github.com/eclipse/transformer>
  - <https://github.com/eclipse/transformer/tree/main/maven-plugins/transformer-maven-plugin>
  - <https://openliberty.io/blog/2021/03/17/eclipse-transformer.html>


## Packaging
- **jpackage** (jdk 14; incubating)
  - *command-line tool to <mark>create native installers and packages</mark> for Java applications*
  - <https://www.baeldung.com/java14-jpackage>
  - *can wrap runtimes generated by jlink*
  - installmation
    - <https://github.com/SergeMerzliakov/installmation>
    - GUI für jpackage
    - Java 11+
    - <https://thickclient.blog/2019/12/23/installmation-an-installer-generator-for-java-11-apps>
- **jmod**
- **jlink**
  - jdk 9+
  - *generates a <mark>custom Java runtime image</mark> that contains only the platform modules that are required for a given application*
  - *contains only the modules we picked and the dependencies they need to function*
  - *can create launcher scripts (sh, bat)*
  - *use `jdeps` to see the list of JDK modules that the application uses*
- **Graal/native-image**
- **javapackager**
  - <https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javapackager.html>
  - *Performs tasks related to packaging and signing Java and JavaFX applications*
- **moditect**
  - *Currently the following tasks are supported:*
    - *Generating module-info.java descriptors for given artifacts (Maven dependencies or local JAR files)*
    - *Adding module descriptors to your project's JAR as well as existing JAR files (dependencies)*
    - *Creating module runtime images*
  - <https://github.com/moditect/moditect>
- **jdeploy**
  - *Deploy your app to Mac, Linux, and Windows users without the usual hassles.*
  - <https://www.jdeploy.com/>
  - <https://www.reddit.com/r/java/comments/sqbz69/deploy_java_desktop_apps_as_native_bundles_for/.compact>


## Release
- **jreleaser**
  - *takes inputs from popular builds tools (Ant, Maven, Gradle) such as JAR files, binary distributions (.zip, .tar), JLink images, or any other file that you’d like to publish as a Git release on popular Git services such as Github or Gitlab. Distribution files can additionally be published to be consumed by popular package managers as Homebrew, Snapcraft, or get ready to be launched via Jbang. Releases may be announced in a variety of channels such as Twitter, Zulip, or SDKMAN!*
  - <https://jreleaser.org>
