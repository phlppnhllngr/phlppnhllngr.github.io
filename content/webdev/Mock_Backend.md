---
tags: [Notebooks/Webdev]
title: Mock Backend
created: '2019-04-16T08:55:31.426Z'
modified: '2021-07-03T18:38:40.923Z'
parent: Webdev
---

# Mock Backend

## Öffentliche APIs und Services
- **placeholder.com**
  - <https://placeholder.com/>
  - Images
- **jsonplaceholder**
  - <http://jsonplaceholder.typicode.com/>
- **httpstat.us**
  - <https://httpstat.us/>
  - nur Statuscodes, kein Body, optionale Verzögerung
- **mockapi**
  - <https://www.mockapi.io/docs>
- **httpbin**
  - <http://httpbin.org/>
  - verschiedene Content-Types (xml, json, gzip, ...), http & https
- **mocky**
  - <https://github.com/julien-lafont/Mocky> *1.7k
  - <https://www.mocky.io/>
- **jsonstub**
  - <http://jsonstub.com/>
- **mockoon**
  - <https://mockoon.com/>
  - Desktop-App
  - <https://github.com/mockoon/mockoon> *1100
- **postman**
  - <https://www.codingular.com/2019/04/mocking-api-using-postman/>
  - privater Mock-Server nur mit Api-Key
- **mockaroo**
  - random data generator, file download (csv, json, sql, ...) & rest api
  - <https://mockaroo.com/>
- **api-with-github**
  - <https://apiwithgithub.com/>
  - <https://github.com/mddanishyusuf/json-apis-with-github>
- **mocklets**
  - <https://mocklets.com/>
  - free & premium tiers
- **crudcrud**
  - <https://crudcrud.com/>
- **crudpi.io**
  - <https://crudpi.io/>
- **easy-mock**
  - *Support RESTful*
  - *Support Swagger / OpenAPI Specification*
  - <https://github.com/easy-mock/easy-mock> *8.6k
- **mockit**
  - <https://mockit.netlify.com/>
  - <https://github.com/boyney123/mockit>
  - neu (04/2019)
  - simpel, wenig konfigurierbar
- **castlemock**
  - *RESTful APIs and SOAP web services.*
  - *can create mocked services based on WSDL, WADL, Swagger and RAML definition files*
  - Installation: .war oder Docker-Image
  - <https://github.com/castlemock/castlemock> *176


## Code based

### js
- **json-server**
  - <https://github.com/typicode/json-server> *44.000
  - gut konfigurierbar, Middlewares
  - gePOSTete daten können gespeichert werden
  - kann nur json (?)
- **dyson**
  - <https://github.com/webpro/dyson> *800
  - sehr konfigurierbar, middlewares
  - delay, fake data, dynamic http status, cors, ...
- **stubborn**
  - <https://github.com/ybonnefond/stubborn> *5
  - *It is basically nock meets Dyson*
- **miragejs**
  - <https://miragejs.com/docs/main-concepts/route-handlers/>
  - im Gegensatz zu vielen anderen clientseitig (patcht intern XHR & fetch)
- **pretender**
  - <https://github.com/pretenderjs/pretender>
  - clientseitig
- **msw**
  - <https://github.com/mswjs/msw>
  - benutzt Serviceworker
  - *Utilizing the Service Worker API, MSW responds to requests with your mock definition on the network level. This way your application knows nothing about the mocking.*

### Java
- **WireMock**
  - <http://wiremock.org/>
  - <https://github.com/tomakehurst/wiremock> *3600
  - gut konfigurierbar (java oder json)
  - randomizable delays, faulty reponses
- **hoverfly**
  - <https://github.com/SpectoLabs/hoverfly-java> *100

### Andere Sprachen
- **mockserver**
  - <https://github.com/mock-server/mockserver>
  - <http://www.mock-server.com>
  - js und java
  - gut konfigurierbar
  - Maven-Plugin zur Nutzung für Tests
- **prism**
  - <https://github.com/stoplightio/prism>
  - *Turn any OpenAPI file into an API server with mocking, transformations, validations, and more.*
  - <https://stoplight.io/open-source/prism/>
- **mocking hans**
  - <https://github.com/loremipsum/mocking-hans> *20
  - TS
