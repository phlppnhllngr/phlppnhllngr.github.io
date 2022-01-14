---
tags: [Notebooks/API]
title: Test
created: '2019-02-10T19:51:26.605Z'
modified: '2021-08-08T10:11:48.795Z'
parent: API
---

# Test

- **strest**
  - <https://github.com/eykhagen/strest/> *1700
  - node_module, docker image
  - yaml
  - *request chaining, random data generation, vscode extension, response validation*
- **Postman/Newman** → API/Entwicklungstools
- **katalon** 💰
  - API / E2E
  - <https://www.katalon.com/>
- **rest-assured**
  - <https://github.com/rest-assured/rest-assured/>
  - Java
- **karate**
  - <https://github.com/intuit/karate/> *5.5k
  - [Docs](https://karatelabs.github.io/karate/)
  - DSL, Java
  - *combine API test-automation, mocks, performance-testing and even UI automation into a single, unified framework.*
  - *The BDD syntax popularized by Cucumber is language-neutral, and easy for even non-programmers.*
  - *Powerful JSON & XML assertions are built-in, and you can run tests in parallel for speed. Test execution and report generation feels like any standard Java project.*
  - *A Java API exists for those who prefer to programmatically integrate Karate's rich automation and data-assertion capabilities.*
  - *But there's also a stand-alone executable for teams not comfortable with Java. You don't have to compile code. Just write tests in a simple, readable syntax - carefully designed for HTTP, JSON, GraphQL and XML. And you can mix API and UI test-automation within the same test script.*
- **frisby**
  - <https://github.com/vlucas/frisby/>
  - *built on top of Jest*
  - JS
- **pact**
  - *testing HTTP and message integrations using contract tests*
  - <https://docs.pact.io/>
  - JS, Java, ...
- **RAFT**
  - REST API Fuzz Testing
  - <https://github.com/microsoft/rest-api-fuzz-testing/>
  - Bestandteile
    - RESTler (restler-fuzzer)
      - *finding security and reliability bugs*
      - *For a given service with an OpenAPI/Swagger specification, RESTler analyzes its entire specification, and then generates and executes tests that exercise the service through its REST API.*
      - Tutorial (Docker): <https://phts.medium.com/running-restler-on-docker-69210b78190e/>
      - <https://github.com/microsoft/restler-fuzzer/>
    - OWASP ZAP
- **cats**
  - *Automation testing is cool, but what if you could automate testers? More specifically, what if you could automate all of the process of writing test cases, getting test data, writing the automation tests and then running them? This is what CATS does.*
  - *Generate tests at runtime based on OpenApi specs*
  - *enables you to generate hundreds of API tests within seconds with no coding effort.*
  - *All tests cases are generated and run automatically based on a pre-defined set of 72 Fuzzers. The Fuzzers cover different types of testing like: negative testing, boundary testing, structural validations, security and even end-to-end functional flows.*
  - <https://github.com/Endava/cats/> *395
- **RESTest**
  - *Automated Black-Box Testing of RESTful Web APIs*
  - *test cases are automatically derived from the OpenAPI Specification (OAS) of the API under test*
  - *RESTest generates REST Assured test cases* (Java)
  - *test failures are collected and they can be easily spotted and analyzed in a user-friendly GUI, built with Allure*
  - <https://github.com/isa-group/RESTest>


## Stress, Load, Resilience
- **Gremlin**
  - <https://www.gremlin.com/blog/introducing-gremlin-free/>
  - *provides the ability to run both Shutdown and CPU attacks on your hosts or containers, controlled by a simple user interface at no cost*
  - free & 💰
- **Apache Jmeter**
  - <http://jmeter.apache.org/index.html/>
  - *100% pure Java application designed to load test functional behavior and measure performance*
  - *Ability to load and performance test many different applications/server/protocol types: Web - HTTP, HTTPS, SOAP / REST Webservices, FTP, Database via JDBC, ...*
- **Gatling**
  - <https://gatling.io/>
  - <https://github.com/gatling/gatling/> *4400
  - *load test your web applications*
  - Scala DSL
  - Plugin für Maven
- **k6**
  - <https://k6.io/>
  - <https://github.com/loadimpact/k6/> *5.6k
  - *A modern load testing tool, using Go and JavaScript*
  - *Like unit-testing, for performance*
  - CLI oder Docker
  - https://k6.io/blog/load-testing-with-postman-collections
- **wrk**
  - CLI
  - <https://github.com/wg/wrk/> *29.3k
- **plow**
  - <https://github.com/six-ddc/plow/> *2k
  - *high-performance HTTP benchmarking tool with real-time web UI and terminal displaying*
  - Go / Docker
- **autocannon**
  - NodeJs
  - *greatly inspired by wrk and wrk2*
  - <https://github.com/mcollina/autocannon/> *5.2k
- **locust**
  - Python
  - *easy to use, scriptable and scalable performance testing tool. You define the behaviour of your users in regular Python code*
  - *has a user friendly web interface that shows the progress of your test in real-time*
  - <https://github.com/locustio/locust>
- **loader.io** 💰
  - <https://loader.io/>
  - *load testing service that allows you to stress test your web-apps & apis with thousands of concurrent connections*
