---
title: Maven
parent: Java
---

# Maven
{: .no_toc }
- <https://github.com/carlossg/docker-maven> (verschiedene Docker images mit Maven)
- <https://www.reddit.com/r/java/comments/beytye/writing_a_full_featured_maven_pom>
- <https://maven.apache.org/configure.html>
- <https://blog.frankel.ch/faster-maven-builds/1>
- <https://blog.frankel.ch/faster-maven-builds/2>
- <https://andresalmiray.com/a-pom-by-any-other-name/>


## Inhalt
{: .no_toc }
- TOC
{:toc}


## CLI
- options: <https://maven.apache.org/ref/current/maven-embedder/cli.html>
- reactor-project (=Modul) ausschließen: `mvn -pl '!parent/excludeme' clean package`
- mit bestimmtem JDK ausführen:<br/>
  Linux: `export JAVA_HOME=/foo/bar && mvn -v`
- Multithread-Build: (<https://cwiki.apache.org/confluence/display/MAVEN/Parallel+builds+in+Maven+3>)<br>
  `mvn -T 1C ...`


## Maven wrapper (mvnw)
- <https://github.com/takari/maven-wrapper> (soll Bestandteil von Maven 4 werden)


## Maven daemon (mvnd)
- *aims at providing faster Maven builds using techniques known from Gradle and Takari*
- *embeds Maven (so there is no need to install Maven separately). The actual builds happen inside a long living background process, a.k.a. daemon. The mvnd client is a native executable built using GraalVM. It starts faster and uses less memory compared to starting a traditional JVM.*
- <https://github.com/mvndaemon/mvnd>


## Lifecycle, Phasen, Goals
- <https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html>
- Die default-Phasen hängen ab von `project.packaging` (<https://maven.apache.org/ref/current/maven-core/default-bindings.html>)
- Default Executions (Knoten `id`) von Plugins können immer übersprungen werden, indem man ihre Phase auf `none` setzt. Die meisten Plugins unterstützen auch `configuration.skip`. Falls skip nicht unterstützt wird, kann man folgendes tun:
  ```
  properties
    <foo.phase>compile
  /properties
  plugins
    plugin (foo)
      <phase>${foo.phase}

  mvn -Dfoo.phase=none ....
  ```
- Goals eines Plugins können mit `mvn help:describe -Dplugin=group:plugin` angezeigt werden

### Übersicht über die 3 Lifecycles und ihre zugehörigen Phasen
<style>small { color: grey; }</style>
- <u>clean</u>
  - pre-clean
  - clean
  - post-clean
- <u>default</u>
  - validate <small>validate the project is correct and all necessary information is available</small>
  - initialize <small>initialize build state, e.g. set properties or create directories</small>
  - generate-sources <small>generate any source code for inclusion in compilation</small>
  - process-sources
  - generate-resources
  - process-resources
  - compile
  - process-classes <small>post-process the generated files from compilation, for example to do bytecode enhancement on Java classes</small>
  - generate-test-sources
  - process-test-sources
  - generate-test-resources
  - ...
  - test-compile
  - ...
  - test <small>run tests using a suitable <mark>unit testing</mark> framework. These tests should not require the code be packaged or deployed.</small>
    - nur die Tests eines best. Pakets ausführen: `mvn -Dtest="my.package.*Test test`
    - Test-Ausführung überspringen: `mvn clean package -DskipTests`
    - Test-Compile und -Ausführung überspringen: `mvn -Dmaven.test.skip=true clean package`
    - nur Tests einer best. Kategorie (z.B. JUnit5 -> `@Tag(my.package.Group1.class) MyTest`, JUnit4 -> @Category) ausführen: `mvn test -Dgroups=my.package.Group1,my.package.Group2`
  -  ...
  - package
  -  ...
  - integration-test <small>process and deploy the package if necessary into an environment where integration tests can be run</small>
  -  ...
  - verify <small>run any checks on results of integration tests to ensure quality criteria are met</small>
  - install
    - überspringen: `-Dmaven.install.skip=true`
  - deploy
- <u>site</u>
  - pre-site
  - site <small>generate the project's site documentation</small>


## Profiles
- <https://maven.apache.org/guides/introduction/introduction-to-profiles.html>


## Variablen
- **${project.basedir}**
  - *The directory that the current project resides in*
  - *in a module of a multi module project this is the root of the module (not root of the parent)*
- **${project.parent.basedir}**
- **${project.build.directory}**
  - default: "target"
- **${maven.multiModuleProjectDirectory}**
  - *the start of a multi module structure where the .mvn location can be found.*
  - ".mvn"-Verzeichnis muss es geben, darf aber leer sein
  - seit v3.3.1
- **${session.executionRootDirectory}**
  - *a variable that always points to the ... directory ... from which the maven command was executed*


## Erweiterungen
- **polyglot**
  - <https://github.com/takari/polyglot-maven>
- **Maven wrapper**
  - *The project codebase has been accepted to be included in the upstream Apache Maven project itself. Currently the plan is to release the wrapper as a feature of the upcoming Maven 3.7.0 release.*
  - <https://github.com/takari/maven-wrapper>
- **git-versioning**
  - *can virtually set project version and properties, based on current Git status* (branch, tag)
  - <https://github.com/qoomon/maven-git-versioning-extension>
- **jgitver**
  - *automatically define versions using jgitver & git tags*
  - <https://github.com/jgitver/jgitver-maven-plugin>
- **hocon**
  - *provides a Hocon POM parser extension for Maven 4* (Hocon ist ein JSON-Derivat)
  - <https://github.com/apache/maven-hocon-extension> 


## Plugins
- <http://maven.apache.org/plugins/index.html>
- Defaults (unterschiedlich je nach project.packaging): <https://maven.apache.org/ref/current/maven-core/default-bindings.html>
<br/>
- **appassembler**
  - <https://www.mojohaus.org/appassembler/appassembler-maven-plugin/index.html>
  - *for generating scripts for starting java applications*
- **antrun**
  - <https://maven.apache.org/plugins/maven-antrun-plugin>
- **assembly**
  - *extracts all dependency JARs into raw classes and groups them together. It can also be used to build an executable JAR by specifying the main class. It works in project with less dependencies only; for large project with many dependencies, it will cause Java class names to conflict.* 
  - <http://maven.apache.org/plugins/maven-assembly-plugin>
- **build helper**
  - <https://www.mojohaus.org/build-helper-maven-plugin/index.html>
  - z. B. Auslesen der aktuellen pom.version (nützlich für Zusammenspiel mit versions-plugin), ...
  - ```
    <execution>
      <id>parse-version</id>
      <phase>initialize</phase>
      <goals>
        <!-- https://www.mojohaus.org/build-helper-maven-plugin/parse-version-mojo.html -->
        <goal>parse-version</goal>
      </goals>
      <configuration>
        <propertyPrefix>parsedVersion</propertyPrefix>
      </configuration>
    </execution>
    <execution>
      <goals>
        <goal>bsh-property</goal>
      </goals>
      <configuration>
        <properties>
          <property>foo.bar</property>
        </properties>
        <source>foo.bar = project.getVersion().endsWith("SNAPSHOT") ? "foo" : "bar";</source>
      </configuration>
    </execution>
    ```
- **buildplan**
  - *inspect project lifecyle*
  - *List plugin executions within a project: `mvn buildplan:list`* 
  - <https://github.com/mojohaus/buildplan-maven-plugin> 
- **changelog**
  - *generates reports regarding the recent changes in your SCM*
  - <https://maven.apache.org/plugins/maven-changelog-plugin/>
- **checkstyle**
  - <https://maven.apache.org/plugins/maven-checkstyle-plugin>
- **clean**
  - <https://maven.apache.org/plugins/maven-clean-plugin>
- **compiler**
  - <https://maven.apache.org/plugins/maven-compiler-plugin>
  - configuration
    - source
    	- *refers to the source code*
    - target
    	- *refers to the format of the generated class files* 
    - release
    	- *... but they [source, target] do not take into account API changes as maven.compiler.release does*
    	- *if you blindly just use `<maven.compiler.source>8</maven.compiler.source>` and `<maven.compiler.target>8</maven.compiler.target>`, if you build using Java 11 for example the generated class files will support Java 8 but the API may still rely on Java 11 changes and break when run on Java 8*
    	- pom:
    	
	  ```xml
	  <profile>
	    <id>java-8-api</id>
	    <activation>
	      <jdk>[9,)</jdk>
	    </activation>
	    <properties>
	      <maven.compiler.release>8</maven.compiler.release>
	    </properties>
	  </profile>
	  ```
	  
	*That way if you build on Java 9+, maven.compiler.release will come into effect and restrict the API to be compatible with Java 8.*
	- *can't we just add the 3 properties without setting up a profile? -- No, because the Java 8 compiler would complain that it doesn't understand the "source" option.*
- **cxf-codegen**
  - *can generate java artifacts from WSDL*
  - <https://cxf.apache.org/docs/maven-cxf-codegen-plugin-wsdl-to-java.html>
- **depclean**
  - *detects and removes all the unused dependencies declared in the pom.xml file of a project or imported from its parent*
  - Ausführung erfordert Java 11+
  - <https://github.com/ASSERT-KTH/depclean>  
- **dependency**
  - <https://maven.apache.org/plugins/maven-dependency-plugin>
  - *find duplicates / unused, download dependencies, ...*
  - Beliebige Dependency runterladen
    ```
    mvn org.apache.maven.plugins:maven-dependency-plugin:3.2.0:get -Dartifact=groupId:artifactId:version
    mvn org.apache.maven.plugins:maven-dependency-plugin:3.2.0:get -Dartifact=org.projectlombok:lombok:1.18.12
    ```
  - Abhängigkeiten des Projekts in ein spez. Verzeichnis runterladen
    ```
    mvn -DoutputDirectory="." dependency:copy-dependencies
    ```
- **dependency-check**
  - Maven-Plugin für OWASP DependencyCheck
  - <https://jeremylong.github.io/DependencyCheck/dependency-check-maven>
  - *identify the use of known vulnerable components*
  - Bsp. XML-Konfig:
    ```xml
    <configuration>
      <skip>true</skip>
      <cveValidForHours>24</cveValidForHours>
      <formats>JUNIT,HTML</formats>
      <!-- https://nvd.nist.gov/vuln-metrics/cvss -->
      <failBuildOnCVSS>7</failBuildOnCVSS>
      <junitFailOnCVSS>7</junitFailOnCVSS>
      <suppressionFiles>dependency-check-suppressions.xml</suppressionFiles>
    </configuration>
    ```
  - mit Jenkins:
    ```groovy
    sh 'mvn --batch-mode --no-transfer-progress --settings settings.xml dependency-check:check -Ddependency-check.skip=false'
    post {
    	always {
		junit(testResults: 'target/dependency-check-junit.xml')
		archiveArtifacts artifacts: 'target/dependency-check-report.html', onlyIfSuccessful: false
        }
    }
    ```
- **depgraph**
  - *generates dependency graphs in various formats*
  - *can be configured to show duplicate and/or conflicting versions*
  - <https://github.com/ferstl/depgraph-maven-plugin/>
- **deploy**
  - <http://maven.apache.org/plugins/maven-deploy-plugin>
  - ```xml
    <distributionManagement>
      <repository>
        <id>libs-release-local</id>
        <name>libs-release-local</name>
        <url>${deploy.root}/libs-release-local</url>
      </repository>
      <snapshotRepository>
        <id>libs-snapshot-local</id>
        <name>libs-snapshot-local</name>
        <url>${deploy.root}/libs-snapshot-local</url>
      </snapshotRepository>
    </distributionManagement>
    ```
- **directory**
  - *discovery of various project-related paths*
  - <https://github.com/jdcasey/directory-maven-plugin>
- **dockerfile**
  - <https://github.com/spotify/dockerfile-maven>
  - *If you bind the default phases, when you type mvn package, you get a Docker image. When you type mvn deploy, your image gets pushed*
- **download**
  - *download files (...) different protocols*
  - <https://github.com/maven-download-plugin/maven-download-plugin>
- **duplicate-finder**
  - *find and flag duplicate classes and resources on the java classpath*
  - https://github.com/basepom/duplicate-finder-maven-plugin
- **enforcer**
  - <https://maven.apache.org/enforcer/maven-enforcer-plugin>
  - *provides goals to control certain environmental constraints such as Maven version, JDK version and OS family along with many more built-in rules and user created rules*
  - built-ins: requireReleaseDeps, requireJavaVersion, ... (<https://maven.apache.org/enforcer/enforcer-rules/index.html>)
  - best. Dependencies verbieten, best. Imports verbieten, ...
  - auch custom (java-code) rules
- **errorprone**
  - <https://errorprone.info/index>
- **exec**
  - <http://www.mojohaus.org/exec-maven-plugin>
- **failsafe**
  - <https://maven.apache.org/surefire/maven-failsafe-plugin/index.html>
  - *designed to run integration tests while the Surefire Plugin is designed to run unit tests*
- **flatten**
  - https://www.mojohaus.org/flatten-maven-plugin/
  - *generates a flattened version of the pom.xml that Maven installs and deploys instead of the original*
- **flyway**
  - <https://flywaydb.org/documentation/maven>
- **fmt**
  - <https://github.com/coveooss/fmt-maven-plugin>
  - *Formats your code using google-java-format which follows Google's code styleguide*
- **formatter**
  - <https://code.revelc.net/formatter-maven-plugin/>
  - *formatting java source code using the Eclipse code formatter*
- **frontend**
  - <https://github.com/eirslett/frontend-maven-plugin>
- **git-spezifische Plugins**
  - hooks
    - ~~https://github.com/olukyrich/githook-maven-plugin *17~~
      - seit 06/17 inaktiv & nirgends verfügbar
    - githook-maven-plugin
      - <https://github.com/phillipuniverse/githook-maven-plugin> *16 (fork von ^)
      - nachdem man das Plugin im pom.xml hinzugefügt hat, `mvn initialize` ausführen zum Installieren der Hooks
    - pre-commit-maven-plugin
      - <https://github.com/oslomarketsolutions/pre-commit-maven-plugin> *10
      - *plugin for the pre-commit framework*
      - *When compiling a maven project, this plugin will install the git hooks automatically in the developer's Git project*
      - hooks: pre-commit, pre-push, commit-msg
      - Setup relativ kompliziert
    - git-build-hook
      - <https://github.com/rudikershaw/git-build-hook> *6
      - nicht in Doku: muss explizit an Phase gebindet werden
    - git-hook-maven-plugin
      - <https://github.com/arthinking/git-hook-maven-plugin>
      - Doku chinesisch
    - git-code-format-maven-plugin
      - *automatically deploys <https://github.com/google/google-java-format> code formatter as a pre-commit git hook*
      - <https://github.com/Cosium/git-code-format-maven-plugin>
  - gitflow
    - <https://github.com/aleksandr-m/gitflow-maven-plugin>
  - jgit-flow (jgitflow)
    - *Although this plugin is based on the maven-release-plugin, it does things a bit differently to provide a cleaner workflow.* 
    - <https://bitbucket.org/atlassian/jgit-flow/wiki/Home.wiki#!maven-jgit-flow-plugin> 
- **googleformatter**
  - *reformat a projects source/test-sources using the google-java-format project to conform with the Google Code Style Guide* 
  - <https://github.com/talios/googleformatter-maven-plugin> 
- **help**
  - goals
    - evaluate
      - `mvn help:evaluate -Dexpression=foo.bar`
    - effective-pom
      - `mvn help:effective-pom -Dverbose` 
    - effective-settings
    - system
      - *displays a list of the platform details like system properties and environment variables.*
    - describe
      - `mvn help:describe -cmd=package` -> zeigt die Phasen und zugeordnete Plugins+Goals
    - ...
  - <https://maven.apache.org/plugins/maven-help-plugin/> 
- **hibernate-enhance**
  - <https://vladmihalcea.com/maven-gradle-hibernate-enhance-plugin/>
- **install**
- **jar**
  - *provides the capability to build and sign JARs. But it just compiles the java files under src/main/java and src/main/resources/. It doesn't include the dependencies JAR files.* 
  - <https://maven.apache.org/plugins/maven-jar-plugin/>
  - jar vs assembly vs shade: <https://stackoverflow.com/a/43444019/7437541>
- **jaxws**
  - 1) org.codehaus.mojo
	  - *reads a WSDL and generates all the required artifacts for web service development, deployment, and invocation*
	  - letzter Release: v2.6, 01/2020
	  - <https://www.mojohaus.org/jaxws-maven-plugin>
	  - <https://www.baeldung.com/maven-wsdl-stubs>
  - 2) com.sun.xml.ws
  	- die moderne Version des Plugins, auch für Java 11+ geeignet 
  	- <https://github.com/eclipse-ee4j/metro-jax-ws/tree/master/jaxws-ri/extras/jaxws-maven-plugin>
  	- <https://eclipse-ee4j.github.io/metro-jax-ws/jaxws-maven-plugin/>
  - 3) org.jvnet.jax-ws-commons -> der Vorgänger von 2)
  - 4) com.helger.maven -> Fork von 2), inaktiv
