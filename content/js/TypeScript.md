---
tags: [Notebooks/Javascript]
title: TypeScript
parent: JavaScript
---

# Typescript
- <https://goalkicker.com/TypeScriptBook2>
- https://github.com/semlinker/awesome-typescript
- Playground: https://www.typescriptlang.org/play/
- https://github.com/basarat/typescript-book
- https://github.com/Microsoft/TypeScript-New-Handbook
- https://typescript-exercises.github.io/


## Tools
- tsdx
    - https://github.com/palmerhq/tsdx
    - *Zero-config CLI for TS package development*
- ts-migrate
    - *tool for helping migrate [js] code to TypeScript*
    - https://github.com/airbnb/ts-migrate
- tsconfig/bases
    - *TSConfigs for you to extend in your apps, tuned to a particular runtime environment* (deno, node, svelte, ...)
    - https://github.com/tsconfig/bases
- typescript-eslint
    - "Nachfolger" von tslint
    - https://github.com/typescript-eslint/typescript-eslint


## Libs
- https://github.com/DefinitelyTyped/DefinitelyTyped (@types)
- https://github.com/TypeStrong/ts-node
- https://www.npmjs.com/package/ts-node-dev
- marshal.ts
    - https://github.com/marcj/marshal.ts
    - *by far fastest serialization implementation to marshal JSON-representable data from JSON objects to class instances to database records and vice versa*
    - nach eigenen Angaben schneller als class-transformer
- TypeORM
    - https://github.com/typeorm/typeorm
- TypedJSON
    - https://github.com/JohnWeisz/TypedJSON
    - *Typed JSON parsing and serializing for TypeScript that preserves type information*
- overmind
    - https://github.com/cerebral/overmind
    - state management
- class-validator
    - https://github.com/typestack/class-validator
    - *Validation made easy using TypeScript decorators*
- Test
    - ts-mockito
        - https://www.npmjs.com/package/ts-mockito
    - ts-jest
        - https://github.com/kulshekhar/ts-jest


## Deno
- https://deno.land/
- REPL: https://deno.town/
- *has the TypeScript compiler built in, so while there still is transpilation, it's invisible to the developer.*

### Libs
- Reno
    - *routing library designed to sit on top of Deno's standard HTTP module*
    - https://github.com/reno-router/reno
- Aleph.js
    - *The React Framework in Deno, inspired by Next.js*
    - *file-system routing, SSR & SSG, HMR with Fast Refresh, and more*
    - https://github.com/alephjs/aleph.js
- oak
    - https://github.com/oakserver/oak
    - *middleware framework for Deno's net server*
- DenoDB
    - *MySQL, SQLite, MariaDB, PostgreSQL and MongoDB ORM for Deno*
    - https://github.com/eveningkid/denodb *1.1k
