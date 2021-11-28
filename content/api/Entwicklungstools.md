---
tags: [Notebooks/API]
title: Entwicklungstools
created: '2019-02-14T20:17:47.102Z'
modified: '2021-06-10T08:28:17.816Z'
parent: API
---

# Entwicklungstools

## Clients
- **Insomnia**
  - <https://insomnia.rest/>
  - Plugins, z.B. um Zufallsdaten zu generieren
    - <https://insomnia.rest/plugins/>
    - <https://support.insomnia.rest/article/26-plugins/>
    - <https://npms.io/search?q=insomnia-plugin/>
    - <https://www.npmjs.com/package/insomnia-plugin-faker/>
  - CLI ("Inso")
- **Postman**
  - <https://www.getpostman.com/>
  - Tests (JavaScript), Mock-Server
  - scopes
    <table>
      <thead>
        <th>scope</th>
        <th>getter</th>
        <th>setter persistent?</th>
      </thead>
      <tbody>
        <tr>
          <td>workspace/globals</td>
          <td>pm.globals.get('x') oder globals.x</td>
          <td>y</td>
        </tr>
        <tr>
          <td>environment</td>
          <td>pm.environment.get('x')</td>
          <td>y</td>
        </tr>
        <tr>
          <td>collection (variables)</td>
          <td>pm.environment.get('x')</td>
          <td>n</td>
        </tr>
      </tbody>
    </table>
  - function library
    ```js
    pm.globals.set('library', function functions() {
      function myFunc1() {}
      function myFunc2(x) {}
      return {
          myFunc1,
          myFunc2
      }
    } + '; functions();');

    // woanders
    const library = eval(globals.library);
    library.myFunc1();
    ```
  - newman
    - <https://www.npmjs.com/package/newman/>
    - *the cli companion for postman*
    - *allows you to effortlessly run and test a Postman collection directly from the command-line. ... easily integrate it with your continuous integration servers and build systems.*
- **talend api tester**
  - restlet.com
  - chrome plugin
- ~~postwoman~~ **hoppscotch**
  - <https://hoppscotch.io/>
  - Browser-App, Offline-Support (pwa)
  - viele Features (pre-/post-req-scripts, ...)
  - <https://github.com/hoppscotch/hoppscotch/> *19.3k
  - CLI
    - <https://github.com/hoppscotch/hopp-cli/>
- **milkman**
  - <https://github.com/warmuuh/milkman/> *385
  - *heavily inspired by Postman. not limited to e.g. http requests. other things are possible, like database-requests or GRPC, GraphQl, etc...*


## Andere
- **swagger**
  - swagger-inflector
    - *uses the Swagger Specification to drive an API implementation. The spec drives the creation of routes and controllers automatically, matching methods and method signatures from the implementation. To allow for an iterative development, the framework will mock responses for any unimplemented methods, based on the specification. You have full control over the mapping of controllers to classes and methods as well as models.*
    - <https://github.com/swagger-api/swagger-inflector>
- **openapi-cop**
  - <https://github.com/EXXETA/openapi-cop/>
  - node_module
  - *A proxy that validates responses and requests against an OpenAPI document*
- **openapi-generator**
  - <https://github.com/OpenAPITools/openapi-generator/>
  - *allows generation of API client libraries (SDK generation), server stubs, documentation and configuration automatically given an OpenAPI Spec (v2, v3)*
- **Akita**
  - *watches API traffic to automatically generate OpenAPI specs in just minutes, completely black box, without requiring any code or config changes.*
  - *Akita is able to tell you:*
    - *Endpoints added that expose new functionality*
    - *Parameters removed that may break existing clients*
    - *Simple type changes (ex string to int) that can pollute data pipelines*
    - *Complex type changes (ex phone number to datetime) that can break dependencies*
  - <https://docs.akita.software/docs/>
- **quicktype**
  - *generates strongly-typed models and serializers from JSON, JSON Schema, TypeScript, and GraphQL queries*
  - *Target Languages: js, java, ...*
  - <https://github.com/quicktype/quicktype/>
