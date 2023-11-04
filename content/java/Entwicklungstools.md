---
title: Entwicklungstools
parent: Java
---

# Entwicklungstools

## Linter, statische Codeanalyse
- **SpotBugs**
  - <https://spotbugs.github.io/>
  - <https://github.com/spotbugs/spotbugs> <img loading="lazy" src="https://img.shields.io/github/stars/spotbugs/spotbugs?style=flat-square">
  - Integration mit Eclipse und Maven
  - Extensions
    - <https://spotbugs.github.io/#extensions>
    - <https://github.com/KengoTODA/findbugs-slf4j> - *A SpotBugs/FindBugs plugin to verify usage of SLF4J*
- **SonarLint**
  - <https://www.sonarlint.org/>
  - Regeln für Java und viele andere Sprachen. (Optional:) Bezieht Regeln von einem SonarQube-Server.
  - Ohne SonarQube-Server sind die Regeln nicht konfigurierbar.
  - Regeln: <https://rules.sonarsource.com/java>
  - Plugins für Eclipse, VS Code
- **SonarQube**
  - <https://docs.sonarqube.org/latest/>
  - <https://github.com/mc1arke/sonarqube-community-branch-plugin>
- **Checkstyle**
  - <https://checkstyle.org>
  - <https://github.com/checkstyle/checkstyle> <img loading="lazy" src="https://img.shields.io/github/stars/checkstyle/checkstyle?style=flat-square">
  - konfigurierbare Linter-Regeln
  - Übersicht Regeln: <https://checkstyle.org/checks.html>
  - Tooling
    - Plugins für IDEs, Maven, Gradle, Jenkins etc: <https://checkstyle.org/index.html#Related_Tools>
    - <https://github.com/sevntu-checkstyle/sevntu.checkstyle>
      - *Additional Checkstyle checks*
  - Konfigs von Sun & Google: <https://checkstyle.org/style_configs.html> (nicht erweiterbar)
  - eigene Regeln und Ignores möglich
- **PMD**
  - *source code analyzer. It finds common programming flaws like unused variables, empty catch blocks, unnecessary object creation, and so forth. It supports many languages. It can be extended with custom rules* 
  - <https://pmd.github.io>
  - <https://github.com/pmd/pmd> <img loading="lazy" src="https://img.shields.io/github/stars/pmd/pmd?style=flat-square">
  - Eclipse-Plugin
- **ErrorProne**
  - <https://github.com/google/error-prone> <img loading="lazy" src="https://img.shields.io/github/stars/google/error-prone?style=flat-square">
  - <https://errorprone.info/index>
  - Integration mit Bazel, Maven, Gradle
  - gut konfigurierbar (eigene Regeln mit Java-Code definierbar)
  - mit ErrorProne kann auch eine gesamte Codebase refactored werden: <https://errorprone.info/docs/refaster>
  - Plugins
    - NullAway
      - *compile time null checks/warnings*
      - <https://github.com/uber/NullAway>
- **semgrep**
  - *static analysis tool that finds bugs and enforces code standards at editor, commit, and CI time. Precise rules look like the code you’re searching; no more traversing abstract syntax trees, wrestling with regexes, or using a painful DSL. Code analysis is performed locally (code is not uploaded) and Semgrep runs on uncompiled code.*
  - *Go · Java · JavaScript · JSX · JSON · Python · Ruby · TypeScript · TSX*
  - <https://github.com/returntocorp/semgrep>
- **policeman's forbidden api checker**
  - *find invocations of method/class/field signatures and fail build*
  - <https://github.com/policeman-tools/forbidden-apis>
  - Maven- & Gradle-Plugin
- **UCDetector (unnecessary code detector)**
  - *eclipse PlugIn tool to find unnecessary (dead) public java code*
  - <http://www.ucdetector.org/>
- **coala**
  - *unified command-line interface for linting and fixing all your code, regardless of the programming languages*
  - *Python, C/C++, Java, JavaScript, CSS, and several others out of the box*
  - inaktiv seit 2021
  - <https://github.com/coala/coala/> <img loading="lazy" src="https://img.shields.io/github/stars/coala/coala?style=flat-square">
