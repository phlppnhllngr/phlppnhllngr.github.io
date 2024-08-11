---
title: Libs
parent: Java
---

# Libs
{: .no_toc }
<https://github.com/akullpp/awesome-java>


## Inhalt
{: .no_toc }
- TOC
{:toc}


## Async
- **EA-Async**
  - Sync Syntax ("async/await") für CompletableFuture
  - <https://github.com/electronicarts/ea-async> 
- **Disruptor**
  - <https://github.com/LMAX-Exchange/disruptor>
  - *concurrent programming framework for the processing of a large number of transactions, with low-latency*
  - *faster than ArrayBlockingQueue and LinkedBlockingQueue*
- **RSocket**
  - <https://github.com/rsocket/rsocket-java>
  - *async binary messaging*
- **Netty**
  - <https://netty.io/> 
  - <https://www.baeldung.com/netty>
  - <https://www.manning.com/books/netty-in-action>
- **Chronicle Threads**
  - Event Loop 
  - <https://github.com/OpenHFT/Chronicle-Threads>
- **ShedLock**
  - *Distributed lock for your scheduled tasks*
  - *makes sure that your scheduled tasks are executed at most once at the same time. If a task is being executed on one node, it acquires a lock which prevents execution of the same task from another node (or thread)*
  - *if one task is already being executed on one node, execution on other nodes does not wait, it is simply skipped*
  - *ShedLock is not and will never be full-fledged scheduler, it's just a lock* 
  - <https://github.com/lukas-krecan/ShedLock> 

### Scheduling
- **Quartz**
  - <https://github.com/quartz-scheduler/quartz> 
- **jobrunr**
  - <https://github.com/jobrunr/jobrunr>
  - *perform background processing on the JVM. Dead simple API. Extensible. Reliable.*
  - *perform fire-and-forget, delayed and recurring jobs inside Java applications using only Java 8 lambda's*
- **db-scheduler**
  - *inspired by the need for a clustered java.util.concurrent.ScheduledExecutorService simpler than Quartz.*
  - *Requires a single database-table for persistence* 
  - <https://github.com/kagkarlsson/db-scheduler> 

### Reactive
- **Reactor**
  - *Non-Blocking Reactive Streams Foundation for the JVM both implementing a Reactive Extensions inspired API and efficient event streaming support.*
  - <https://github.com/reactor/reactor-core>
  - <https://projectreactor.io/>
  - <https://projectreactor.io/learn>
  - <https://projectreactor.io/docs>
    - <https://projectreactor.io/docs/core/release/reference/#metrics>
    - <https://projectreactor.io/docs/core/release/reference/#debugging>
    - <https://projectreactor.io/docs/core/release/reference/#testing>
  - <https://github.com/schananas/practical-reactor>
- **RxJava**
  - *Reactive Extensions for the JVM*
  - *extends the observer pattern to support sequences of data/events and adds operators that allow you to compose sequences together declaratively while abstracting away concerns about things like low-level threading, synchronization, thread-safety and concurrent data structures.*
  - <https://github.com/ReactiveX/RxJava>
- **Akka Streams**
- **Alpakka**
  - *Reactive Enterprise Integration library for Java and Scala, based on Reactive Streams and Akka*  
  - <https://github.com/akka/alpakka>   
- **BlockHound**
  - *Java agent to detect blocking calls from non-blocking threads*
  - *comes with a few built-in integrations: Project Reactor, RxJava 2 is supported.*
  - <https://github.com/reactor/BlockHound> 

