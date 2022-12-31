---
tags: [Notebooks/API]
title: 'Backends'
created: '2021-07-09T18:00:56.352Z'
modified: '2021-09-02T10:15:44.116Z'
parent: API
---

# Backends
- → Automatisierung/Lowcode (low code APIs)
- **supabase**
  - <https://github.com/supabase/supabase/> <img loading="lazy" src="https://img.shields.io/github/stars/supabase/supabase?style=flat-square"/>
  - *The open source Firebase alternative.*
  - *adds realtime and RESTful APIs to your existing PostgreSQL database without a single line of code*
  - *listen to database changes*
  - *Create a backend in less than 2 minutes.*
    - *Postgres Database*
    - *Authentication*
    - *instant APIs*
    - *realtime subscriptions and Storage*
    - *Serverless functions ("Edge Functions")*
  - basiert u.a. auf postgrest
  - [Is Supabase Legit? Firebase Alternative Breakdown - Fireship Youtube, 04/2021](https://www.youtube.com/watch?v=WiwfiVdfRIc)
  - [supabase crash course - traversy youtube, 07/21](https://www.youtube.com/watch?v=7uKQBl9uZ00)
- **api-platform**
  - *web framework designed to easily create API-first projects*
  - *dedicated to API-driven projects and implementing the Jamstack architecture*
  - *contains a PHP library (Core) to create fully featured hypermedia (or GraphQL) web APIs*
  - php, db, frontend (vue/react), api
  - <https://api-platform.com/>
- **postgREST**
  - <https://github.com/PostgREST/postgrest/> <img loading="lazy" src="https://img.shields.io/github/stars/PostgREST/postgrest?style=flat-square"/>
  - *serves a fully RESTful API from any existing PostgreSQL database*
  - *handles authentication (via JSON Web Tokens) and delegates authorization to the role information defined in the database*
- **Directus**
  - <https://github.com/directus/directus> <img loading="lazy" src="https://img.shields.io/github/stars/directus/directus?style=flat-square"/>
  - *suite of software that wraps custom SQL databases with a dynamic API and intuitive Admin App*
  - *database-first at it's foundation, far more "open", performant, and flexible [compared to other headless cms]*
  - Supported Databases: kein DB2
- **appwrite**
  - <https://github.com/appwrite/appwrite/> <img loading="lazy" src="https://img.shields.io/github/stars/appwrite/appwrite?style=flat-square"/>
  - <https://appwrite.io/>
  - *end-to-end backend server for Web, Mobile, Native, or Backend apps packaged as a set of Docker microservices*
  - *Appwrite API services aim to make developer's life a lot easier by hiding the complexity of common and repetitive software development tasks. Using Appwrite, you can easily manage*
    - *user authentication with multiple sign-in methods*
    - *a database for storing and querying user and team data*
    - *storage and file management*
    - *image manipulation and cropping*
    - *schedule cron tasks*
    - *and many other features to help you get more results in faster times and with a lot less code.*
- **hasura**
  - *turn your SQL database into a GraphQL API*
  - [Hasura in 100 Seconds - Fireship Youtube, 06/21](https://www.youtube.com/watch?v=xiZ61BkMKo8)
- **crux.land**
  - *free registry service meant for hosting small (≤ 20kB) single deno scripts*
  - *To use crux.land simply upload a file with one of the supported file extensions (ts, tsx, js, jsx) and if successful you will recieve a permanent link to said file. This link may be used in deno or browsers import*
  - <https://crux.land/>
- **swagger-inflector**
  - *uses the Swagger Specification to drive an API implementation. The spec drives the creation of routes and controllers automatically, matching methods and method signatures from the implementation. To allow for an iterative development, the framework will mock responses for any unimplemented methods, based on the specification. You have full control over the mapping of controllers to classes and methods as well as models.*
  - *Inflector uses the following libraries: swagger models for the swagger definition, Jackson for JSON processing, Jersey 2.32 for REST, Minimum Java 8*
  - <https://github.com/swagger-api/swagger-inflector>
- **PocketBase**
  - *Open Source realtime backend in 1 file*
  - *is an open source Go backend, consisting of: embedded database (SQLite) with realtime subscriptions, built-in files and users management, convenient Admin dashboard UI, and simple REST-ish API*
  - <https://pocketbase.io/>
  - <https://www.youtube.com/watch?v=Wqy3PBEglXQ>
  - <https://github.com/pocketbase/pocketbase> <img loading="lazy" src="https://img.shields.io/github/stars/pocketbase/pocketbase?style=flat-square"/>
  - [YT: Fireship - I built a $5 chat app with Pocketbase & Svelte. Will it scale?](https://www.youtube.com/watch?v=gUYBFDPZ5qk)