- **jib**
  - → Docker/Tools
- **jtoolprovider**
  - *This Maven Plugin does two things. First, it automatically transforms your Maven dependency graph into Java modules. Second, it bridges Maven and built-in Java tools like jdeps, jlink, and jpackage.*
  - *makes it much, much easier to generate native Java desktop applications with nice, small installers.*
  - <https://github.com/wiverson/jtoolprovider-plugin> *12
- **kubernetes** (jkube)
  - Goals
    - apply
    	- *applies the resources created with k8s:resource to a connected Kubernetes cluster. It’s similar to k8s:deploy but does not the full deployment cycle of creating the resource, creating the application image and sending the resource descriptors to the clusters.*  
    - resource
    	- *Create Kubernetes resource descriptors* 
    - build
    - push
    - deploy
    	- *main goal for building your docker image, generating the kubernetes resources and deploying them into the cluster*
    - watch
    	- *reacting to code changes to automatically recreate images or copy new artifacts into running containers*
    - helm
    - log
    - debug
    - remote-dev
    	- Preview-Feature (03/23)
    	- *allows you to run and debug code in your local machine: While connected to and consuming services that are only available in your cluster, While exposing your locally running application to other Pods and services running on your cluster* 
  - <https://github.com/eclipse/jkube/tree/master/kubernetes-maven-plugin> 
  - <https://www.eclipse.org/jkube/docs/kubernetes-maven-plugin/> 
