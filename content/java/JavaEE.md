---
tags: [Notebooks/Java]
title: Java EE
created: '2021-03-14T14:43:26.672Z'
modified: '2021-03-14T14:44:52.562Z'
parent: Enterprise
grand_parent: Java
---

# Java EE
- Java EE 8 war die letzte Version von Oracle, zukünftig Eclipse Foundation/"Jakarta EE"
- <https://en.wikipedia.org/wiki/Jakarta_EE>
- <https://docs.oracle.com/javaee/7/tutorial/>
<br/><br/><img src="https://blog.doubleslash.de/wp-content/uploads/2018/07/JEE_Komponenten_Technologien-1-e1530537749157.png.webp" loading="lazy"/>


## Servlet
- JEE 7: v3.1, JEE 8: v4.0


## RESTful Web Services (JAX-RS)
- JEE 7: v2.0, JEE 8: v2.1


## JSON Processing (JSON-P)
- JEE 7: v1.0, JEE 8: v1.1


## JSON Binding (JSON-B)
- JEE 7: /, JEE 8: v1.1


## Enterprise Beans (EJB)
- JEE 7: v3.2 Lite, JEE 8: v3.2 Lite
- Features: dependency injection, declarative transactions, declarative security, pooling, concurrency control, asynchronous execution, remoting
- *EJB beans have no concept of scoping*
- *the message driven bean can be used to receive messages from the Java Messaging System or from any other system that has a JCA resource adapter. Using full blown messaging for simple events is far more heavyweight than the CDI event bus and EJB only defines a listener, not a producer API.*
- <https://en.wikipedia.org/wiki/Jakarta_Enterprise_Beans>


## Transactions (JTA)


## Persistence (JPA)


## Bean Validation


## Interceptors
- JEE 7: v1.2, JEE 8: v1.2

```java
// Foo.java
@Retention(RetentionPolicy.RUNTIME)
@Target({ ElementType.METHOD })
@javax.interceptor.InterceptorBinding
public @interface Foo {}

// FooInterceptor.java
@javax.interceptor.Interceptor @Transactional
class FooInterceptor {
 @javax.interceptor.AroundInvoke
 public Object invoke(InvocationContext context) {
   System.out.println("foo");
   try {
     return context.proceed();
   } catch (Exception ex) {
     ...
   } finally {
     System.out.println("bar");
   }
 }
}

// Service.java
class Service {
  @Foo
  void foo() {...}
}
```


## Contexts and Dependency Injection (CDI)
- JEE 7: v1.1, JEE 8: v2.0
- Features: dependency injection, scoping, event bus
- <https://www.baeldung.com/java-ee-cdi>
- **Managed Beans**
  - *It doesn’t refer to instances of a class but meta-information which can be used to create those instances. It is represented by the interface `Bean<T>` and will be gathered on container startup via classpath scanning.*
- **Contextual Instance**
  - *Contextual Instances are exactly our singleton instances per scope, our ‘session singletons’, ‘request singletons’, etc. Usually a user never uses a Contextual Instance directly, but only via its ‘Contextual Reference’*
- **Contextual Reference**
  - *By default, a CDI container wraps all Contextual Instances via a proxy and only injects those proxies instead of the real instances. In the CDI specification those proxies are called ‘Contextual Reference’.*


### Dependency Injection

#### @javax.inject.Inject
```xml
<!-- META-INF/beans.xml -->
<beans
  xmlns="http://java.sun.com/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/beans_1_0.xsd"
  bean-discovery-mode="all">
</beans>
```
```java
class Foo {}

class Bar {
  @Inject Bar(Foo foo) {
    this.foo = foo;
  }
}
```

#### @javax.enterprise.inject.Produces
- wie `@Bean` in Spring

```java
class Foo {}

class FooFactory {
  @Produces Foo foo() {
    return new Foo();
  }
}

class Bar {
  @Inject setFoo(Foo foo) {
    this.foo = foo;
  }
}
```

### Scopes

### Events
- <https://dzone.com/articles/cdi-jsf-using-the-cdi-observes>

```java
class Foo {...}

class Fire {
  @Inject Event<Foo> fooEvent;
  
  void fire() {
    this.fooEvent.fire(new Foo());
  }
}

class Observe {
  void onFoo(@javax.enterprise.event.Observes Foo foo) {...}
}
```


## Web apps
- <u>Verzeichnis WEB-INF/</u>
  - Servlet Spec: *The WEB-INF node is not part of the public document tree of the application. No file contained in the WEB-INF directory may be served directly to a client by the container. However, the contents of the WEB-INF directory are visible to servlet code using the getResource and getResourceAsStream method calls on the ServletContext, and may be exposed using the RequestDispatcher calls.*
- <u>Verzeichnis META-INF/</u>
  - **beans.xml**
    - *If a WebApplication gets started, a ServletFilter will automatically also start your CDI container which will firstly register all CDI-Extensions available on the ClassPath and then start with the class scanning. All ClassPath entries with a META-INF/beans.xml will be scanned and all classes will be parsed and stored as ‘Managed Bean’ (`interface Bean<T>`) meta-information inside the CDI container.*

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
  - <u>web.xml</u>
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

  - <u>ibm-web-ext.xml</u>
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

  - <u>ibm-web-bnd.xml</u>
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
      <td>WEB-INF/classes</td>
    </tr>
    <tr>
      <td>src/main/resources</td>
      <td>WEB-INF/classes</td>
    </tr>
    <tr>
      <td>Maven dependencies</td>
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
