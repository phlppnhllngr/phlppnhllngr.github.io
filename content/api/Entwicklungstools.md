---
title: Entwicklungstools
parent: API
---

# Entwicklungstools
-> siehe auch Webdev/Mock Backends

## Clients
- **Insomnia**
  - <https://insomnia.rest/>
  - Plugins, z.B. um Zufallsdaten zu generieren
    - <https://insomnia.rest/plugins/>
    - <https://support.insomnia.rest/article/26-plugins/>
    - <https://npms.io/search?q=insomnia-plugin/>
    - <https://www.npmjs.com/package/insomnia-plugin-faker/>
  - CLI
    - "Inso"
    - benötigt nodejs
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
    - node_module; <https://www.npmjs.com/package/newman/>
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
- **HTTP Toolkit**
  - *for debugging, testing and building with HTTP(S) on Windows, Linux & Mac*
  - *intercept, inspect & rewrite HTTP(S) traffic, from everything to anywhere. Explore Android app traffic, mock requests between your microservices, and x-ray your browser traffic to debug, understand and test anything*
  - <https://github.com/httptoolkit/httptoolkit>
- **HTTPie**
  - 03/2022: private beta 
  - <https://httpie.io/>
- **Thunder Client** -> IDE/VSCode/Plugins
- **Nightingale**
  - closed source 
  - <https://nightingale.rest/> 
- **Yaade**
  - *open-source, self-hosted, collaborative API development environment.*
  - *self-hosted Postman alternative*
  - <https://news.ycombinator.com/item?id=30895372>
- **Hurl**
  - *command line tool that runs HTTP requests defined in a simple plain text format*
  - *can chain requests, capture values and evaluate queries on headers and body response. Hurl is very versatile: it can be used for fetching data, testing HTTP sessions and testing XML / JSON APIs.* 
  - <https://hurl.dev/>
  - <https://gitlab.com/everyonecancontribute/dev/hurl-playground>
- **RecipeUI**
  - <https://github.com/RecipeUI/RecipeUI>
- **bruno**
  - <https://www.usebruno.com/>
  - <https://github.com/usebruno/bruno>
- **Insomnium**
  - *fork of Kong/insomnia* 
  - <https://github.com/ArchGPT/insomnium>
- **Restfox**
  - <https://restfox.dev/>
- **Kreya**
  - <https://kreya.app/>  


## Generatoren
- **quicktype**
  - *generates strongly-typed models and serializers from JSON, JSON Schema, TypeScript, and GraphQL queries*
  - *Target Languages: js, java, ...*
  - <https://github.com/quicktype/quicktype/>
- **openapi-generator**
  - <https://github.com/OpenAPITools/openapi-generator/>
  - *allows generation of API client libraries (SDK generation), server stubs, documentation and configuration automatically given an OpenAPI Spec (v2, v3)*

## Andere
- **swagger**
  - *OpenAPI = Specification, Swagger = Tools for implementing the specification* 
  - <https://swagger.io/>
  - <https://swagger.io/swagger-editor/>
- **OpenAPI.Tools**
  - <https://openapi.tools/> 
- **openapi-cop**
  - <https://github.com/EXXETA/openapi-cop/>
  - node_module
  - *A proxy that validates responses and requests against an OpenAPI document*
- **har2openapi**
  - *automatically creates API documentation via a OpenApi Spec (OAS) file by using network requests captured in one or more HAR files* 
  - <https://github.com/dcarr178/har2openapi> 
- **Akita**
  - *watches API traffic to automatically generate OpenAPI specs in just minutes, completely black box, without requiring any code or config changes.*
  - *Akita is able to tell you:*
    - *Endpoints added that expose new functionality*
    - *Parameters removed that may break existing clients*
    - *Simple type changes (ex string to int) that can pollute data pipelines*
    - *Complex type changes (ex phone number to datetime) that can break dependencies*
  - <https://docs.akita.software/docs/>
- **mitmproxy2swagger**
  - *automatically converting mitmproxy captures to OpenAPI 3.0 specifications. This means that you can automatically reverse-engineer REST APIs by just running the apps and capturing the traffic.*   
  - <https://github.com/alufers/mitmproxy2swagger>
- **Charles**
  - *is an HTTP proxy / HTTP monitor / Reverse Proxy that enables a developer to view all of the HTTP and SSL / HTTPS traffic between their machine and the Internet. This includes requests, responses and the HTTP headers (which contain the cookies and caching information).* 
  - <https://www.charlesproxy.com/> 
