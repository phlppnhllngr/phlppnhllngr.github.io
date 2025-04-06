---
title: Diverses
parent: API
---

# Diverses

## API-Design
- <https://opensource.zalando.com/restful-api-guidelines/>
- **How to (and how not to) design REST APIs**
  - <https://github.com/stickfigure/blog/wiki/How-to-%28and-how-not-to%29-design-REST-APIs>
  - [HN Diskussion, 11/2023](https://news.ycombinator.com/item?id=38103310)
- **json patch**
  - *JSON Patch is a format for describing changes to a JSON document. It can be used to avoid sending a whole document when only a part has changed. When used in combination with the HTTP PATCH method, it allows partial updates for HTTP APIs in a standards compliant way.
The patch documents are themselves JSON documents.
JSON Patch is specified in RFC 6902 from the IETF.*
 - <https://jsonpatch.com/>


## Paginierung
- [HN - Paginating Requests in APIs](https://news.ycombinator.com/item?id=31541070)


## Idempotenz
- <https://docs.stripe.com/api/idempotent_requests>
- <https://old.reddit.com/r/programming/comments/1cnvy7y/how_stripe_prevents_double_payment_using/>


## API Versionierung
- <https://blog.frankel.ch/evolve-apis/>
  - API Gateways
  - API Versioning
- <https://stripe.com/blog/api-versioning>
- <https://apisyouwonthate.com/blog/api-evolution-for-rest-http-apis>
- <https://apigility.org/documentation/api-primer/versioning>
  - via URL (Pfad)
  - via Media Type
  - via Header
  - via Query Param 


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


## Unified API
- **Nango**
  - *A single API for all your integrations.*
  - *simplifies integrating your product with any external API*
  - *Over 100 Pre-configured APIs, Easy to Add Your Own* 
  - <https://github.com/nangoHQ/nango>
- **Merge**
  - <https://www.merge.dev/> 
- **Revert**
  - <https://www.revert.dev/>
  - <https://github.com/revertinc/revert>