- **license**
  - <http://www.mojohaus.org/license-maven-plugin>
  - *generate your projects license file from your project and dependencies*
- ~~license-check~~
  - <https://github.com/mrice/license-check>
  - Projekt inaktiv
  - *Make sure your Maven dependencies have declared, recognized open source licenses*
  - *checks to make sure that your Maven dependencies have a license declared in their POM files and that you aren't including a license on your project's blacklist*
  - sucht nicht transitiv
  - kann best. Scopes (z.B. test) ausschließen
- **license-verifier-plugin**
  - <https://github.com/AyoyAB/Ayoy-Maven-License-Verifier-Plugin> *9
  - *verify that you only use dependencies and transitive dependencies with acceptable licenses*
  - → Diverses/Rechtliches
  - gut konfigurierbar, sucht transitiv
  - Lizenzinfo kann ab Plugin-Version 1.2.0 aus einem separaten jar bezogen werden (benötigt dann aber java 11+)
  - Optionen
    - excludeMissing
      - Dependencies, dier hier aufgeführt sind, werden nicht durchsucht, auch die transitiven Dependencies nicht
      - die gelisteten Dependencies müssen eine Version haben
  - <details>
      <summary>license.xml</summary>
    </details>
- **licensescan**
  - *for analysing the licenses in dependencies and transitive dependencies, asserting compatibility and potentially fail the build if forbidden licenses appear*
  - <https://github.com/carlomorelli/LicenseScan-Maven-Plugin>
