---
tags: [Notebooks/Javascript]
title: Frameworks
created: '2019-04-11T08:16:46.669Z'
modified: '2021-09-05T12:51:46.355Z'
parent: JavaScript
---

# Frameworks

## Vergleich
~~https://medium.freecodecamp.org/a-realworld-comparison-of-front-end-frameworks-with-benchmarks-2019-update-4be0d3c78075~~
https://medium.com/dailyjs/a-realworld-comparison-of-front-end-frameworks-2020-4e50655fe4c1

- **Svelte**
  - https://svelte.dev/
  - https://github.com/sveltejs/svelte *37.5k
  - auch custom elements möglich
  - https://objectcomputing.com/resources/publications/sett/july-2019-web-dev-simplified-with-svelte (eslint- & prettier-integration, testing, ...)
  - https://www.freecodecamp.org/news/the-svelte-handbook/
  - https://madewithsvelte.com/
  - https://github.com/CalvinWalzel/awesome-svelte
  - https://svelte-community.netlify.com/
  - test
    - https://github.com/rspieker/jest-transform-svelte
    - https://github.com/ktsn/svelte-jest
    - https://github.com/mihar-22/svelte-jester
    - https://github.com/bahmutov/cypress-svelte-unit-test
    - https://github.com/testing-library/svelte-testing-library
  - libs
    - https://github.com/c0bra/svelma
    - https://github.com/ItalyPaleAle/svelte-spa-router
  - tools
    - sapper
      - https://github.com/sveltejs/sapper
      - https://sapper.svelte.dev/
      - router, preload, ssr
    - kit (7.8.21: beta)
      - nachfolger von sapper
      - https://github.com/sveltejs/kit
    - https://github.com/sveltejs/eslint-plugin-svelte3
    - https://github.com/kaisermann/svelte-preprocess
    - elderjs
      - static site generator
      - https://github.com/elderjs/elderjs
    - snowpack
    - https://github.com/GeopJr/SveltePress
- **Ionic**
  - https://ionicframework.com/
- **hyperapp**
  - https://github.com/jorgebucaran/hyperapp *17k
- **apprun**
  - https://github.com/yysun/apprun *900
- **preact**
  - https://preactjs.com/
  - https://github.com/preactjs/preact *25k
  - *3kB React alternative with the same modern API*
  - preact vs react
    - https://preactjs.com/guide/v10/differences-to-react/
    - *we don't ship our own Synthetic Event system [...] follow a bit more closely the DOM specification*
- **domponent**
  - https://github.com/tamb/domponent *50
- **stimulus**
  - https://github.com/stimulusjs/stimulus *7.8k
- **project-x**
  - https://github.com/calebporzio/project-x *500
- **alpine**
  - https://github.com/alpinejs/alpine *2.3k
  - *A rugged, minimal framework for composing JavaScript behavior in your markup.*
- **mint**
  - https://www.mint-lang.com/
  - *programming language for writing single page applications*
  - compiled zu react
- **fluorjs**
  - https://fluorjs.github.io/
- **moon**
  - https://github.com/kbrsh/moon *5.1k
  - inaktiv seit 03/2020
- **solid**
  - https://github.com/ryansolid/solid
  - nach eigenen Angaben das performanteste JS-Framework (12/2020; https://javascript.plainenglish.io/javascript-frameworks-performance-comparison-2020-cd881ac21fce)
- **turbolinks**
  - https://github.com/turbolinks/turbolinks *11.8k
  - *Get the performance benefits of a single-page application without the added complexity of a client-side JavaScript framework.*
  - *Use HTML to render your views on the server side and link to pages as usual. When you follow a link, Turbolinks automatically fetches the page, swaps in its `<body>`, and merges its `<head>`, all without incurring the cost of a full page load.*
- **htmx**
  - https://htmx.org/
  - *allows you to access AJAX, WebSockets and Server Sent Events directly in HTML, using attributes*
  - *htmx is the successor to intercooler.js*
  - quickstart
    ```html
    <!-- Load from unpkg -->
    <script src="https://unpkg.com/htmx.org@0.3.0"></script>
    <!-- have a button POST a click via AJAX -->
    <button hx-post="/clicked" hx-swap="outerHTML">Click Me</button>
    ```
    *The hx-post and hx-swap attributes tell htmx: "When a user clicks on this button, issue an AJAX request to /clicked, and replace the entire button with the response"*
- **single-spa**
  - *allows you to: Use multiple frameworks on the same page*
  - *a JavaScript router for front-end microservices. With single-spa you can use multiple frameworks in a single-page application, allowing you to split code by functionality and have Angular, React, Vue.js, etc. apps all living in harmony. single-spa makes them work together and won't load them until they're needed.*
  - https://github.com/single-spa/single-spa
