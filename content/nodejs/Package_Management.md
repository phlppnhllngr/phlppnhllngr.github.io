---
tags: [Notebooks/Node]
title: Package Management
created: '2019-02-17T20:48:46.024Z'
modified: '2021-07-21T06:55:12.003Z'
parent: Node.js
---

# Package Management
- https://github.com/pnpm/benchmarks-of-javascript-package-managers

## npm
- http://www.tiernok.com/posts/2019/faster-npm-installs-during-ci/
- https://medium.com/@jeromewus/how-to-speed-up-node-js-modules-installation-in-ci-cd-pipeline-as-of-2020-4865d77c0eb7 (28.3.20)

### CLI
- https://docs.npmjs.com/cli-documentation

### Tools
- https://github.com/sindresorhus/awesome-npm
- **npm-gui**
  - https://github.com/q-nick/npm-gui/
- **pwr**
  - https://github.com/jesusprubio/pwr
  - *The (cheated) interactive CLI for npm*
- **glicky**
  - https://github.com/alex-saunders/glicky
  - Browser-GUI
- **volta**
  - https://volta.sh/
  - *Volta’s job is to manage your JavaScript command-line tools, such as node, npm, yarn, or executables shipped as part of JavaScript packages. Similar to package managers, Volta keeps track of which project (if any) you’re working on based on your current directory. The tools in your Volta toolchain automatically detect when you’re in a project that’s using a particular version of the tools, and take care of routing to the right version of the tools for you.*

### Tipps
- **package-lock.json**
  - *Even if you use exact dependency versions, the dependencies of your dependencies won't. That's why you use the package-lock file.*
- **Plathalter in npm-Scripts**
  - https://www.stefanjudis.com/today-i-learned/package-json-values-are-accessible-in-npm-yarn-scripts/
  ```json
  {
    "config": { "src": "./src/js" },
    "scripts": {
      "transpile": "babel $npm_package_config_src" // %npm_package_config_src% auf windows
    }
  }
  ```
- `npm link` um symlinked modules in node_modules zu verwenden
- ```
  "myscript": "run-some-program",
  "myscript-with-args": "npm run myscript -- --somekey=someval"
  ```
- `npm i --ignore-scripts` um (postinstall-)scripts zu deaktivieren


## yarn
  - **workspaces**
    - für Monorepos
  - **yarn 2** ("berry")
    - https://github.com/yarnpkg/berry
    - https://dev.to/arcanis/introducing-yarn-2-4eh1?q=1
    - *new features*
      - *apply changes to a specific package in your dependency tree*
        `"left-pad": "patch:left-pad@1.3.0#./my-patch.patch"`
      - Run commands on all workspaces with `yarn workspaces foreach`
      - [typescript plugin](https://github.com/yarnpkg/berry/tree/master/packages/plugin-typescript) *which will automatically add the relevant @types/ packages each time you run yarn add*


## pnpm
  - https://pnpm.js.org/
  - *disk space efficient package manager - pnpm uses hard links and symlinks to save one version of a module only ever once on a disk.*