- **m2e-lifecycle-mapping**
  - kein eigentliches Plugin
  - damit können Plugins, die eigentlich an keine Phase gebunden sind (gebunden werden können), an eine gebunden werden
- **modernizer**
  - *Detect uses of legacy Java APIs*
  - legacy APIs: <https://github.com/gaul/modernizer-maven-plugin/blob/master/modernizer-maven-plugin/src/main/resources/modernizer.xml>
  - <https://github.com/gaul/modernizer-maven-plugin> *280
- **native-image**
  - <https://www.graalvm.org/reference-manual/native-image/NativeImageMavenPlugin>
  - <https://mvnrepository.com/artifact/org.graalvm.nativeimage/native-image-maven-plugin>
  - dieses Plugin benötigt `native-image`
    - zunächst braucht man den `graalvm updater (gu)` aus einem Graal-JDK
    - solch ein JDK kann man z.B. mit `sdkman` installieren
      - `sdk ls java` zeigt alle verfügbaren JDKs
      - dann z.B. `sdk install java 21.0.0.r11-grl`
      - dann zum neuen JDK wechseln `sdk default java 21.0.0.r11-grl`
      - neues Terminal > `java -version`
    - mit gu kann man dann `native-image` installieren (`gu install native-image`)
    - Fehler
      - wenn `gcc` fehlt (Debian GNU/Linux 10 (buster)):
        - `sudo apt update`
        - `sudo apt install build-essential`
        - `gcc --version`
      - wenn `/usr/bin/ld: cannot find -lz` (Debian GNU/Linux 10 (buster)):
        - `sudo apt install zlib1g-dev`
