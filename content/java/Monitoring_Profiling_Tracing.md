---
tags: [Notebooks/Java]
title: 'Monitoring, Profiling'
created: '2019-03-21T20:24:50.818Z'
modified: '2021-08-29T15:46:23.821Z'
parent: Java
---

# Monitoring, Profiling
- <https://github.com/akullpp/awesome-java#monitoring>
- (2) <https://dzone.com/articles/java-performance-monitoring-5-open-source-tools-you-should-know>
- (1) <https://blog.codota.com/top-9-free-java-process-monitoring-tools/>
<br/>→ DevOps/Monitoring
<br/>
- /jdk/bin
  - **jcmd** (java diagnostic command tool)
    - <https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr006.html>
    - *The jcmd utility is used to send diagnostic command requests to the JVM, where these requests are useful for controlling Java Flight Recordings, troubleshoot, and diagnose JVM and Java Applications.*
    - *it must be used on the same machine on which JVM is running*
  - jinfo
  - jmap
  - jlink
  - jmod
  - jimage
  - jdeps
  - jstat
  - javap
  - **jstack**
    - *attaches to the specified process or core file and prints the stack traces of all threads that are attached to the virtual machine, including Java threads and VM internal threads, and optionally native stack frames. The utility also performs deadlock detection.*
  - **jmc** (java mission control)
      - *contains a plugin that allows us to visualize the data collected by JFR*
      <br/><img src="https://download.oracle.com/technology/products/missioncontrol/updatesites/base/5.2.0/eclipse/images/screen-capture-01-large.png" loading="lazy" />
  - **jfr** (java flight recorder)
    - *collects information about the events in a Java Virtual Machine (JVM) during the execution of a Java application*
    - *is a tool for collecting diagnostic and profiling data about a running Java application. It is integrated into the Java Virtual Machine (JVM)*
    - *low overhead, continuous monitoring*
    - *not a standalone tool*
    - *activate it in two ways: when starting a Java application or
      passing diagnostic commands of the jcmd tool when a Java application is already running*
    - <https://github.com/flight-recorder/health-report>
    - <https://www.javaadvent.com/2021/12/keep-your-sql-in-check-with-flight-recorder-jmc-agent-and-jfrunit.html>
    - Übersicht jfr events: <https://bestsolution-at.github.io/jfr-doc/>
    - Custom events (jdk.jfr api; java 9+): <https://www.morling.dev/blog/rest-api-monitoring-with-custom-jdk-flight-recorder-events/>
    - <https://blogs.oracle.com/javamagazine/java-flight-recorder-and-jfr-event-streaming-in-java-14>
    - <https://www.baeldung.com/java-flight-recorder-monitoring>
    - <https://cryostat.io/> - *JFR for Containerized Java Applications*
  - **jconsole**
    - *The JConsole graphical user interface is a monitoring tool that complies to the Java Management Extensions (JMX) specification. JConsole uses the extensive instrumentation of the Java Virtual Machine (Java VM) to provide information about the performance and resource consumption of applications running on the Java platform.*
    - <https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html>
    <br/><img src="https://docs.oracle.com/javase/8/docs/technotes/guides/management/figures/overviewtab.gif" loading="lazy" />


## Profilers
- *profilers should detail out all memory usage by the JVM including object creation, method executions, iterative executions, thread executions, and garbage collection*
- **micrometer**
  - <https://micrometer.io>
