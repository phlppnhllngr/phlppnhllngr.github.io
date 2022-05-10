---
tags: [Notebooks/Javascript]
title: Monorepo
created: '2020-01-09T20:30:47.318Z'
modified: '2021-04-13T15:02:24.532Z'
parent: JavaScript
---

# Monorepo
- <https://medium.com/@maoberlehner/monorepos-in-the-wild-33c6eb246cb9>
- <https://doppelmutzi.github.io/monorepo-lerna-yarn-workspaces/>
- <https://codewithhugo.com/yarn-workspaces-application-monorepo/>
- nur einen Teil des Monorepos auschecken mit `git sparse-checkout`


## Tools
- **yarn (2) workspaces**
  - nur 1 node_modules (im root folder), in dem alle Deps landen (spezifische Deps können mit noHoist davon ausgeschlossen werden)
- **yarn workspaces + lerna**
- **npm**
  - link
- **bolt**
- **bit**
  - *platform for building with components and using them to compose apps and systems.*
  - *isolates components, giving us the freedom to build and work with each component as an isolated module*
  - <https://github.com/teambit/bit>
- **Turborepo** 
  - <https://turborepo.org/> 
- **lerna**
  - älter als yarn workspaces, kann mehr
  - Versionierung für alle gleich oder voneinander unabhängig wählbar
  - "Umzug" aus versch. Git-Repos unter Beibehaltung der Historie (`lerna import`)
  - möglich, nur ein node_modules im root folder zu haben (mit `--hoist`)
  - <https://lernajs.io/>
  - <https://github.com/lerna/lerna>
  - zum Verwalten eines Monorepos
  - Beispiele: babel, gridsome
    ```
    app
    |-packages
    |  |-shared
    |  |  |-package.json (name: @app/shared, version: 1.0.0)
    |  |  |-index.js
    |  |-client
    |  |  |-package.json (name: @app/client, dependencies: @app/shared: 1.0.0, lodash-es: latest)
    |  |  |-index.js
    |  |  |-node_modules
    |  |  |  |-@app
    |  |  |  |  |-shared (symlink auf packages/shared)
    |  |-server
    |  |  |-package.json (name: @app/server, dependencies: @app/shared: 1.0.0)
    |  |  |-index.js
    |-lerna.json
    |-package.json
    ```
  - macht `npm install` für 3rd party dependencies, symlinks in node_modules für eigene Packages
  - <u>Tooling</u>
    - **syncpack**
      - <https://github.com/JamieMason/syncpack>
      - *Manage multiple package.json files, as in Lerna Monorepos*
      - *Ensure that multiple packages requiring the same dependency define the same version*
    - **lerna-wizard**
      - <https://github.com/webuniverseio/lerna-wizard>
      - *command line wizard for lerna*