- **pmd**
  - <https://pmd.github.io/latest/pmd_userdocs_tools_maven.html>
- **prettier**
  - *Node, prettier, and prettier-java are bundled into the plugin*
  - <https://github.com/HubSpot/prettier-maven-plugin>
- **process**
  - *start multiple processes in pre-integration-test phase in order* 
  - <https://github.com/bazaarvoice/maven-process-plugin> 
- **proguard**
  - <https://github.com/wvengen/proguard-maven-plugin>
- **project-info-reports**
  - *generate reports information about the project.*
  - *ci-management, dependencies, licenses, ...*
  - <https://maven.apache.org/plugins/maven-project-info-reports-plugin>
- **properties**
  - <https://www.mojohaus.org/properties-maven-plugin/index.html>
  - *It provides goals to read properties from files and URLs and write properties to files, and also to set system properties.*
  - versch. properties-files je nach Env, wie Spring
  - <https://www.baeldung.com/java-accessing-maven-properties>
- **release**
  - <http://maven.apache.org/maven-release/maven-release-plugin>
  - ```xml
    <scm>
      <developerConnection>scm:svn:${svn.url}/trunk</developerConnection>
      <connection>scm:svn:${svn.url}/trunk</connection>
      <url>${svn.url}</url>
    </scm>

    <distributionManagement>
      <repository>
        <id>libs-release-local</id>
        <name>libs-release-local</name>
        <url>${deploy.root}/libs-release-local</url>
      </repository>
      <snapshotRepository>
        <id>libs-snapshot-local</id>
        <name>libs-snapshot-local</name>
        <url>${deploy.root}/libs-snapshot-local</url>
      </snapshotRepository>
    </distributionManagement>
    
    <plugin>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>build-helper-maven-plugin</artifactId>
      <version>${maven.buildhelper.version}</version>
      <executions>
        <execution>
	  <id>parse-version</id>
	  <phase>initialize</phase>
	  <goals>
	    <!-- https://www.mojohaus.org/build-helper-maven-plugin/parse-version-mojo.html -->
	    <goal>parse-version</goal>
	  </goals>
	  <configuration>
	    <propertyPrefix>parsedVersion</propertyPrefix>
	  </configuration>
	</execution>
      </executions>
    </plugin>
    <plugin>
       <!-- https://maven.apache.org/maven-release/maven-release-plugin/index.html -->
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-release-plugin</artifactId>
       <version>${maven.release-plugin.version}</version>
       <configuration>
         <autoVersionSubmodules>true</autoVersionSubmodules>
	 <developmentVersion>${parsedVersion.majorVersion}.${parsedVersion.nextMinorVersion}.0-SNAPSHOT</developmentVersion>
  	 <tagNameFormat>@{project.version}</tagNameFormat>
	</configuration>
    </plugin>
    ```
    ```
    mvn --batch-mode clean build-helper:parse-version release:clean release:prepare
    mvn --batch-mode release:perform // mvn --batch-mode release:rollback
    ```
