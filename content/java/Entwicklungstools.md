---
tags: [Notebooks/Java]
title: Entwicklungstools
created: '2019-02-05T10:25:02.900Z'
modified: '2021-09-13T12:48:59.168Z'
parent: Java
---

# Entwicklungstools

## Linter, statische Codeanalyse
- **SpotBugs**
  - https://spotbugs.github.io/
  - https://github.com/spotbugs/spotbugs ⭐1500
  - Plugins für Eclipse und Maven
  - https://github.com/KengoTODA/findbugs-slf4j - *A SpotBugs/FindBugs plugin to verify usage of SLF4J*
- **SonarLint**
  - https://www.sonarlint.org/
  - Regeln für Java und viele andere Sprachen. (Optional:) Bezieht Regeln von einem SonarQube-Server. SonarQube gibt es z.B. als Docker-Image: https://docs.docker.com/samples/library/sonarqube/
  - Ohne SonarQube-Server sind die Regeln nicht konfigurierbar.
  - Regeln: https://rules.sonarsource.com/java
  - Plugins für Eclipse, VS Code
- **Checkstyle**
  - https://checkstyle.org
  - https://github.com/checkstyle/checkstyle ⭐4900
  - konfigurierbare Linter-Regeln
  - Übersicht Regeln: https://checkstyle.org/checks.html
  - Tooling
    - Plugins für IDEs, Maven, Gradle, Jenkins etc: https://checkstyle.org/index.html#Related_Tools
    - https://github.com/sevntu-checkstyle/sevntu.checkstyle
      - *Additional Checkstyle checks*
  - Konfigs von Sun & Google: https://checkstyle.org/style_configs.html (nicht erweiterbar)
  - eigene Regeln und Ignores möglich
- **PMD**
  - https://pmd.github.io
  - https://github.com/pmd/pmd ⭐2500
- **ErrorProne**
  - https://github.com/google/error-prone ⭐4800
  - https://errorprone.info/index
  - Integration mit Bazel, Maven, Gradle
  - gut konfigurierbar (eigene Regeln mit Java-Code definierbar)
  - mit ErrorProne kann auch eine gesamte Codebase refactored werden: https://errorprone.info/docs/refaster
  - Plugins
    - NullAway
      - *compile time null checks/warnings*
      - https://github.com/uber/NullAway
- **semgrep**
  - *static analysis tool that finds bugs and enforces code standards at editor, commit, and CI time. Precise rules look like the code you’re searching; no more traversing abstract syntax trees, wrestling with regexes, or using a painful DSL. Code analysis is performed locally (code is not uploaded) and Semgrep runs on uncompiled code.*
  - *Go · Java · JavaScript · JSX · JSON · Python · Ruby · TypeScript · TSX*
  - https://github.com/returntocorp/semgrep
- **policeman's forbidden api checker**
  - *find invocations of method/class/field signatures and fail build*
  - https://github.com/policeman-tools/forbidden-apis
  - Maven- & Gradle-Plugin
- **UCDetector (unnecessary code detector)**
  - *eclipse PlugIn tool to find unnecessary (dead) public java code*
  - http://www.ucdetector.org/
- **coala**
  - *unified command-line interface for linting and fixing all your code, regardless of the programming languages*
  - *Python, C/C++, Java, JavaScript, CSS, and several others out of the box*
  - https://github.com/coala/coala/ ⭐3.2k


