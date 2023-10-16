---
title: Server
parent: Java
---

# Server
→ Java/Build/Packaging/EAR, WAR, JAR
- jwebserver
  - *The Simple Web Server was added to the jdk.httpserver module in JDK 18. It is a minimal HTTP static file server, designed to be used for prototyping, testing, and debugging*
  - *The Simple Web Server is run with jwebserver on the command line. It serves static files in a single directory hierarchy over HTTP/1.1; dynamic content and other HTTP versions are not supported.*
  - <https://inside.java/2021/12/06/working-with-the-simple-web-server/>


## Servlet Container

### Tomcat
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


### Jetty
- <https://www.eclipse.org/jetty/>
- <https://github.com/eclipse/jetty.project>
- verbraucht weniger RAM als Tomcat


## Application Server
- <https://en.wikipedia.org/wiki/List_of_application_servers#Java>

### Websphere Application Server (Traditional aka "tWAS")
- <https://www.ibm.com/cloud/blog/websphere-trial-options-and-downloads>
- <https://en.wikipedia.org/wiki/IBM_WebSphere_Application_Server#Version_history>
- <https://stackoverflow.com/questions/45815445/ibm-webpshere-full-profile-webpshere-traditional-profile-and-websphere-classic>
- **Installation**
  - <https://geekflare.com/was9-installation-guide>
- **Tipps**
  - *Java 11 is not supported on twas 9*
  - Beim Hochfahren führt Websphere ein 'class path scanning' durch (~~kann man nicht abschalten?~~ "metadata-complete=true" im web.xml-root-Element?). Ältere Versionen kommen dabei nicht mit module-info.java zurecht. Über Einträge im Manifest kann man die entsprechenden Jars vom Scanning ausschließen:
  ```
  // <https://stackoverflow.com/questions/49067032/websphere-hates-multi-release-jars>
  "Ignore-Scanning-Packages": "META-INF.versions",
  "Ignore-Scanning-Archives": "jaxb-runtime-2.3.1.jar,jaxb-api-2.3.1.jar,txw2-2.3.1.jar,..."
  ```
- **Classloading**
  - <https://www.theserverside.com/tutorial/Classloaders-Demystified-Understanding-How-Java-Classes-Get-Loaded-in-Web-Applications>
  - Class loading sollte auf 'parent last' gesetzt werden, damit die Libs der Anwendung greifen, nicht die Webpshere-eigenen
  - Um Classpath-Konflikte zu analysieren: Classloading-Trace aktivieren; serverName > Java und Prozess > Prozessdefinition > JVM > Ausführliche Ausgabe zum Laden der Klassen => loggt absolute Dateipfade der geladenen Klassen nach AppServer/profiles/AppSrv01/logs/server1/native_std<u>err</u>.log (nach Restart des Servers)
  - ClassNotFoundException
    - tritt auf, wenn eine nicht vorhandene Klasse mit `Class.forName(...)` geladen wird
  - NoClassDefFoundError
    - tritt auf, wenn eine nicht vorhandene Klasse "direkt" verwendet und geladen wird; `A a = new A()`
- **Performance**
  - <https://developer.ibm.com/languages/java/articles/optimize-jvm-startup-with-eclipse-openjj9>
  - <https://stackoverflow.com/questions/1178210/websphere-application-server-what-on-earth-will-it-take-to-start-any-fast>
  - <https://www.ibm.com/support/pages/custom-properties-improving-application-startup-websphere-application-server>
  - <https://www.ibm.com/support/pages/apar/PM26361>