- **replacer**
  - <https://code.google.com/archive/p/maven-replacer-plugin>
  - *replace tokens within a file with a given value and fully supports regular expressions*
  - Example: <https://gist.github.com/21decemb/a338ec66c81bcaca1d9d>
- **resources**
  - <https://maven.apache.org/plugins/maven-resources-plugin>
  - *handles the copying of project resources to the output directory*
  - *replace placeholder-strings in resources at build time*: <https://maven.apache.org/plugins/maven-resources-plugin/examples/filter.html>
- **rewrite**
  - *Eliminate Tech-Debt. At build time.*
  - -> Java/Entwicklungstools/OpenRewrite
  - <https://github.com/openrewrite/rewrite-maven-plugin>
- **semantic-release**
  - *This tool is intended to be used on github projects that use a Travis-CI server*
  - <https://github.com/conveyal/maven-semantic-release>
- **shade**
  - <https://maven.apache.org/plugins/maven-shade-plugin/index.html>
  - *provides the capability to package the artifact in an uber-jar, including its dependencies and to shade - i.e. rename - the packages of some of the dependencies*
  - *remove (parts of) unused dependencies*
  - <https://maven.apache.org/plugins/maven-shade-plugin/examples/resource-transformers.html>
- **site**
- **spotbugs**
  - <http://spotbugs.readthedocs.io/en/latest/maven.html>
