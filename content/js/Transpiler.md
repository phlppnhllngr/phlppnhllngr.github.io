---
tags: [Notebooks/Javascript]
title: Transpiler
created: '2019-02-14T14:42:18.470Z'
modified: '2021-05-08T13:11:15.014Z'
parent: JavaScript
---

# Transpiler

## Babel
- <https://babeljs.io/>
- *REPL*: https://babeljs.io/repl/build/master
- *babel-node*: https://babeljs.io/docs/en/babel-node (nicht transpilierten Code direkt ausführen)
- user handbook: https://github.com/jamiebuilds/babel-handbook/blob/master/translations/en/user-handbook.md
- https://github.com/babel/babel-upgrade - *tool for upgrading Babel versions*

### Plugins
- https://babeljs.io/docs/en/babel-plugin-proposal-optional-chaining 
- https://babeljs.io/docs/en/babel-plugin-proposal-class-properties 
- https://babeljs.io/docs/en/babel-plugin-proposal-nullish-coalescing-operator
- https://babeljs.io/docs/en/babel-plugin-proposal-pipeline-operator
- https://github.com/rpetrich/babel-plugin-transform-async-to-promises
- https://github.com/nd-02110114/babel-plugin-object-to-json-parse


## swc
- <https://github.com/swc-project/swc> ⭐6.1k
- *It's 16x faster than babel*
- rust based
- node module, Loader für Webpack


## sucrase
  - *an alternative to Babel that allows super-fast development builds*
  - *assumes that you're developing with a recent browser or recent Node.js version, so it focuses on compiling non-standard language extensions: JSX, TypeScript, and Flow*
  - *Sucrase is about 20x faster than Babel.*
  - <https://github.com/alangpierce/sucrase>