## Visualisierung von Projektabhängigkeiten etc.
- **Tattletale**
  - [https://tattletale.jboss.org/](https://tattletale.jboss.org/)
  - *can help you get an overview of the project you are working on or a product that you depend on*
  - *will provide you with reports that can help you Find missing classes from the classpath, Find similar JAR files that have different version numbers, Find unused JAR archives, ...*
- **sourcetrail**
  - [https://github.com/CoatiSoftware/Sourcetrail](https://github.com/CoatiSoftware/Sourcetrail)
  - [https://www.sourcetrail.com/#intro](https://www.sourcetrail.com/#intro)
  - *source explorer that helps you get productive on unfamiliar source code*
  - *supporting C, C++, Java and Python*
- **Flow**
  - *Record your application executions and visualize what happened at runtime through an interactive web interface*
  - Als Intellij-Plugin oder Standalone
  - http://findtheflow.io/
- **appmap**
  - https://appland.com/products/appmap
  - https://www.reddit.com/r/java/comments/mbjomm/visualize_the_architecture_of_your_java_app_in_vs/
  - Plugins für VSCode, Intellij, Maven
- **revapi**
  - *an API analysis and change tracking tool*
  - analysiert java, json, yaml, ...
  - *as a sneak peak consider the following detected changes: checked exception added/removed to/from method signature / formal type parameter added to class / non-final method replaced by a final method in superclass*
  - [https://github.com/revapi/revapi](https://github.com/revapi/revapi) ⭐126


## Formatter
- **google-java-format**
  - https://github.com/google/google-java-format
  - Eclipse- & Maven-Plugins
- **prettier-java**
  - *opinionated code formatter. It enforces a consistent style by parsing your code and re-printing it with its own rules*
  - https://github.com/jhipster/prettier-java
  - node_module & Maven-Plugin (→ maven/plugins)
- **spotless**
  - import order, unused imports, indentation, ...
  - Wrapper um prettier/google-format/eclipse-jdt (?)
  - Maven-Plugin → maven/spotless-plugin
- **uncrustify**
  - *A source code beautifier for C, C++, C#, ObjectiveC, D, Java, Pawn and VALA*
  - https://github.com/uncrustify/uncrustify


## Diverse
- **sdkman**
  - <https://sdkman.io/>
  - versch. Versionen von JDK, Maven, ... verwalten
  - für Linux. Windows: nur mit git bash
- **update4j**
  - https://github.com/update4j/update4j
  - *first auto-update and launcher library designed for Java 9+. Easily host your application files anywhere (even Google Drive, Dropbox, Amazon S3, or Maven Central) and you can synchronize them with all your distributed applications. You can use any protocol you wish to retrieve those files and may be protected under authenticated API.*
- **jrebel**
  - *can skip rebuilds and redeploys during Java development -- while maintaining application state*
  - kostet Geld
  - <https://www.jrebel.com/products/jrebel/>
- **jenv**
  - <https://github.com/jenv/jenv/>
  - *lets you switch between java versions. However, this project does not install java for you*
  - *jEnv supports the notion of a global JDK and multiple local JDKs. The global JDK is the JDK that will be used if we type java into the command line anywhere on our computer. A local JDK is a JDK that is configured for a specific folder only. If we type java into the command line in this folder, it will not use the global JDK, but the local JDK instead.*
  - Extra plugin für Maven und Gradle nötig
  - Linux & MacOS. Windows: nur mit WSL oder git bash
- **bugjail**
  - https://bugjail.com/
- **remote debugging**
  - https://stackify.com/java-remote-debugging/
  - https://www.rookout.com/blog/remote-java-debugging
- **hotswap agent**
  - https://github.com/HotswapProjects/HotswapAgent
  - *unlimited redefinition of classes at runtime*
  - *main purpose of this project used to be avoiding of infamous change code->restart and wait...->check development lifecycle*
  - *Each application framework (Spring, Hibernate, Logback, ...) needs special reloading mechanism to keep up-to-date after class redefinition (e.g. Hibernate configuration reload after new entity class is introduced). Hotswap agent works as a plugin system and ships preconfigured with all major framework plugins.*
- **j2cl**
  - *transpiler from Java to Closure style JavaScript*
  - https://github.com/google/j2cl
- **OpenRewrite**
  - *mass refactoring ecosystem for Java and other source code*
  - *Migrate to Java 11 from Java 8, Migrate to JUnit 5 from JUnit 4, Migrate to SLF4J from Log4j*
  - <https://github.com/openrewrite/rewrite/>