## Mapper
- <https://github.com/akullpp/awesome-java#bean-mapping>
- <https://github.com/arey/java-object-mapper-benchmark>
- **mapstruct**
  - *Java annotation processor for the generation of type-safe and performant mappers*
  - <http://mapstruct.org/>
  - <https://github.com/mapstruct/mapstruct> 3.8k
  - [One-Stop Guide to Mapping with MapStruct](https://reflectoring.io/java-mapping-with-mapstruct/)
- **dozer bean mapper**
  - <https://github.com/DozerMapper/dozer> *1.9k
- **ModelMapper**
  - *intelligent object mapping library that automatically maps objects to each other*
  - *uses a convention based approach while providing a simple refactoring safe API for handling specific use cases.*
  - <https://github.com/modelmapper/modelmapper> *1.9k
- **ShapeShift**
  - reflection based 
  - <https://github.com/krud-dev/shapeshift> 


## (De)Serialisierung

### yaml
- **snake-yaml**
  - <https://bitbucket.org/asomov/snakeyaml/>
- **eo-yaml**
  - <https://github.com/decorators-squad/eo-yaml>
- **jackson.dataformat.yaml**
- **yamlbeans**
  - <https://github.com/EsotericSoftware/yamlbeans>

### json
- **Benchmarks**
  - <https://github.com/fabienrenaud/java-json-benchmark>
  - <https://github.com/eishay/jvm-serializers/wiki>
- <u>Libs</u>
  - <https://github.com/akullpp/awesome-java#json>
  - **Jackson**
    - <https://github.com/FasterXML/jackson>
    - Extensions
      - <https://github.com/FasterXML/jackson#third-party-datatype-modules> (hibernate, lombok, java.time, ...)
      - <https://github.com/zalando/jackson-datatype-money>
      - <https://github.com/FasterXML/jackson-modules-java8>
    - Recipes
      - null handling
        - [Stack Overflow: Serialize null object as empty](https://stackoverflow.com/a/45566139)
  - **jackson-jr**
    - *designed as a light-weight alternative to `jackson-databind`: will only deal with Maps, Lists, Strings, wrappers and Java Beans (jr-objects), or simple read-only trees (jr-stree)*
    - <https://github.com/FasterXML/jackson-jr> 
  - **Gson**
    - etwas langsamer als Jackson
    - <https://github.com/google/gson>
  - **moshi**
    - <https://github.com/square/moshi>
  - **dsl-json**
    - <https://github.com/ngs-doo/dsl-json>
    - *faster than any other Java JSON library. On par with fastest binary JVM codecs*
  - **jsonschema2pojo**
    - *Generate Java types from JSON or JSON Schema and annotates those types for data-binding with Jackson, Gson, etc*
    - <https://github.com/joelittlejohn/jsonschema2pojo> *5.2k
  - **json-masker**
    - *mask sensitive values inside JSON* 
    - <https://github.com/Breus/json-masker> 

### binary
- **kryo**
  - *binary object graph serialization framework for Java*
  - *The project is useful any time objects need to be persisted, whether to a file, database, or over the network*
  - *can also perform automatic deep and shallow copying/cloning. This is direct copying from object to object, not object to bytes to object*
  - <https://github.com/EsotericSoftware/kryo> 


## Web
- **zalando/problem**
  - <https://github.com/zalando/problem>
  - *a library that implements application/problem+json*
- **HtmlUnit**
  - <https://github.com/HtmlUnit/htmlunit>
  - *not a generic unit testing framework. simulate a browser for testing purposes and is intended to be used within another testing framework such as JUnit or TestNG.*
  - JS: ja
  - htmlunit vs selenium
    <br/>
    *HtmlUnit is a java based implementation of a WebBrowser without a GUI and a way to simulate a browser for testing purposes and Selenium-WebDriver makes direct calls to the browser using each browser’s native support for automation. we can see that HtmlUnit provides API without GUI possibility for automation whereas WebDriver provides internal browsers' possibilities for automation.*
- **jsoup**
  - <https://github.com/jhy/jsoup/> ⭐8.1k
  - Html-Parser
  - JS: nein
- **Jericho**
  - Html-Parser 
  - <http://jericho.htmlparser.net/docs/index.html> 
- <u>Scraping</u>
  - <https://github.com/akullpp/awesome-java#web-crawling>
  - **crawler4j**
    - <https://github.com/yasserg/crawler4j> ⭐3.9k
  - **webmagic**
    - <https://github.com/code4craft/webmagic> ⭐9.2k
- **playwright/java**
- **jjwt**
  - <https://github.com/jwtk/jjwt> ⭐6.7k
  - *creating and verifying JSON Web Tokens (JWTs)*
- <u>Http-Client</u>
  - **retrofit**
    - basiert auf OkHttp, bringt json-Support mit
    - <https://square.github.io/retrofit/> ⭐38.2k
  - **okhttp**
    - *HTTP/2 support*
    - <https://github.com/square/okhttp> ⭐41.8k
  - **unirest**
    - basiert auf Apache Http 
    - <https://github.com/Kong/unirest-java>
    - <https://www.baeldung.com/unirest>
  - **feign**
    - *inspired by Retrofit*
    - *java clients for ReST or SOAP services*
    - konfigurierbarer Wrapper um apache-http/okhttp/spring/... + jackson/gson/...
    - Support für Soap, Logging (slf4j), retry, async, ...
    - <https://github.com/OpenFeign/feign> <img loading="lazy" src="https://img.shields.io/github/stars/OpenFeign/feign?style=flat-square"/>
    - Error Decoder: <https://www.baeldung.com/feign-retrieve-original-message>
  - **Apache HttpComponents**
    - v5.1
      - *Standards based, pure Java, implementation of HTTP versions 1.0, 1.1, 2.0*
    - <https://hc.apache.org/index.html>
  - **king-http**
    - *An asynchronous http client with support for sse [server sent events]* 
    - <https://github.com/king/king-http-client#api>
  - **cxf-rt-rs-sse**
    - *Apache CXF client implementation of JAX RS Client API for SSE*
    - <https://www.baeldung.com/java-ee-jax-rs-sse>
  - **Jersey 2**
    - <https://howtodoinjava.com/jersey/jersey-restful-client-examples/>
    - <https://www.baeldung.com/jersey-jax-rs-client>
  - **Google**
    - Monorepo: <https://github.com/googleapis/google-http-java-client>
    - Module:
      - google-http-client
        - Core
        - enthält `HttpRequestFactory`, `HttpRequestInitializer`, `GenericJson`, `JsonFactory` (abstract) etc
        - enthält `NetHttpTransport`, `ApacheHttpTransport` (deprecated; man soll google-http-client-apache-v2 verwenden)
      - google-http-client-jackson2
        - enthält `JacksonFactory` etc
        - abhängig von google-http-client 
      - google-http-client-gson
        - enthält `GsonFactory` etc
        - abhängig von google-http-client
      - google-http-client-apache-v2
        - enthält `ApacheHttpTransport` etc
      - ...
    - <https://googleapis.github.io/google-http-java-client/>
    - Google Api Client
      - <https://github.com/googleapis/google-api-java-client>
      - <https://www.baeldung.com/google-http-client>
- <u>http server</u> -> Java/Server
- <u>websockets</u>
  - **javax.websocket-api**
  - client
    - **tyrus-standalone-client**
- **graphql-java**
  - <https://github.com/graphql-java/graphql-java> ⭐4.9k
- **openapi4j**
  - *openapi4j is a suite of tools, including the following: OpenAPI 3 parser, JSON schema and request validator*
  - <https://github.com/openapi4j/openapi4j>
- **WebView.jar**
  - *cross-platform WebView*
  - *executable jar file [...], or using the Java API*
  - <https://github.com/shannah/webviewjar> 


## Resilience
- **failsafe**
  - <https://github.com/jhalterman/failsafe> ⭐2900
  - *Fault tolerance and resilience patterns for the JVM*
- **resilience4j**
  - <https://github.com/resilience4j/resilience4j> ⭐3300
  - retry, rate limiting, cache, ... 
  - Module für Spring, Spring Boot, vertx und andere
- **bucket4j**
  - rate limiting
  - <https://github.com/vladimir-bukhtoyarov/bucket4j>
  - <https://www.baeldung.com/spring-bucket4j>


## Cache
- **ehcache**
  - <https://www.ehcache.org/>
  - <https://github.com/ehcache/ehcache3> ⭐1300
  - v3 = java 8+
  - *scales from in-process caching, all the way to mixed in-process/out-of-process deployments*
- **JetCache**
  - <https://github.com/alibaba/jetcache> 
  - *JetCache is a Java cache framework which is <mark>more convenient than Spring Cache</mark>. JetCache is a Java cache abstraction which provides consistent use for various caching solutions. It provides more powerful annotation than that in Spring Cache. Presently There are <mark>four implements: RedisCache, TairCache(not open source on github), CaffeineCache (in memory), a simple LinkedHashMapCache (in memory).</mark>*
- **Caffeine**
  - <https://github.com/ben-manes/caffeine> ⭐6100
  - in-memory, java 8+
- **cache2k**
  - <https://cache2k.org/>
- **Apache Commons JCS**
  - Java Caching System
  - *distributed caching system*
  - *most useful for high read, low put applications*
  - *Features: Disk overflow (and defragmentation), Data expiration (idle time and max life), ...*
  - <https://commons.apache.org/proper/commons-jcs/index.html>
- **jcabi cache**
  - <https://aspects.jcabi.com/annotation-cacheable.html>
- **Guava Caching**  
- <u>Redis Clients</u>
  - **jedis**
  - **Redisson**
    - *distributed Java objects and services on top of Redis server. State of the Art Redis Java client*
    - <https://github.com/redisson/redisson>
    - <https://redisson.org/feature-comparison-redisson-vs-jedis.html>
  - **Lettuce**
    - <https://github.com/lettuce-io/lettuce-core> 

## PDF
- **OpenPDF**
  - <https://github.com/LibrePDF/OpenPDF> ⭐1.5k
  - Fork von iText 4.2.0 (letzte FOSS Version)
- **iText**
  - <https://itextpdf.com/>
  - 4.2.0 (letzte FOSS): <https://mvnrepository.com/artifact/com.lowagie/itext/4.2.0>
  - ab 4.2.1: Community-Edition (Lizenz: AGPL 3.0; <https://itextpdf.com/en/how-buy/agpl-license>) oder Commercial edition (💰)
  - tools
    - i7j-pdfhtml
      - *iText 7 add-on... convert HTML and CSS into standards compliant PDFs*
      - <https://github.com/itext/i7j-pdfhtml/>
- **PDFBox**
  - <https://pdfbox.apache.org/>
  - <https://github.com/apache/pdfbox> (mirror) ⭐1.1k
- **openhtmltopdf**
  - *rendering arbitrary well-formed XML/XHTML (and even HTML5) using CSS 2.1 for layout and formatting, outputting to PDF or images*
  - *Based on Flying Saucer and Apache PDF-BOX 2*
  - <https://github.com/danfickle/openhtmltopdf>
- **flyingsaucer**
  - *XML/XHTML and CSS 2.1 renderer in pure Java*
  - <https://github.com/flyingsaucerproject/flyingsaucer>
- **wkhtmltopdf-Wrapper**
  - → Diverses/PDF
  - java-wkhtmltopdf-wrapper
    - <https://github.com/jhonnymertz/java-wkhtmltopdf-wrapper> ⭐250
  - htmltopdf-java
    - <https://github.com/wooio/htmltopdf-java> ⭐100
    - *Access to wkhtmltopdf is performed via JNA, exposed through a Java-friendly layer*
- **Aspose.PDF for Java**
  - *supports the creation of PDF documents through both an API and from XML templates*
  - closed source, kostenpflichtig
  - <https://docs.aspose.com/pdf/java/>
- **Apache FOP** -> ./Diverses


## DB
→ Java/Datenbank


## AOP
- aspectj
  - <https://eclipse.org/aspectj>


## Validation
- **libphonenumber**
  - <https://github.com/google/libphonenumber>
- **yavi**
  - *lambda based type safe validation*
  - *No more reflection, No more (runtime) annotation*
  - z. B.:
    ```java
    foo.constraint(Foo::getBar, "bar", c -> c.notBlank().message("{0} darf nicht leer sein"))
    // -> foo.bar darf nicht leer sein
    ```
  - <https://github.com/making/yavi>
- **java-fluent-validator**
  - <https://github.com/mvallim/java-fluent-validator>
- **hibernate validator**
  - <https://docs.jboss.org/hibernate/stable/validator/reference/en-US/html_single/>
- <u>json</u>
  - **json-schema**
    - <https://github.com/everit-org/json-schema> *631
  - **json-schema-validator**
    - <https://github.com/java-json-tools/json-schema-validator> *1400
  - **json-schema-validator**
    - <https://github.com/networknt/json-schema-validator> *313
- **fluent-validator**
  - *leveraging the fluent interface style and JSR 303 - Bean Validation specification*
  - <https://github.com/neoremind/fluent-validator> *942


## XML
- **joox**
  - <https://github.com/jOOQ/jOOX>
  - Wrapper um org.w3c.dom
  - jQuery-ähnliche API zum Manipulieren von XML
- **xpath**


## DI
- **guice**
  - <https://github.com/google/guice>
- **dagger**
  - *compile-time dependency injection*
  - <https://github.com/google/dagger>
  - <https://dagger.dev/>
- **avaje-inject**
  - *Uses Java annotation processing for dependency injection, Generates source code, Avoids any use of reflection or classpath scanning (so low overhead and fast startup)*
  - <https://github.com/avaje/avaje-inject> *64
- **feather**
  - *ultra-lightweight dependency injection*
  - *based on optimal use of reflection to provide dependencies. No code generating, classpath scanning, proxying or anything costly involved.*
  - <https://github.com/zsoltherpai/feather> *328


## Metrics
- **micrometer**
  - <https://github.com/micrometer-metrics/micrometer> *2.1k
  - *An application metrics facade for the most popular monitoring tools. Think SLF4J, but for metrics.*


## Template engines
- <https://github.com/akullpp/awesome-java#template-engine>
- <https://github.com/xmlet/template-benchmark>
- <https://github.com/jreijn/spring-comparing-template-engines>
- → build/manifold

### text (file) based
- **thymeleaf**
  - <https://www.thymeleaf.org>
  - <https://github.com/thymeleaf> *2100
  - Reflection, rel. langsam, nicht typesafe
  - Module und Plugins für Spring, Eclipse, ...
- **mustache.java**
  - basiert auf mustache.js
  - *We call it "logic-less" because there are no if statements, else clauses, or for loops.*
  - die Dokumentation für mustache-java selbst ist nicht sehr umfangreich (Typsicherheit? IDE-plugins?)
  - <https://github.com/spullara/mustache.java> *1600
  - <https://www.baeldung.com/mustache>
- **jmustache**
  - *Java implementation of the Mustache template language*
  - <https://github.com/samskivert/jmustache> *709
- **rocker**
  - <https://github.com/fizzed/rocker> *560
  - keine Reflection, typesafe (compiled templates)
  - *Rocker just uses the textual file at compile time rather than at run-time.*
  - *uses the textual template file only to automatically generate a Java class that replicates the specific template in Java language*
  - *does not verify the HTML language rules or even well-formed HTML documents*
  - Maven-Plugin
- **groovy**
  - MarkupTemplateEngine
  - XmlTemplateEngine
  - ...
- **jte**
  - <https://github.com/casid/jte> *200
  - compile time checked
  - Intellij-, Maven-Plugins
  - behauptet schneller als "rocker" zu sein
- **freemarker**
- **Pebble**
  - <https://pebbletemplates.io/>
  - <https://github.com/PebbleTemplates/pebble>
- **velocity**
- **jinjava**
  - <https://github.com/HubSpot/jinjava>
- **jstachio**
  - *typesafe Java Mustache templating engine*
  - ```java
    @JStache(template = """
        {{#people}}
        {{message}} {{name}}! You are {{#ageInfo}}{{age}}{{/ageInfo}} years old!
        {{#-last}}
        That is all for now!
        {{/-last}}
        {{/people}}
        """)
    public record HelloWorld(String message, List<Person> people) implements AgeLambdaSupport {
    }
    ```
  - <https://github.com/jstachio/jstachio>

### java-code based
- **HtmlFlow**
  - <https://github.com/xmlet/HtmlFlow> *85
  - angeblich schneller als j2html
- **j2html**
  - <https://github.com/tipsy/j2html> *600
  - *replaces the need of textual template files by templates defined within the Java language*
- **java-html-dsl2**
  - keine Lib, eher ein Hobbyprojekt/PoC
  - <https://github.com/benjiman/java-html-dsl2>


## Regex
- **JavaVerbalExpressions**
  - <https://github.com/VerbalExpressions/JavaVerbalExpressions>
  - *build regex using human language*


## Reflection & Bytecode
- **reflections**
  - <https://github.com/ronmamo/reflections>
- **joor**
  - *simple wrapper for the java.lang.reflect package*
  - *Runtime compilation of Java code: jOOR has an optional dependency on the java.compiler module and simplifies access to javax.tools.JavaCompiler*
  - <https://github.com/jOOQ/jOOR>
- **classgraph**
  - <https://github.com/classgraph/classgraph>
  - *classpath scanner and module scanner*
  - *can find all classes that extend a given class (all subclasses of a given class), or all classes that implement a given interface, or all classes that are annotated with a given annotation*
  - *can find all resources with paths matching a given pattern*
- **permit-reflect**
  - <https://github.com/nqzero/permit-reflect>
  - *permit reflective access for java 11+ (modules)*
- **Objenesis**
  - *serves one purpose: To instantiate a new object of a particular class*
  - *Java already supports this dynamic instantiation of classes using Class.newInstance(). However, this only works if the class has an appropriate constructor. There are many times when a class cannot be instantiated this way*
  - <http://objenesis.org/>
- **ByteBuddy**
  - *high level byte code manipulation, built on top of ASM*
  - auch als Agent erhältlich
  - <https://bytebuddy.net/>
  - Beispiele
    - http interceptor: <https://httptoolkit.tech/blog/how-to-intercept-debug-java-http/>
    - log4j-jndi-be-gone: <https://github.com/nccgroup/log4j-jndi-be-gone> - *A Byte Buddy Java agent-based fix for CVE-2021-44228, the log4j 2.x "JNDI LDAP" vulnerability.*
- **cglib**
  - *high level API to generate and transform Java byte code.*
  - *IMPORTANT NOTE: cglib is unmaintained and does not work well (or possibly at all?) in newer JDKs, particularly JDK17+. If you need to support newer JDKs, we will accept well-tested well-thought-out patches... but you'll probably have better luck migrating to something like ByteBuddy.* 
  - <https://github.com/cglib/cglib> 
  - <https://www.baeldung.com/cglib> 
- **javassist**
  - *makes Java bytecode manipulation simple. It is a class library for editing bytecodes in Java; it enables Java programs to define a new class at runtime and to modify a class file when the JVM loads it.*
  - *Unlike other similar bytecode editors, Javassist provides two levels of API: source level and bytecode level.*
  - *If the users use the source- level API, they can edit a class file without knowledge of the specifications of the Java bytecode. The whole API is designed with only the vocabulary of the Java language. You can even specify inserted bytecode in the form of source text; Javassist compiles it on the fly.*
  - *On the other hand, the bytecode-level API allows the users to directly edit a class file as other editors.* 
  - <https://github.com/jboss-javassist/javassist> *3.4k


## CLI
- **picocli**
  - <https://picocli.info/>
- **jbock**
  - <https://github.com/h908714124/jbock>
  - *annotation based command line args parser*
- **Spring Shell**
  - <https://spring.io/projects/spring-shell>


## Utility
- **jcabi aspects**
  - <https://aspects.jcabi.com/>
  - <https://github.com/jcabi/jcabi-aspects> 
  - nützliche Annotationen, z.B. @Async, @RetryOnFailure, @Cacheable
- **underscore**
  - <http://javadev.github.io/underscore-java>
- **apache commons**
  - <https://commons.apache.org/>
- **Guava**
  - EventBus
    - https://github.com/google/guava/wiki/EventBusExplained
    - Guide: http://www.baeldung.com/guava-eventbus
- **immutables**
  - <https://immutables.github.io/>
  - *Java annotation processors to generate simple, safe and consistent value objects*
  

## Functional
- **vavr**
  - <https://www.vavr.io/>
  - *functional library for Java. It helps to reduce the amount of code and to increase the robustness*
  - *provides immutable collections and the necessary functions and control structures to operate on these values*
- **functionalj**
  - <http://www.functionalj.io/>
- <u>Stream extensions</u>
  - **StreamEx**
    - <https://github.com/amaembo/streamex>
  - **protonpack**
    - <https://github.com/poetix/protonpack>
- <u>Exceptions</u>
  - **NoException**
    - *functional programming for Java exception handlers. Many applications contain thousands of try-catch constructs and it's a mess. Catch clauses are verbose, repetitive, inconsistent, buggy, and hard to test. NoException provides a set of predefined exception handlers (try-catch replacements) that are concise and neat.*
    - https://noexception.machinezoo.com/
  - **throwing-function**
    - `stream().map(ThrowingFunction.unchecked(URI::new))`
    - <https://github.com/pivovarit/throwing-function>


## Office
- **docx4j**
  - <https://github.com/plutext/docx4j> *1.4k
  - *creating, editing, and saving OpenXML "packages", including docx, pptx, and xslx.*
- <u>Word</u>
  - **Aspose.Words-for-Java**
    - *Word processing API that enables you to perform a great range of document processing tasks directly within your Java applications. Aspose.Words for Java API supports processing word (DOC, DOCX, OOXML, RTF) HTML, OpenDocument, PDF, EPUB, XPS, SWF and all image formats. With Aspose.Words you can generate, modify, and convert documents without using Microsoft Word.*
    - <https://github.com/aspose-words/Aspose.Words-for-Java> *237
  - **syncfusion** (💰)
    - <https://www.syncfusion.com/word-framework/java/word-library>
  - **poi-tl**
    - *Generate awesome word(docx) with template*
    - <https://github.com/Sayi/poi-tl>
- <u>Excel</u>
  - siehe docx4j
  - **fastexcel**
    - *(Apache POI) includes many features, but when it comes down to huge worksheets it quickly becomes a memory hog.*
    - <https://github.com/dhatim/fastexcel>
  - **apache poi**
    - die Streaming-Api ist um einiges schneller (org.apache.poi.xssf.streaming)
  - **easyexcel**
    - <https://programming.vip/docs/easyexcel-easy-and-flexible-to-read-excel-content.html>
    - <https://programmer.ink/think/easyexc-alibaba-easyexcel-version-2.0.5-simple-reading-and-writing-example.html>
    - <https://github.com/alibaba/easyexcel> *17.8k
  - **poiji**
    - *A tiny library converting excel rows to a list of Java objects based on Apache POI*
    - ```java
      public class Employee {
        @ExcelRow
        private int rowIndex;
        @ExcelCell(0)
        private long employeeId;
        @ExcelCell(1)
        private String name;
      }
      ```
    - <https://github.com/ozlerhakan/poiji> *256
  - **jxls**
    - <http://jxls.sourceforge.net/>
- **CSV**
  - super-csv
    - <https://github.com/super-csv/super-csv/>
  - FastCSV
    - <https://github.com/osiegmar/FastCSV>


## FTP
- <https://www.infoworld.com/article/2073325/java-ftp-client-libraries-reviewed.html>
- **java.net.URLConnection**
  - <https://www.baeldung.com/java-ftp-client#ftp-support-in-jdk>
- **JSch**
  - <https://www.baeldung.com/java-file-sftp#jsch>
  - <https://github.com/mwiede/jsch>
    - Fork von com.jcraft:jsch
- **Apache Commons Net**
  - populärste Lib
  - <https://www.baeldung.com/java-ftp-client>
  - <https://github.com/apache/commons-net>
  - <https://medium.com/bliblidotcom-techblog/java-ftp-integration-using-apache-commons-net-5efb3d300829>
  - <https://www.codejava.net/java-se/ftp/java-ftp-file-upload-tutorial-and-example>
  - <https://mvnrepository.com/artifact/commons-net/commons-net>
  - kann FTP und FTPS, aber kein SFTP
- **SSHJ**
  - *ssh, scp and sftp for java* 
  - <https://www.baeldung.com/java-file-sftp#sshj>
  - <https://github.com/hierynomus/sshj>
- **Apache Commons VFS**
  - <https://www.baeldung.com/java-file-sftp#vfs>
    - *Apache Commons VFS uses JSch library internally*
  - <https://github.com/apache/commons-vfs>
  - <https://mvnrepository.com/artifact/org.apache.commons/commons-vfs2>


## Diverses
- **javax.measure**
  - JSR-363 (formerly JSR-275)
  - <https://www.baeldung.com/javax-measure>
- <u>javax.money (jsr-354: "currency and money")</u>
  - <https://www.baeldung.com/java-money-and-currency>
  - → java.util.Currency
  - **JavaMoney**
    - <https://github.com/JavaMoney/jsr354-api>
  - **joda-money**
    - <https://www.joda.org/joda-money/>
- <u>Configuration</u>
  - **config**
    - <https://github.com/lightbend/config> *4.7k
    - Configuration library
    - *supports files in three formats: Java properties, JSON, and a human-friendly JSON superset*
  - **jasypt**
    - <http://www.jasypt.org/>
    - *add basic encryption capabilities to his/her projects with minimum effort, and without the need of having deep knowledge on how cryptography works*
    - EncryptableProperties
  - **Externalized Properties**
    - *resolve application properties from various external sources.*
    - <https://github.com/joeljeremy7/externalized-properties>
  - **owner**
    - <https://github.com/matteobaccan/owner>
- **yaml-resource-bundle**
  - <https://github.com/akihyro/yaml-resource-bundle>
- **fswatch**
  - <https://github.com/vorburger/ch.vorburger.fswatch>
  - *watch for file changes, simplifies java.nio.file.WatchService*
- <u>date & time</u>
  - **ThreeTen**
    - <https://www.threeten.org/threetenbp/>
    - *provides a backport of the Java SE 8 date-time classes to Java SE 6 and 7*
  - **Time4J**
    - *Advanced date, time and interval library* 
    - <https://github.com/MenoData/Time4J> 
  - **PrettyTime**
    - *creates human readable, relative timestamps in over 43 languages*
    - *moments ago, 10 minutes from now*   
    - <https://github.com/ocpsoft/prettytime> 
- <u>state management</u>
  - **stateless4j**
    - state machine
    - <https://github.com/stateless4j/stateless4j> *684
  - **state-machine**
    - *Generates java classes to handle state transitions based on a state machine defined with type safety*
    - <https://github.com/davidmoten/state-machine> *100
- <u>feature flags</u>
  - **ff4j**
    - *Enable and disable features at runtime - no deployment*
    - role based / time based / custom predicates
    - if/else or aop (annotations)
    - monitoring, metrics, web console, spring-boot-starter
    - <https://github.com/ff4j/ff4j>
- <u>Native</u>
  - **JavaCPP** 
    - *provides efficient access to native C++ inside Java*
    - *Under the hood, it uses JNI*
    - Presets
      - *contain Java configuration and interface classes for widely used C/C++ libraries*
      - <https://github.com/bytedeco/javacpp-presets> 
- **jmolecules**
  - *Libraries to help developers express architectural abstractions in Java code*
  - *Express that a piece of code (package, class, method…​) implements an architectural concept*
  - ```java
    @Entity public class BankAccount { /* ... */ }
    @ValueObject public class Currency { /* ... */ }
    @Repository public class Accounts { /* ... */ }
    @DomainLayer package org.acmebank.domain;
    ```
  - <https://github.com/xmolecules/jmolecules>
- **JGraphT**
  - Lib für Graphen (data structure)
  - (un)directed, weighted, ... (<https://jgrapht.org/guide/UserOverview#graph-structures>)
  - <https://github.com/jgrapht/jgrapht>
- <u>LDAP</u>
  - **UnboundID**
    - *for communicating with LDAP directory servers*
    - *includes an in-memory directory server is available to allow you easily create one or more simple LDAPv3-compliant servers to use in your testing frameworks*
    - <https://ldap.com/unboundid-ldap-sdk-for-java/>
    - <https://github.com/pingidentity/ldapsdk>
- **Apache FOP**
  - Formatting Objects Processor
  - *reads a formatting object (FO) tree and renders the resulting pages to a specified output. Output formats currently supported include PDF, PS, PCL, AFP, XML, Print, AWT and PNG, and to a lesser extent, RTF and TXT. The primary output target is PDF.* 
  - <https://xmlgraphics.apache.org/>
- **Javet**
  - *an awesome way of embedding Node.js and V8 in Java*
  - ```
    // server.js:
    const express = require("express");
    const app = express();
    
    var test = () => console.log(`hello`);
    ...
    // Main.java:
    File jsFile = ... // server.js
    try (NodeRuntime nodeRuntime = V8Host.getNodeInstance().createV8Runtime()) {
      new Thread(() -> {
        nodeRuntime.getExecutor(jsFile).executeVoid();
        nodeRuntime.await();
      }).start();
      try (V8ValueFunction v8ValueFunction = nodeRuntime.getGlobalObject().get("test")) {
        v8ValueFunction.callVoid(null, i);
      }
    }
    ```
  - <https://github.com/caoccao/Javet> 
- **javatuples**
  - <https://github.com/javatuples/javatuples>
- **RecordBuilder**
  - *annotation processor that creates: a companion builder class for Java records, an interface that adds "with" copy methods*
  - Java 16+
  - <https://github.com/Randgalt/record-builder>
- **GreenMail** -> Webdev/Email
 
