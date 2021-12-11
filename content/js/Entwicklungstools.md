---
tags: [Notebooks/Javascript]
title: Entwicklungstools
created: '2019-02-14T15:00:44.173Z'
modified: '2021-09-13T11:27:57.427Z'
parent: JavaScript
---

# Entwicklungstools
- https://tooling.js.org/
- https://bundlers.tooling.report/

## Build
- https://css-tricks.com/comparing-the-new-generation-of-build-tools/ (8.4.21)
- **Parcel**
  - https://github.com/parcel-bundler/parcel
  - https://github.com/parcel-bundler/awesome-parcel
- **esbuild**
  - <span>https://github.com/evanw/esbuild <img src="https://badgen.net/github/stars/evanw/esbuild" alt="evanw/esbuild gh stars"/></span>
  - *The current build tools for the web are at least an order of magnitude slower*
  - Tools
    - estrella
      - *lightweight and versatile build tool based on the fantastic esbuild TypeScript and JavaScript compiler.*
      - *Rebuild automatically when source files change, ...*
      - https://github.com/rsms/estrella
- **snowpack**
    - https://github.com/snowpackjs/snowpack *12.8k
    - *Build web applications with less tooling and 10x faster iteration. No bundler required.*
    - benutzt intern esbuild
- **lyo**
  - https://github.com/bokub/lyo
  - *Lyo is the easiest way to transform Node.js modules into browser-compatible libraries*
- **Rome**
  - https://github.com/rome/tools
  - Toolchain (build, lint, test, ...)
  - Stand 4.5.21 beta; nur Linter
- **vite**
  - Dev-Server + Build
  - *Native-ESM powered web dev build tool*
  - *opinionated web dev build tool that serves your code via native ES Module imports during dev and bundles it with Rollup for production*
  - <https://github.com/vitejs/vite> ⭐30.3k
  - Tools
    - <https://github.com/vitejs/awesome-vite>
    - vitesse
      - *Opinionated Vite Starter Template*
      - <https://github.com/antfu/vitesse>
- **wmr**
  - https://github.com/preactjs/wmr
- **Webpack** → JS/Webpack
- **Rollup**
  - https://github.com/rollup
  - https://github.com/rollup/awesome


## Dokumentation
- **JSDoc**
  - http://usejsdoc.org/
  - https://fettblog.eu/typescript-jsdoc-superpowers/
  - um in VSCode zu "aktivieren", braucht es eine `jsconfig.json`-Datei im workspace-root mit Inhalt:
    ```json
    {
        "compilerOptions": {
            "checkJs": true,
            "target": "es6",
            "moduleResolution": "node"
        },
        "include": [
            "src/**/*"
        ]
    }
    ```
    https://code.visualstudio.com/docs/languages/jsconfig
- **storybook**
  - https://github.com/storybooks/storybook *45k
  - *tool for developing UI components in isolation for React, Vue, and Angular* [und andere]
  - *Get code snapshot tests out of the box with Storyshots, an official addon.*
  - *Reuse stories in your unit tests to confirm nuanced functionality.*
  - *Pinpoint UI changes with visual testing tools.*
  - https://www.chromatic.com/
- **better-docs**
  - https://github.com/SoftwareBrothers/better-docs
  - generiert Seite anhand von jsdoc


## Performance
- **Chrome**
  - performance monitor
  - https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference
- https://www.npmjs.com/package/benchmark
- http://jsben.ch/
- https://bundlephobia.com/
- https://jsperf.com/
- **window.performance**
  - mark
  - measure
    - https://dev.to/dazn/visualising-front-end-performance-bottlenecks-4da6
    - *will help us visualise functions in (Chrome) Developer Tools*
  - profile
  - https://chromestatus.com/features/5170190448852992


## Debugging
- **firefox-devtools/debugger**
  - https://github.com/devtools-html/debugger.html
  - *You can use it to debug code running locally in Firefox or running remotely, for example on an Android device running Firefox for Android.The debugger ships inside Firefox, and these pages describe how to use the version that's embedded in Firefox. However, you can also run it as a standalone web application, and can then use it to debug code running in other browsers and in Node.*
  - works with the Firefox and Chrome debugging protocols
- **Chrome Devtools**
  - getEventListeners(node)
  - monitorEvents(node, event?: string), unmonitorEvents(node)
  - node_modules von Debugging ausschließen: Triple Dots → Settings → Blackboxing 
- **Firefox Quantum aka Firefox Developer Edition**
  - https://www.mozilla.org/de/firefox/developer/


## CDNs
- **unpkg**
  - https://unpkg.com/
  - *unpkg is a fast, global content delivery network for everything on npm. Use it to quickly and easily load any file from any package using a URL like: unpkg.com/:package@:version/:file*
- **skypack**
  - *packages are preoptimized for browser use. it handles minification, browser polyfilling, gzip/brotli, HTTP/3, caching, and more!*
  - https://www.skypack.dev/
- **jspm**
  - *All modules on npm are converted into ES modules*
  - *Packages are served heavily optimized*
  - https://jspm.org/
- **esm.sh**
  - *global content delivery network to transform NPM packages to standard ES Modules*
  - optional: self-hosted
  - https://esm.sh/