- **infer**
  - *static analysis tool - if you give Infer some Java or C/C++/Objective-C code it produces a list of potential bugs*
  - *can run Infer with a variety of build systems (...) Gradle, Maven, Other build systems*
  - <https://fbinfer.com/docs/hello-world>


## Dynamische Analyse
- **Digma**
  - *continually analyzing observability sources and providing feedback during development* 
  - Stand 10/23 nur als Intellij-Plugin verfügbar 
  - <https://github.com/digma-ai/digma> <img loading="lazy" src="https://img.shields.io/github/stars/digma-ai/digma?style=flat-square">
  - [YT - Continuous Code Feedback with OpenTelemetry and Digma By Roni Dover - 10/2023](https://www.youtube.com/watch?v=Tyv79hhaL6c)
  - OTEL-Extension: <https://foojay.io/today/observing-java-applications-running-via-docker-compose-using-opentelemetry/>


## Visualisierung von Projektabhängigkeiten etc.
- **Tattletale**
  - <https://tattletale.jboss.org/>
  - *can help you get an overview of the project you are working on or a product that you depend on*
  - *will provide you with reports that can help you Find missing classes from the classpath, Find similar JAR files that have different version numbers, Find unused JAR archives, ...*
- **sourcetrail**
  - Entwicklung eingestellt September '21 
  - <https://github.com/CoatiSoftware/Sourcetrail>
  - <https://www.sourcetrail.com/#intro>
  - *source explorer that helps you get productive on unfamiliar source code*
  - *supporting C, C++, Java and Python*
- **Flow**
  - *Record your application executions and visualize what happened at runtime through an interactive web interface*
  - Als Intellij-Plugin oder Standalone
  - <http://findtheflow.io/>
- **appmap**
  - <https://appland.com/products/appmap>
  - <https://www.reddit.com/r/java/comments/mbjomm/visualize_the_architecture_of_your_java_app_in_vs/>
  - Plugins für VSCode, Intellij, Maven
- **revapi**
  - *an API analysis and change tracking tool*
  - analysiert java, json, yaml, ...
  - *as a sneak peak consider the following detected changes: checked exception added/removed to/from method signature / formal type parameter added to class / non-final method replaced by a final method in superclass*
  - <https://github.com/revapi/revapi> <img loading="lazy" src="https://img.shields.io/github/stars/revapi/revapi?style=flat-square">
- **sourcegraph**
  - *Search all of your repositories across all branches and all code hosts. Navigate code, find references, see code owners, trace history, and more. Roll out large-scale changes to many repositories at once and track big migrations.*
  - <https://about.sourcegraph.com/>


## Formatter
- **google-java-format**
  - *exposes extremely few configuration options that govern formatting behavior. goals of this tool are to bring consistency to the codebase, and to free developers from arguments over style choices. It is an explicit non-goal to support developers' individual preferences* 
  - <https://github.com/google/google-java-format>
  - Eclipse- & Maven-Plugins
  - [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
- **prettier-java**
  - *opinionated code formatter. It enforces a consistent style by parsing your code and re-printing it with its own rules*
  - <https://github.com/jhipster/prettier-java>
  - node_module & Maven-Plugin (→ maven/plugins)
- **spotless**
  - *general-purpose formatting*
  - Java und viele andere Sprachen, Intergration per Maven, Gradle, IDE etc
  - unterstützt prettier, google-format, eclipse-jdt, ...
  - Maven-Plugin → maven/spotless-plugin
- **uncrustify**
  - *A source code beautifier for C, C++, C#, ObjectiveC, D, Java, Pawn and VALA*
  - *Highly configurable - 828 configurable options as of version 0.76.0*
  - Binaries für Windows & Linux
  - <https://github.com/uncrustify/uncrustify>
- **palantir-java-format**
  - *based on the excellent google-java-format*
  - <https://github.com/palantir/palantir-java-format>


## Diverse
- **Windows: Umgebungsvariablen für spez. Java-Version setzen**
  - .bat:
    ```bat
    @echo off

    rem /M => The /M option sets the variable at SYSTEM scope. The default behaviour is to set it for the USER.
    rem Usage: Set Env-Vars JAVA_HOME_{8,11,17}, then add the folder with this script ("j.bat") to PATH, then execute this script: "j 8|11|17"

    setLocal enableDelayedExpansion
    set jh=JAVA_HOME_%1
    "!%jh%!\bin\java.exe" -version
    if %ERRORLEVEL% NEQ 0 (
      pause
    ) else (
      setx /M JAVA_HOME "!%jh%!"
      setx /M PATH "!%jh%!\bin;%PATH%"
      echo Java %1 activated as system-wide default.
    )
    ```
  - .ps1:
    ```powershell
    $jh = "JAVA_HOME_{0}" -f $args[0]
    $val = [System.Environment]::GetEnvironmentVariable($jh, 'Machine')
    & "${val}\bin\java.exe" "-version"
    if ($? -eq "True") {
    [System.Environment]::SetEnvironmentVariable('JAVA_HOME', "${val}", 'Machine')
      $p = "${val}\bin;${env:PATH}"
      [System.Environment]::SetEnvironmentVariable('PATH', "${p}", 'Machine')
      Write-Host $("Java {0} activated as system-wide default." -f $args[0])
    }
    ```

- **sdkman**
  - <https://sdkman.io>
  - versch. Versionen von JDK, Maven, ... verwalten
  - für Linux. Windows: nur mit git bash
- **update4j**
  - <https://github.com/update4j/update4j>
  - *first auto-update and launcher library designed for Java 9+. Easily host your application files anywhere (even Google Drive, Dropbox, Amazon S3, or Maven Central) and you can synchronize them with all your distributed applications. You can use any protocol you wish to retrieve those files and may be protected under authenticated API.*
- **jrebel**
  - *can skip rebuilds and redeploys during Java development -- while maintaining application state*
  - kostet Geld
  - <https://www.jrebel.com/products/jrebel>
- **jenv**
  - <https://github.com/jenv/jenv>
  - *lets you switch between java versions. However, this project does not install java for you*
  - *jEnv supports the notion of a global JDK and multiple local JDKs. The global JDK is the JDK that will be used if we type java into the command line anywhere on our computer. A local JDK is a JDK that is configured for a specific folder only. If we type java into the command line in this folder, it will not use the global JDK, but the local JDK instead.*
  - Extra plugin für Maven und Gradle nötig
  - Linux & MacOS. Windows: nur mit WSL oder git bash
- **bugjail**
  - <https://bugjail.com/>
- **remote debugging**
  - <https://stackify.com/java-remote-debugging/>
  - <https://www.rookout.com/blog/remote-java-debugging>
- **hotswap agent**
  - <https://github.com/HotswapProjects/HotswapAgent>
  - *unlimited redefinition of classes at runtime*
  - *main purpose of this project used to be avoiding of infamous change code->restart and wait...->check development lifecycle*
  - *Each application framework (Spring, Hibernate, Logback, ...) needs special reloading mechanism to keep up-to-date after class redefinition (e.g. Hibernate configuration reload after new entity class is introduced). Hotswap agent works as a plugin system and ships preconfigured with all major framework plugins.*
- **j2cl**
  - *transpiler from Java to Closure style JavaScript*
  - <https://github.com/google/j2cl>
- **OpenRewrite**
  - *mass refactoring ecosystem for Java and other source code*
  - *Migrate to Java 11 from Java 8, Migrate to JUnit 5 from JUnit 4, Migrate to SLF4J from Log4j*
  - <https://github.com/openrewrite/rewrite>
  - <https://github.com/openrewrite/rewrite-spring>
  - -> Java/Maven/Rewrite-Plugin
- **Quiltflower**
  - *general purpose decompiler focused on improving code quality, speed, and usability. Quiltflower is a fork of Fernflower and Forgeflower.*
  - <https://github.com/QuiltMC/quiltflower>
- **DepClean**
  - *automatically detects (and removes) unused dependencies in Maven projects*
  - *can be executed as a Maven goal through the command line or integrated directly into the Maven build lifecycle* 
  - <https://github.com/ASSERT-KTH/depclean>
- **Playground**
  - Browser 
  - <https://dev.java/playground/> 
