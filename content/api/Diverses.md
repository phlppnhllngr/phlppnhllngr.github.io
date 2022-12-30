---
tags: [Notebooks/API]
title: Diverses
created: '2019-10-16T21:52:04.220Z'
modified: '2021-07-09T18:01:12.807Z'
parent: API
---

# Diverses

## API-Design
- <https://opensource.zalando.com/restful-api-guidelines/>
- [HN - Paginating Requests in APIs](https://news.ycombinator.com/item?id=31541070)
- <https://blog.frankel.ch/evolve-apis/>
  - API Gateways
  - API Versioning 

## Fehlerhandling
- **RFC 7807 - Problem Details for HTTP APIs**
  - ```json
    {
      "type": "https://example.com/probs/out-of-credit",
      "title": "You do not have enough credit.",
      "detail": "Your current balance is 30, but that costs 50.",
      "instance": "/account/12345/msgs/abc",
      "balance": 30,
      "accounts": ["/account/12345", "/account/67890"]
    }
    ```
  - <https://datatracker.ietf.org/doc/html/rfc7807>
  - <https://codeopinion.com/problem-details-for-better-rest-http-api-errors/>
  - <https://www.mscharhag.com/api-design/rest-error-format> 



## binäre Datenformate
- **Protocol Buffers**
  - im Vergleich zu json:
    - <https://www.youtube.com/watch?v=uGYZn6xk-hA/>
    - (deutlich) leichtgewichtiger (<https://nilsmagnus.github.io/post/proto-json-sizes/>)
    - geeigneter für große Datenmengen
    - nicht self-contained, benötigt .proto-Schemata
- **colfer**
  - <https://github.com/pascaldekloe/colfer/>
- **bebop**
  - laut eigenen Angaben schneller als google protobuf
  - C#, TS
  - <https://github.com/RainwayApp/bebop/>


## gRPC
- Microservicekommunikation mit protocol buffers, Alternative zu Http/Rest/Json
- <https://grpc.io/>
- <https://github.com/fullstorydev/grpcurl/>
- <https://github.com/grpc/grpc-web/>