- **spotless**
  - <https://github.com/diffplug/spotless/tree/main/plugin-maven#java>
  - Formatter (elcipse jdt, prettier, google-format)
  - nur die gestageten Files formatieren: <https://github.com/diffplug/spotless/issues/178#issuecomment-351638034>
- **sortpom**
  - *helps the user sort pom.xml*
  - <https://github.com/Ekryd/sortpom>
- **source**
  - <https://maven.apache.org/plugins/maven-source-plugin>
  - *creates a jar archive of the source files of the current project*
- **spring-boot**
  → Spring/Entwicklungstools/Maven-Plugin
- **surefire**
  - <http://maven.apache.org/surefire/maven-surefire-plugin>
- **openapi-generator-maven-plugin**
  - unterstützte Languages+Libs
    - Liste 1: <https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator/src/main/java/org/openapitools/codegen/languages>
    - Liste 2: <https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator/src/main/resources>
    - Feign
    	- nur wirklich mit Jackson möglich (angeblich werden Gson und Jackson unterstützt) 
  - <https://openapi-generator.tech/docs/plugins/> 
  - <https://github.com/OpenAPITools/openapi-generator/blob/master/modules/openapi-generator-maven-plugin/README.md>
  - <https://www.baeldung.com/spring-boot-openapi-generator-custom-templates>
