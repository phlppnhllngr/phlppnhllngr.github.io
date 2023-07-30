---
title: Libs
parent: Node.js
grand_parent: JavaScript
---

# Libs

## Utility
- **cross-env**
  - <https://www.npmjs.com/package/cross-env>
  - Run scripts that set and use environment variables across platforms 
  - `"build": "cross-env key=value webpack" → process.env['key'] == 'value'`
- **dotenv**
  - <https://www.npmjs.com/package/dotenv>
  - *loads environment variables from a .env file into process.env*
- **ensure-node-env**
  - <https://www.npmjs.com/package/ensure-node-env>
  - vergleicht installierte node- und npm-Versionen mit denen in package.json ("engines")
  - funktioniert nicht mit nvm (?)
- **check-node-version**
  - wie ensure-node-env
  - <https://www.npmjs.com/package/check-node-version>
- **concurrently**
  - <https://www.npmjs.com/package/concurrently>
- **npm-run-all**
  - <https://www.npmjs.com/package/npm-run-all>
  - `npm-run-all` complex
  - `run-s` aka `npm-run-all -s` sequential, simple
  - `run-p` aka `npm-run-all -p` parallel, simple (<https://github.com/mysticatea/npm-run-all/blob/HEAD/docs/run-p.md>)
- **npm-check**
  - <https://www.npmjs.com/package/npm-check>
  - *Check for outdated, incorrect, and unused dependencies*
- **check-dependencies**
  - <https://www.npmjs.com/package/check-dependencies>
  - *Checks if currently installed npm/bower dependencies are installed in the exact same versions that are specified in package.json*
- **onchange**
  - *Use glob patterns to watch file sets and run a command when anything is added, changed or deleted.*
  - <https://www.npmjs.com/package/onchange>
- **patch-package**
  - <https://github.com/ds300/patch-package>
  - *lets app authors instantly make and keep fixes to npm dependencies*
- **secure-env**
  - <https://github.com/kunalpanchal/secure-env>
  - *secure .env-files*
- **wait-on**
  - <https://github.com/jeffbski/wait-on>
  - *will wait for files, ports, sockets, and http(s) resources to become available*
- **np**
  - <https://github.com/sindresorhus/np>
  - *A better `npm publish`*


## Lizenzen
- **license-checker**
  - *see all the license info for a module and its dependencies*
  - cli & js-lib
  - options
    - `--production` only show production dependencies
    - `--failOn <license names>`
    - `--onlyAllow foo;bar;baz`
      - semikolon-separierter String
    - `--customPath` to add a custom format
    - output formats: terminal, json, csv
    - ...
  - <https://github.com/davglass/license-checker>
  - <https://www.npmjs.com/package/license-checker>
- **npm-license-crawler**
  - *wrapper around license-checker to analyze several node packages (package.json files) as part of your software project. This way, it is possible to create a list of third party licenses for your software project in one go*
  - cli & js-lib
  - <https://github.com/mwittig/npm-license-crawler>
  - <https://www.npmjs.com/package/npm-license-crawler>
- **legally**
  - *Discover the license of npm packages that you are using*
  - cli & js-lib
  - <https://github.com/franciscop/legally>


## Web
- **node-http-proxy**
  - <https://github.com/http-party/node-http-proxy>
- **swagger-stats**
  - *API Observability. Trace API calls and Monitor API performance, health and usage statistics in Node.js Microservices*
  - <https://github.com/slanatech/swagger-stats>


## DB
- <https://github.com/arangodb/arangodb>
- <https://knexjs.org> - query builder, migrations
- <https://vincit.github.io/objection.js> - ORM
- <https://waterlinejs.org> - ORM
- <https://github.com/sequelize/sequelize> - ORM
- <https://github.com/prisma/prisma2> - ORM + migrations
- <https://github.com/mikro-orm/mikro-orm>


## Template engines
- **handlebars**
  - <https://github.com/wycats/handlebars.js/> *15.1k
  - Browser & nodejs
- **mustache**
- **pug**
  - <https://github.com/pugjs/pug> *18.9k
  - <https://pugjs.org/>
  - Browser & nodejs
- **twig.js**
  - <https://github.com/twigjs/twig.js/>
  - <https://twig.symfony.com/doc/3.x/> 


## Email
- <https://nodemailer.com>


## FS
- fs-extra
  - <https://www.npmjs.com/package/fs-extra>
  - *adds file system methods that aren't included in the native fs module and adds promise support to the fs methods*