- **Docker**
  - <https://hub.docker.com/r/ibmcom/websphere-traditional>
  - <https://github.com/WASdev/ci.docker.websphere-traditional>
    - Dockerfiles: <https://github.com/WASdev/ci.docker.websphere-traditional/tree/master/docker-build>
    - Samples: <https://github.com/WASdev/ci.docker.websphere-traditional/tree/master/samples>
  - Varianten
    - ubi
      - universal base image
      - *the UBI, from Red Hat, is a more strategic, and lighter-weight, flavor of Linux, based on a heavily pared-down version of RHEL*
  - unoffiziell: <https://hub.docker.com/r/psinfra/websphere-traditional>
  - Tutorials
    - <https://medium.com/cloud-engagement-hub/experiences-using-the-twas-docker-container-557a9b044370> (08/2019)
    - <https://medium.com/cloud-engagement-hub/so-you-want-customized-websphere-container-images-heres-how-42f0e598733f> (03/2020)
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
  <https://github.com/WASdev/ci.docker.websphere-traditional/blob/master/docker-build/9.0.5.7/Dockerfile-ubi8#L102>
- **Livereload**
  - [http://dplatz.de/blog/2018/was-autodeploy.html](http://dplatz.de/blog/2018/was-autodeploy.html) (04/2018)
  - [https://www.ibm.com/docs/en/was-zos/9.0.5?topic=applications-updating-enterprise-application-files](https://www.ibm.com/docs/en/was-zos/9.0.5?topic=applications-updating-enterprise-application-files)
- **zusätzliche deployment descriptors**
  - ibm-web-ext.xml
      - nicht zwingend erforderlich
      - *allows you to configure some settings for web module e.g. context-root, directory browsing, etc and JSP engine parameters* (https://stackoverflow.com/questions/49790297/why-we-need-ibm-web-bnd-xml-and-ibm-web-ext-xml)

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <web-ext
        xmlns="http://websphere.ibm.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://websphere.ibm.com/xml/ns/javaee http://websphere.ibm.com/xml/ns/javaee/ibm-web-ext_1_1.xsd"
        version="1.1">
        <reload-interval value="3"/>
        <enable-directory-browsing value="false"/>
        <enable-file-serving value="true"/>
        <enable-reloading value="true"/>
        <enable-serving-servlets-by-class-name value="false"/>
        <context-root uri="myapp"/>
      </web-ext>
      ```

  - <u>ibm-web-bnd.xml</u>
    - nicht zwingend erforderlich
    - *provides binding between resource references used in web module and actual components, like datasouces, queues, etc. However since Java EE 6, you can actually use the lookup attribute from the @Resource annotation to provide them in the code* (<https://stackoverflow.com/questions/49790297/why-we-need-ibm-web-bnd-xml-and-ibm-web-ext-xml>)
    
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <web-bnd 
      xmlns="http://websphere.ibm.com/xml/ns/javaee"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://websphere.ibm.com/xml/ns/javaee http://websphere.ibm.com/xml/ns/javaee/ibm-web-bnd_1_2.xsd"
      version="1.2">
      <virtual-host name="default_host"/>
    </web-bnd>
    ```


### (Open) Liberty
- *A lightweight open framework for building fast and efficient cloud-native Java microservices.*
- *Open Liberty is a lightweight open source Java™ runtime that is built by using modular features. WebSphere Liberty is a commercial version of Open Liberty.*
- [Stack Overflow: What is the difference between OpenLiberty and WebSphere Liberty?](https://stackoverflow.com/a/46306037/7437541)
- *Liberty features support for the following application frameworks:*
  - *MicroProfile, an open source project that defines new standards and APIs to accelerate and simplify the creation of microservices.*
  - *Jakarta EE and Java™ EE, including features for individual specifications, like JNDI or JAX-RS.*
  - *Spring Framework and Spring Boot, including mechanisms to make compact containers from Spring Boot's fat .jar's.*
- *You can tell Liberty to treat certain files as "minor" changes - which would not require a restart by using this system property (you can add this in your jvm.options file in your server directory - create it if it is not already there): `-Dcom.ibm.ws.app.manager.minorUpdateFileExtensions=.html,.png,.jpg,.myOtherExtension`*
- InstantOn
  - *provides incredibly fast startup times for MicroProfile and Jakarta EE applications* 
  - *uses new features of the OpenJ9 JVM and a Linux technology called Checkpoint/Restore In Userspace CRIU to take a checkpoint of the application process as it starts. This checkpoint is a snapshot of the running application process that can be persisted and then quickly restored to bring the application process back into the state it was in when the checkpoint was taken.* 
  - <https://openliberty.io/blog/2022/09/29/instant-on-beta.html>
  - <https://www.infoq.com/articles/rapid-startup-of-your-cloud-native-java>
- <https://openliberty.io/>
- <https://hub.docker.com/_/open-liberty/>
- <https://hub.docker.com/_/websphere-liberty>
- <https://openliberty.io/blog/2018/07/02/creating-dual-layer-docker-images-for-spring-boot-apps.html>
- Übersicht Features: <https://www.ibm.com/docs/de/was-liberty/core?topic=management-liberty-features>


### WildFly
- ehemals "JBoss AS"
- <https://www.wildfly.org/>
- <https://github.com/wildfly/wildfly>
- <https://github.com/wildfly/quickstart>
- <https://docs.wildfly.org/26/Admin_Guide.html>
- **Docker**
  - <https://github.com/jboss-dockerfiles/wildfly>
  - <https://quay.io/organization/wildfly>
    - <https://quay.io/repository/wildfly/wildfly>
    - <https://quay.io/repository/wildfly/wildfly-runtime>
    - Runtime-Image + Wildfly-Maven-Plugin + Galleon-Feature-Packs: <https://www.wildfly.org/news/2022/08/04/wildfly-maven-docker/>
  - ```
    docker run --name wildfly -p 8080:8080 -p 9990:9990 -it quay.io/wildfly/wildfly:23.0.2.Final /opt/jboss/wildfly/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0
    docker exec -it wildfly /bin/sh
    /opt/jboss/wildfly/bin/add-user.sh -> admin
    ```
- **Konfig**
  - *offers three different approaches to configure and manage servers: a web interface, a command line client and a set of XML configuration files*
  - *Any configuration changes made via the web interface or the CLI are persisted back to the XML configuration files.*
  - <https://docs.wildfly.org/26/Admin_Guide.html#Management_Clients>
  - <https://docs.wildfly.org/26/Admin_Guide.html#Management_tasks>
  - <http://www.mastertheboss.com/jbossas/jboss-configuration/how-to-use-environment-variables-in-standalone-xml-or-host-xml/>
  - CLI
    - <https://docs.wildfly.org/26/Admin_Guide.html#Command_Line_Interface>
    - <https://docs.wildfly.org/26/Admin_Guide.html#CLI_Recipes>
    - ```
      /opt/jboss/wildfly/bin/jboss-cli.sh --connect
      /subsystem=datasources:read-resource(recursive=true)
      /subsystem=datasources/data-source=ExampleDS:read-resource-description
      /subsystem=datasources/data-source=ExampleDS:write-attribute(name=flush-strategy,value=FailingConnectionOnly)
      /subsystem=datasources/data-source=ExampleDs/statistics=pool:read-resource(include-runtime=true)

      /subsystem=logging:read-resource
      /subsystem=logging/root-logger=ROOT:remove-handler(name="FILE")
      /subsystem=logging/root-logger=ROOT:read-resource
      /subsystem=logging/console-handler=CONSOLE:read-resource
      /subsystem=logging/pattern-formatter=COLOR-PATTERN:read-resource
      /subsystem=logging/pattern-formatter=COLOR-PATTERN:write-attribute(name="pattern", value="%s%e%n")
      /subsystem=logging/periodic-rotating-file-handler=FILE:remove
      /subsystem=logging/pattern-formatter=COLOR-PATTERN:write-attribute(name="pattern", value="%K{level}%d{HH:mm:ss,SSS} %-5p [%c] (%t) %s%e%n")
      /subsystem=logging/logger=de.foo.bar:add
      /subsystem=logging/logger=de.foo.bar:read-resource
      /subsystem=logging/pattern-formatter=COLOR-PATTERN2:add
      /subsystem=logging/pattern-formatter=COLOR-PATTERN2:write-attribute(name="pattern", value="%s%e%n")
      /subsystem=logging/console-handler=CONSOLE2:add
      /subsystem=logging/console-handler=CONSOLE2:write-attribute(name="formatter", value="COLOR-PATTERN2")
      /subsystem=logging/logger=de.foo.bar:write-attribute(name="handlers", value=["CONSOLE2"])
      /subsystem=logging/logger=de.baz.qux:add(handlers=["CONSOLE2"])
      quit
      ```
    - embedded server
      - <http://www.mastertheboss.com/soa-cloud/docker/how-to-run-cli-commands-in-wildfly-dockerfile/>
      - <https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/management_cli_guide/running_embedded_server>
    - Datasource konfigurieren: <https://gist.github.com/Inkimar/6ca3014fef4abfd02025>
- <u>Extras</u>
  - **Bootable Jar**
    - *contains both the server and your packaged application (a JAR, an EAR or a WAR)*
    - *Some limitations exist*
    - <https://docs.wildfly.org/26.1/Bootable_Guide.html#wildfly_bootable_JAR_development>
    - <https://github.com/wildfly-extras/wildfly-jar-maven-plugin> 
- **Security**
  - <https://wildfly-security.github.io/wildfly-elytron/>
- **Subsystems**
  - alle aktiven auflisten: `/:read-children-names(child-type=subsystem)` (<https://docs.wildfly.org/26/Admin_Guide.html#list-subsystems>)
  - Subsystem deaktivieren: `/subsystem=xxx:remove`
  - DataSource
    - <https://docs.wildfly.org/26/Admin_Guide.html#DataSource>
    - <https://docs.wildfly.org/26/wildscribe/deployment/subsystem/datasources/data-source/index.html>
  - messaging-activemq
    - <https://docs.wildfly.org/26/Admin_Guide.html#Messaging> 
    - <https://stackoverflow.com/questions/41015817/jboss-admin-console-not-showing-any-messaging-option-under-subsystems>
  - metrics
    - <https://docs.wildfly.org/26/Admin_Guide.html#MicroProfile_Metrics_SmallRye_Subsystem_Config>
    - Grafana Dashboard: <https://grafana.com/grafana/dashboards/13489-microprofile-wildfly-16-metrics/>
  - health
    - <https://docs.wildfly.org/26/Admin_Guide.html#MicroProfile_Health_SmallRye>
  - web service
    - <https://docs.wildfly.org/26/Admin_Guide.html#Web_services>
  - jmx
    - <https://docs.wildfly.org/26/Admin_Guide.html#JMX> 


### TomEE
- <https://github.com/apache/tomee>


### GlassFish
- *a Jakarta EE compatible implementation sponsored by the Eclipse Foundation. Eclipse GlassFish 5.1 is also Java EE 8 Compatible.*
- <https://github.com/eclipse-ee4j/glassfish>


### WebLogic
- <https://www.oracle.com/middleware/technologies/weblogic.html>


### JBoss EAP
- kommerzielle Version von WildFly, Support durch RedHat
- <https://www.redhat.com/en/technologies/jboss-middleware/application-platform>


## Andere
- **Netty**
  - *an asynchronous event-driven network application framework for rapid development of maintainable high performance protocol servers & clients*
  - *Netty is able to run inside a servlet container*
  - <https://netty.io/>
- **Reactor-Netty**
  - *TCP/HTTP/UDP/QUIC client/server with Reactor over Netty*
  - <https://github.com/reactor/reactor-netty>
- **Nginx Unit**
  - -> Webdev/Webserver
  - kann JSP & .war (*by using the Servlet Specification 3.1 and WebSocket APIs*)
  - <https://unit.nginx.org/howto/samples/#java> 
  - <https://unit.nginx.org/howto/springboot/> 