- **swagger**
  - *JAX-RS & SpringMVC supported maven build plugin, helps you generate Swagger JSON and API document in build phase.*
  - <https://github.com/kongchen/swagger-maven-plugin>
- **~~swagger-codegen~~**
  - deprecated, siehe openapi-generator-maven-plugin
- **tiles**
  - wiederverwendbare pom-Schnipsel (includes)
  - <https://github.com/repaint-io/maven-tiles>
- **tomcat**
  - <http://tomcat.apache.org/maven-plugin.html>
  - 14.11.19: Support für Tomcat v7
  - *provides goals to manipulate WAR projects within the Apache Tomcat servlet container*
  - *build an executable jar/war*
- **toolchains**
  - <http://maven.apache.org/plugins/maven-toolchains-plugin>
  - *allows to share configuration across plugins. For example to make sure the plugins like compiler, surefire, javadoc, webstart etc. all use the same JDK for execution*
  - <https://maarten.mulders.it/2021/03/introduction-to-maven-toolchains>
- **versions**
  - <https://www.mojohaus.org/versions-maven-plugin>
  - Manipulieren der pom.version, prinzipiell aber jedes property mit `set-property`. Erlaubt revert.
  - Dependency- und Plugin-Updates anzeigen
  - → build-helper-plugin
- **war**
  - <https://maven.apache.org/plugins/maven-war-plugin>
- **was**
  - *Deploy artifact to one or more, local or remote WebSphere Application Server*
  - *Tested on WAS 8.5*
  - inaktiv seit 2017 
  - <https://github.com/orctom/was-maven-plugin> 
- **wildfly**
  - *allows you to: Deploy, redeploy or undeploy your application / Execute CLI commands / Run a standalone server within Maven / packaging of a fully configured server containing application deployment. / ...* 
  - <https://github.com/wildfly/wildfly-maven-plugin>  
- **wildfly-jar**
  - → Java/Server/Wildfly
  - <https://github.com/wildfly-extras/wildfly-jar-maven-plugin/>


## Konfig
- **Linux**
  - Add a file called ".mavenrc" to your home directory with this content:
    `MAVEN_OPTS="$MAVEN_OPTS -Xms512m -Xmx1024m -XX:PermSize=256m -XX:MaxPermSize=512m"`
- **Windows**
  - Add a new environment variable called MAVEN_OPTS and set it to
  `-Xms512m -Xmx1024m -XX:PermSize=256m -XX:MaxPermSize=512m`
- **Eclipse**
  - Within the relevant Run Configuration, select the JRE tab and set the VM Arguments
  `-Xms512m -Xmx1024m -XX:PermSize=256m -XX:MaxPermSize=512m`


## Dependency-Konflikte
- Dependency-Baum aufzeigen mit `mvn dependency:tree`
- Wenn dependency mit versch. Versionen eingebunden ist, gewinnt diejenige, die im Baum weiter unten steht
- enforcer-plugin `<banDuplicatePomDependencyVersions>` oder duplicate-finder-plugin
- [Resolving Maven Dependency Conflicts with a Bill of Materials (BOM)](https://reflectoring.io/maven-bom/)


## Maven in Docker
- → jib-plugin
```
FROM maven:3.8-jdk-8-alpine AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn -e -B dependency:resolve #download dependencies in separate layer => no need to re-download if only source code is changed
COPY src ./src
RUN mvn -e -B package
```
