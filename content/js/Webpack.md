---
tags: [Notebooks/Javascript]
title: Webpack
created: '2019-02-05T09:29:09.764Z'
modified: '2021-04-18T16:31:13.012Z'
parent: JavaScript
---

# Webpack

## Plugins
- **common-shake**
  - https://github.com/indutny/webpack-common-shake
  - *allows tree shaking of commonjs modules*
- **workbox**
  - https://developers.google.com/web/tools/workbox/modules/workbox-webpack-plugin
- **add-asset-html**
  - *add assets to be injected by the html webpack plugin*
  - https://www.npmjs.com/package/add-asset-html-webpack-plugin
- **critters**
  - *Critters is a Webpack plugin that inlines your app's critical CSS and lazy-loads the rest*
  - https://github.com/GoogleChromeLabs/critters
- **webpack-shell-plugin-next**
  - https://www.npmjs.com/package/webpack-shell-plugin-next
  - *This plugin allows you to run any shell commands before or after webpack 4 builds*
- **prerender-spa**
  - *Flexible, framework-agnostic static site generation for sites and SPAs built with webpack*
  - https://github.com/chrisvfritz/prerender-spa-plugin
- **purgecss**
  - https://github.com/FullHuman/purgecss-webpack-plugin
- **size**
  - https://github.com/GoogleChromeLabs/size-plugin
  - zeigt Veränderungen der Chunkgröße bei neu-build
- **script-ext-html**
  - https://www.npmjs.com/package/script-ext-html-webpack-plugin
  - *Enhances html-webpack-plugin functionality with different deployment options for your scripts including:
async, defer, type="module", any custom attributes you wish to add, inlining, preload, prefetch*
- **dotenv plugin**
  - *get values from .env (properties) file and make them available via process.env.X*
  - *wraps dotenv and environment plugin*
  - https://www.npmjs.com/package/dotenv-webpack
- **preload**
  - https://github.com/GoogleChromeLabs/preload-webpack-plugin
  - *A Webpack plugin for automatically wiring up asynchronous (and other types) of JavaScript chunks using <link rel='preload'>. This helps with lazy-loading. Note: This is an extension plugin for html-webpack-plugin - a plugin that simplifies the creation of HTML files to serve your webpack bundles. This plugin is a stop-gap until we add support for asynchronous chunk wiring to script-ext-html-webpack-plugin.*
- **ForkTsCheckerWebpackPlugin**
- **import-http**
  - https://github.com/egoist/import-http
  - Module von URL statt von lokalen node_modules referenzieren
- **friendly-errors-webpack-plugin**
  - https://www.npmjs.com/package/friendly-errors-webpack-plugin


## Loader
- *out of the box, webpack only knows how to handle require- and import-statements of js- and json-files*
- **markdown-loader**
  - https://www.npmjs.com/package/markdown-loader
- **pug html loader**
  - https://www.npmjs.com/package/pug-html-loader
- **ts-loader**
- **awesome-typescript-loader**
- **esbuild-loader**
  - *offering faster alternatives for transpilation (eg. babel-loader/ts-loader) and minification (eg. Terser)*
  - https://github.com/privatenumber/esbuild-loader *1100
- **mark-loader**
  - *Inspect module load time using performance.mark and performance.measure. This dev time loader is useful for calling out candidates for lazy loading.*
  - https://github.com/statianzo/mark-loader


## Utils
- **webpack-merge**
  - https://www.npmjs.com/package/webpack-merge
- **webpack-chain**
  - https://github.com/neutrinojs/webpack-chain
- **webpack-dashboard**
  - GUI für webpack-dev-server
  - https://github.com/FormidableLabs/webpack-dashboard
- **Webpack Bundle Analyzer**
  - https://www.npmjs.com/package/webpack-bundle-analyzer
- **inspectpack**
  - *inspection tool for Webpack frontend JavaScript bundles.*
  - https://docs.google.com/document/d/12rroXl7PU1tdF5TTiE_0C1a8QdL6sBdZQ8C9BWThDJ4/edit
- **webpack-visualizer**
  - https://github.com/chrisbateman/webpack-visualizer
  - *Visualize and analyze your Webpack bundle to see which modules are taking up space and which might be duplicates*
- **webpack-hot-middleware**
  - https://www.npmjs.com/package/webpack-hot-middleware


## Starter
- **webpack-boilerplate**
  - <https://github.com/taniarascia/webpack-boilerplate>
  - *A sensible webpack 5 boilerplate*
