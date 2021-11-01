---
tags: [Notebooks/Java]
title: Java EE
created: '2021-03-14T14:43:26.672Z'
modified: '2021-03-14T14:44:52.562Z'
parent: Java
---

# Java EE


## Web apps
- Servlet Spec: *The WEB-INF node is not part of the public document tree of the application. No file contained in the WEB-INF directory may be served directly to a client by the container. However, the contents of the WEB-INF directory are visible to servlet code using the getResource and getResourceAsStream method calls on the ServletContext, and may be exposed using the RequestDispatcher calls.*

### EAR, WAR, JAR
- **EAR**
  - enterprise (application) archive
  - *supports Java EE*
  - *contains other archives (war, jar, ejb-jar)*
    - *wars are hosted in the app server's "web container"; designed specifically for web request handling - so more of a request/response style of distributed computing*
    - *ejb-jars are hosted in the app server's "ejb container"; designed to provide extended business functionality such as declarative transactions, declarative method level security and multiprotocol support - so more of an RPC style of distributed computing.*
  - target runtime: application server (websphere, jboss)
  - deployment descriptor: META-INF/application.xml
  - *Java Application Servers allow deployment of standalone web modules in a WAR file, though internally, they create EAR files as a wrapper around WAR files*
  - *allows deployment of multiple wars (modules) at once*
- **WAR**
  - web (application) archive
  - *supports servlet & jsp*
  - *contains compiled java code & static web assets*
  - target runtime: servlet container (liberty, tomcat, jetty)
  - deployment descriptor: WEB-INF/web.xml
  - *Standalone web containers such as Tomcat and Jetty do not support EAR files*
- **JAR**
  - ...
- **EJB-JAR**
  - deployment descriptor: META-INF/ejb-jar.xml
- **Manifest files**
  - ...
- **deployment descriptors**
  - web.xml
    <br/>`metadata-complete="true"` disabled WebSphere-Annotation-Scanning
        https://wasdynacache.blogspot.com/2012/05/how-to-speed-up-annotation-processing.html
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <web-app id="WebApp_ID" version="3.1"
      xmlns="http://xmlns.jcp.org/xml/ns/javaee"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" metadata-complete="<boolean>">
      <display-name>myapp</display-name>
      <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>default.html</welcome-file>
        <welcome-file>default.htm</welcome-file>
        <welcome-file>default.jsp</welcome-file>
      </welcome-file-list>
      <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>foo.bar.servlet.HelloServlet</servlet-class>
      </servlet>
      <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
      </servlet-mapping>
    </web-app>
    ```
  - ibm-web-ext.xml
    - nicht zwinged erforderlich
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
  - ibm-web-bnd.xml
    - nicht zwinged erforderlich
    - *provides binding between resource references used in web module and actual components, like datasouces, queues, etc. However since Java EE 6, you can actually use the lookup attribute from the @Resource annotation to provide them in the code* (https://stackoverflow.com/questions/49790297/why-we-need-ibm-web-bnd-xml-and-ibm-web-ext-xml)
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

### mit Maven
<table>
  <thead>
    <tr>
      <th>source</th>
      <th>target</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>src/main/webapp/web.xml</td>
      <td>WEB-INF/web.xml</td>
    </tr>
    <tr>
      <td>src/main/webapp/ibm-web-ext.xml</td>
      <td>WEB-INF/ibm-web-ext.xml</td>
      <td>für WebSphere</td>
    </tr>
    <tr>
      <td>src/main/webapp/ibm-web-bnd.xml</td>
      <td>WEB-INF/ibm-web-bnd.xml</td>
      <td>für WebSphere</td>
    </tr>
    <tr>
      <td>src/main/java</td>
      <td>WEB-INF/classes
    </tr>
    <tr>
      <td>src/main/resources</td>
      <td>WEB-INF/classes
    </tr>
    <tr>
      <td>&lt;Maven dependencies&gt;</td>
      <td>WEB-INF/lib</td>
      <td>3rd party jars</td>
    </tr>
    <tr>
      <td></td>
      <td>META-INF/MANIFEST.MF</td>
    </tr>
    <tr>
      <td></td>
      <td>META-INF/maven</td>
      <td>enthält pom.xml und pom.properties</td>
    </tr>
    <tr>
      <td>src/assembly</td>
      <td></td>
      <td>für maven-assembly-plugin</td>
    </tr>
    <tr>
      <td></td>
      <td>META-INF/application.xml</td>
    </tr>
  </tbody>
</table>