- **MoSKito**
  - <https://www.moskito.org/index.html>
  - aus Hands-On High Performance with Spring 5:
    - *MoSKito	is	a	group	of	three	tools:*
      - *MoSKito-Essential:	This	standalone	project	is	the	core	of	MoSKito.	It makes	it	possible	to	monitor	the	application.*
      - *MoSKito-Central:	This	works	as	a	centralized	storage	server.	It	stores	all of	the	performance-related	information.*
      - *MoSKito-Control:	This	tool	works	for	multi-node	web	applications.	It provides	support	for	monitoring	multi-node	web	applications.*
    - *In	order	to	set	up	MoSKito,	we	need	to	install	a	JAR	file	in	the	application's	WEBINF/lib	directory,	which	is	a	common	folder	for	keeping	API	libraries.	It	can	also be	set	up	by	adding	a	new	section	in	the	web.xml	file.
    The	tool	is	capable	of	collecting	all	of	the	application	performance	metrics, including	memory,	threads,	storage,	caches,	registrations,	payments, conversions,	SQL,	services,	load	distribution,	and	many	more.	It	does	not	require users	to	make	any	code	changes	in	the	application.	It	supports	all	major application	servers,	including	Tomcat,	Jetty,	JBoss,	and	Weblogic.	It	stores	the data	locally.*
    - *MoSKito	also	has	a	notification	feature	to	broadcast	an	alert	when	a	threshold	is met.	It	also	records	a	user's	actions,	which	might	be	of	interest	for	monitoring purposes.	MoSKito	offers	a	mobile	application	for	monitoring	the	application	on the	go.	It	also	has	web-based	dashboards.*
  - <mark>free</mark>
  - *integrations for spring, jee, ... or as java agent*
- **VisualVM**
  - *VisualVM can be used do dump the heap and view the allocated objects. It displays the byte count for every object, and allocated overall size.*
  - <mark>kostenlos</mark>
  - diverse Plugins
    - <https://visualvm.github.io/plugins.html>
    - Menü>Tools>Plugins
  - <https://engineering.talkdesk.com/ninjas-guide-to-getting-started-with-visualvm-f8bff061f7e7> (docker/remote)
- **YourKit** 💰
  - <https://www.yourkit.com/java/profiler/features/>
- **JProfiler** 💰
  - <https://www.ej-technologies.com/products/jprofiler/overview.html>
- **HeapHero**
  - <https://heaphero.io/>
  - *Java & Android Heap Dump Analyzer*
  - *Auto Memory Leak Detection*
  - *Tips to Reduce Memory 30-70%*
  - als SaaS kostenlos, lokale Installation kostet


## APM
- **OverOps** 💰
  - <https://www.overops.com/product>
- **javamelody**
  - <https://github.com/javamelody/javamelody>
  - *monitoring of JavaEE applications*
  - <mark>free</mark>
- **appdynamics** 💰
  - <https://www.appdynamics.de/java/>
- **newrelic** 💰
  - <https://newrelic.com/java>
  - aus Hands-On High Performance with Spring 5:
    - *New	Relic	supports	applications	developed	in	Java,	Scala,	Ruby,	Python,	PHP, .NET,	and	Node.js*
    - *New	Relic	offers	four	different	approaches	for	backend monitoring*
      - *Application	performance	management:	In	application	performance management,	New	Relic	features	high-level	metrics	with	the	ability	to	drill down	to	the	code	level	to	see	how	the	application	is	performing.	On	the dashboard,	New	Relic	displays	a	response	time	graph.	New	Relic	uses	the Apdex	index	score	method	to	distill	metrics	into	performance	indicators. New	Relic	requires	the	user	to	manually	set	the	threshold	values.*
      - *Server	monitoring:	New	Relic	focuses	on	the	hardware	the	application servers	are	running	on.	The	measurements	include	CPU	usage,	memory utilization,	disk	I/O,	and	network	I/O.	New	Relic	provides	brief	details	on the	heap	memory	and	garbage	collection	attributes.*
      - *Database	monitoring:	In	New	Relic,	the	dashboard	for	the	database	is	a part	of	the	application	performance	management	dashboard.	It	is	possible	to view	database	monitoring	metrics	through	plugins.*
      - *Insights	and	analytics:	New	Relic	has	a	built-in,	opt-in	database,	which stores	statistics	and	enables	querying	the	database.*
- **scouter**
  - <https://github.com/scouter-project/scouter> ⭐1.5k
  - *the open source new relic and appdynamics* [1]
  - <mark>free</mark>
- **dynatrace** 💰
  - <https://www.dynatrace.com/>
