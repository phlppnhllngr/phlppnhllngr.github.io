---
tags: [Notebooks/Java]
title: Server
created: '2019-03-14T15:05:54.829Z'
modified: '2021-07-14T07:44:48.029Z'
parent: Java
---

# Server
→ Java/Build/Packaging/EAR, WAR, JAR

## Tomcat
  - *Tomcat is a web server / web container / servlet container. It is often used as an application server for strictly web-based applications but does not include the entire suite of capabilities that a Java EE application server would supply. It does not implement the whole Java EE API.*
  - embedded tomcat
  - Konfig
    - blocking/non-blocking io
    - max threads
    - max connections
    - min spare threads
    - http timeout
    - language
    - encoding


## Jetty
- https://www.eclipse.org/jetty/
- https://github.com/eclipse/jetty.project
- verbraucht weniger RAM als Tomcat


## Websphere
- [https://www.ibm.com/cloud/blog/websphere-trial-options-and-downloads](https://www.ibm.com/cloud/blog/websphere-trial-options-and-downloads)
- [https://en.wikipedia.org/wiki/IBM_WebSphere_Application_Server#Version_history](https://en.wikipedia.org/wiki/IBM_WebSphere_Application_Server#Version_history)

### Traditional
- aka "tWAS"
- **Installation**
  - [https://geekflare.com/was9-installation-guide/](https://geekflare.com/was9-installation-guide/)
- **Tipps**
  - *Java 11 is not supported on twas 9*
  - Class loading sollte auf 'parent last' gesetzt werden, damit die Libs der Anwendung greifen, nicht die Webpshere-eigenen
  - Beim Hochfahren führt Websphere ein 'class path scanning' durch (~~kann man nicht abschalten?~~ "metadata-complete=true" im web.xml-root-Element?). Ältere Versionen kommen dabei nicht mit module-info.java zurecht. Über Einträge im Manifest kann man die entsprechenden Jars vom Scanning ausschließen:
  ```
  // https://stackoverflow.com/questions/49067032/websphere-hates-multi-release-jars
  "Ignore-Scanning-Packages": "META-INF.versions",
  "Ignore-Scanning-Archives": "jaxb-runtime-2.3.1.jar,jaxb-api-2.3.1.jar,txw2-2.3.1.jar,..."
  ```
  - Classloading
    - [https://www.theserverside.com/tutorial/Classloaders-Demystified-Understanding-How-Java-Classes-Get-Loaded-in-Web-Applications](https://www.theserverside.com/tutorial/Classloaders-Demystified-Understanding-How-Java-Classes-Get-Loaded-in-Web-Applications)
    - Um Classpath-Konflikte zu analysieren: Classloading-Trace aktivieren; serverName > Java und Prozess > Prozessdefinition > JVM > Ausführliche Ausgabe zum Laden der Klassen => loggt absolute Dateipfade der geladenen Klassen nach AppServer/profiles/AppSrv01/logs/server1/native_std<u>err</u>.log (nach Restart des Servers)
    - ClassNotFoundException
      - tritt auf, wenn eine nicht vorhandene Klasse mit `Class.forName(...)` geladen wird
    - NoClassDefFoundError
      - tritt auf, wenn eine nicht vorhandene Klasse "direkt" verwendet und geladen wird; `A a = new A()`
- **Docker**
  - [https://hub.docker.com/r/ibmcom/websphere-traditional/](https://hub.docker.com/r/ibmcom/websphere-traditional/)
  - [https://github.com/WASdev/ci.docker.websphere-traditional](https://github.com/WASdev/ci.docker.websphere-traditional)
    - Dockerfiles: [https://github.com/WASdev/ci.docker.websphere-traditional/tree/master/docker-build](https://github.com/WASdev/ci.docker.websphere-traditional/tree/master/docker-build)
    - Samples: [https://github.com/WASdev/ci.docker.websphere-traditional/tree/master/samples](https://github.com/WASdev/ci.docker.websphere-traditional/tree/master/samples)
  - Varianten
    - ubi
      - universal base image
      - *the UBI, from Red Hat, is a more strategic, and lighter-weight, flavor of Linux, based on a heavily pared-down version of RHEL*
  - unoffiziell: [https://hub.docker.com/r/psinfra/websphere-traditional]()
  - Tutorials
    - [https://medium.com/cloud-engagement-hub/experiences-using-the-twas-docker-container-557a9b044370]() (08/2019)
    - [https://medium.com/cloud-engagement-hub/so-you-want-customized-websphere-container-images-heres-how-42f0e598733f]() (03/2020)
  - compose:

    ```yml
    version: '2'
    services:
      was:
        # Stand 12.8.19 gibt es von IBM kein älteres Image als 8.5.5.14 mehr
        image: 'psinfra/websphere-traditional:websphere-8.5.5.12-insecure-profile' #User=wsadmin, kein PW
        # image: 'ibmcom/websphere-traditional:8.5.5.14-profile' #User=wsadmin
        ports:
        - '9043:9043' #http(s)://localhost:9043/ibm/console
        - '9443:9443' #http(s)://localhost:9443/myapp
        - '8082:8082' #?
        volumes:
        - "./PASSWORD:/tmp/PASSWORD"
        - "./server.xml:/opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/servers/server1/server.xml" #siehe unten
    ```

  Im laufenden Container kann man keine JVM-Args für die Anwendung mehr setzten, weil das einen Neustart von Websphere erfordert (?).
  Die JVM-Args müssen deswegen per server.xml (erhalten via `docker cp` und editiert) als Volume übergeben werden:

  ```xml
  <jvmEntries genericJvmArguments="-Dfoo=bar -Dbaz=xy"></jvmEntries>
  ```

  Alternativ könnte man auch per `sed` die Datei im Image ändern
  [https://github.com/WASdev/ci.docker.websphere-traditional/blob/master/docker-build/9.0.5.7/Dockerfile-ubi8#L102]()
- **Livereload**
  - [http://dplatz.de/blog/2018/was-autodeploy.html](http://dplatz.de/blog/2018/was-autodeploy.html) (04/2018)
  - [https://www.ibm.com/docs/en/was-zos/9.0.5?topic=applications-updating-enterprise-application-files](https://www.ibm.com/docs/en/was-zos/9.0.5?topic=applications-updating-enterprise-application-files)


### Liberty
  - https://hub.docker.com/_/websphere-liberty
  - Bücher
    - [IBM WebSphere Application Server Liberty Profile Guide for Developers (Third Edition July 2015)](@attachment/Buecher/DevOps/IBM WebSphere Application Server Liberty Profile Guide for Developers.pdf)
  - *You can tell Liberty to treat certain files as "minor" changes - which would not require a restart by using this system property (you can add this in your jvm.options file in your server directory - create it if it is not already there): `-Dcom.ibm.ws.app.manager.minorUpdateFileExtensions=.html,.png,.jpg,.myOtherExtension`*
  - Open Liberty
    - *opensource subset of websphere liberty*
    - [Stack Overflow: What is the difference between OpenLiberty and WebSphere Liberty?](https://stackoverflow.com/a/46306037/7437541)


## WildFly
- [https://github.com/wildfly/wildfly](https://github.com/wildfly/wildfly)


## TomEE
- [https://github.com/apache/tomee](https://github.com/apache/tomee)


## GlassFish
- *a Jakarta EE compatible implementation sponsored by the Eclipse Foundation. Eclipse GlassFish 5.1 is also Java EE 8 Compatible.*
- [https://github.com/eclipse-ee4j/glassfish](https://github.com/eclipse-ee4j/glassfish)


## WebLogic
- [https://www.oracle.com/middleware/technologies/weblogic.html](https://www.oracle.com/middleware/technologies/weblogic.html)


## JBoss EAP
- [https://www.redhat.com/en/technologies/jboss-middleware/application-platform](https://www.redhat.com/en/technologies/jboss-middleware/application-platform)