- **Stagemonitor**
  - <https://www.stagemonitor.org/de/>
  - <https://github.com/stagemonitor/stagemonitor> ⭐1.5k
  - aus "Hands-On High Performance with Spring 5":
    - *has	a	monitoring	agent	built	with	support	for	clustered	application stacks*
    - *It is optimized	for	time	series	data management,	which	includes	arrays	of	numbers,	indexed	by	time.	Such databases	include	elasticsearch, graphite, and InfluxDB*
    - *Stagemonitor	contains	a	Java-based	agent.	The	agent	sits	in	the	Java	application. The agent	connects	to	the	central	database	and	sends	metrics	and	request	traces and	statistics.	Stagemonitor	requires	one	instance	for	monitoring	all	applications, instances, and	hosts.*
- **Pinpoint**
  - <http://naver.github.io/pinpoint/>
  - *if you’re looking to monitor the performance of large-scale distributed systems written in Java* [1]
  - <mark>free</mark>
  - aus "Hands-On High Performance with Spring 5":
    - Pinpoint is	different	from	Stagemonitor,	in that it was developed with large-scale applications in	mind
- **Glowroot**
  - <https://glowroot.org/>
  - <https://demo.glowroot.org/>
  - <https://github.com/glowroot/glowroot> ⭐700
  - <mark>free</mark>, simple APM (javaagent)
- **Kamon** 💰
  - <https://kamon.io/>
- **Chronon** 💰
  - <http://chrononsystems.com/>
- **Apache Skywalking**
  - <https://github.com/apache/skywalking>
- **fusion-reactor** 💰
  - *will instantly discover Java application errors, memory & CPU bottlenecks and code & SQL performance problems*
  - *Real-Time Monitoring, Continuous Profiling, Database Monitoring, Live Debugging, Multi-Channel Alerts*
  - <https://www.fusion-reactor.com/>
- **Rookout** 💰
  - <https://www.rookout.com/>
  - *remote debugging, logging, monitoring, profiling*
- **Sidekick**
  - *Like chrome dev tools but for your backend*
  - *Add dynamic logs and put non-breaking breakpoints in your running application without the need of stopping & redeploying*
  - *allow self-hosting*
  - *Either use Sidekick's Web IDE, VS Code & IntelliJ IDEA extensions to control your Sidekick Actions or use headless clients to bring Sidekick to your workflow in any way you want!*
  - Support für Java (`-javaagent`), Nodejs, Python
  - IDE-Integration
    - VSCode: Node, Python
    - Intellij: Java 
  - <https://github.com/runsidekick/sidekick>
  - <https://docs.runsidekick.com/>
- **Lightrun** 💰
  - *Dev Observability Platform for Production Debugging*
  - *Instrument Your Live Application with Dynamic Logs, Metrics and Traces Directly from Your IDE. No Reproducing or Redeployments required*
  - <https://lightrun.com/> 
- **OpenTelemetry**
  - → DevOps/Monitoring
  - SDK
    - <https://github.com/open-telemetry/opentelemetry-java>
  - Java-Agent
    - *offload responsibility from the application (no application code required)*
    - viele [frameworks und libs](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md#libraries---frameworks) ohne zusätzl. konfiguration unterstützt ("auto instrumentation"), custom telemetry für alle anderen (über code + annotationen)
    - https://github.com/open-telemetry/opentelemetry-java-instrumentation
    - [Youtube: OpenTelemetry Agent and Collector: Telemetry Built-in Into All Software](https://www.youtube.com/watch?v=cHiFSprUqa0)
- **ycrash** 💰
  - <https://ycrash.io/>
  - *Automatically captures & analyzes GC Logs, thread dumps, heap dumps & several more artifacts to identify root cause.*
  - *compliments Monitoring Tools*
- **Arthas**
  - *allows developers to troubleshoot production issues for Java applications without modifying code or restarting servers*
  - *Often times, the production system network is inaccessible from the local development environment. If issues are encountered in production systems, it is impossible to use IDEs to debug the application remotely. More importantly, debugging in production environment is unacceptable, as it will suspend all the threads, resulting in the suspension of business services.*
  - <https://github.com/alibaba/arthas/>
