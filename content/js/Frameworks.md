---
title: Frameworks
parent: JavaScript
---

# Frameworks
- Vergleich: https://medium.com/dailyjs/a-realworld-comparison-of-front-end-frameworks-2020-4e50655fe4c1>
- **Svelte**
  - <https://svelte.dev/>
  - <https://github.com/sveltejs/svelte> <img loading="lazy" src="https://img.shields.io/github/stars/sveltejs/svelte?style=flat-square"/>
  - auch custom elements möglich
  - <https://objectcomputing.com/resources/publications/sett/july-2019-web-dev-simplified-with-svelte> (eslint- & prettier-integration, testing, ...)
  - <https://www.freecodecamp.org/news/the-svelte-handbook/>
  - <https://madewithsvelte.com/>
  - <https://github.com/CalvinWalzel/awesome-svelte>
  - <https://svelte-community.netlify.com/>
  - test
    - <https://github.com/rspieker/jest-transform-svelte>
    - <https://github.com/ktsn/svelte-jest>
    - <https://github.com/mihar-22/svelte-jester>
    - <https://github.com/bahmutov/cypress-svelte-unit-test>
    - <https://github.com/testing-library/svelte-testing-library>
  - libs
    - <https://github.com/c0bra/svelma>
    - <https://github.com/ItalyPaleAle/svelte-spa-router>
  - tools
    - sapper
      - <https://github.com/sveltejs/sapper>
      - <https://sapper.svelte.dev/>
      - router, preload, ssr
    - kit (7.8.21: beta)
      - nachfolger von sapper
      - <https://github.com/sveltejs/kit>
    - <https://github.com/sveltejs/eslint-plugin-svelte3>
    - <https://github.com/kaisermann/svelte-preprocess>
    - elderjs
      - static site generator
      - <https://github.com/elderjs/elderjs>
    - snowpack
    - <https://github.com/GeopJr/SveltePress>
- **Ionic**
  - <https://ionicframework.com/>
- **hyperapp**
  - <https://github.com/jorgebucaran/hyperapp> <img loading="lazy" src="https://img.shields.io/github/stars/jorgebucaran/hyperapp?style=flat-square"/>
- **apprun**
  - <https://github.com/yysun/apprun> <img loading="lazy" src="https://img.shields.io/github/stars/yysun/apprun?style=flat-square"/>
- **preact**
  - <https://preactjs.com/>
  - <https://github.com/preactjs/preact> <img loading="lazy" src="https://img.shields.io/github/stars/preactjs/preact?style=flat-square"/>
  - *3kB React alternative with the same modern API*
  - preact vs react
    - <https://preactjs.com/guide/v10/differences-to-react/>
    - *we don't ship our own Synthetic Event system [...] follow a bit more closely the DOM specification*
- **domponent**
  - <https://github.com/tamb/domponent> *50
- **stimulus**
  - <https://github.com/stimulusjs/stimulus> *7.8k
- **project-x**
  - <https://github.com/calebporzio/project-x> *500
- **alpine**
  - <https://github.com/alpinejs/alpine> <img loading="lazy" src="https://img.shields.io/github/stars/alpinejs/alpine?style=flat-square"/>
  - *A rugged, minimal framework for composing JavaScript behavior in your markup.*
- **mint**
  - <https://www.mint-lang.com/>
  - *programming language for writing single page applications*
  - compiled zu react
- **fluorjs**
  - <https://fluorjs.github.io/>
- **moon**
  - <https://github.com/kbrsh/moon> <img loading="lazy" src="https://img.shields.io/github/stars/kbrsh/moon?style=flat-square"/>
  - inaktiv seit 03/2020
- **solid**
  - <https://github.com/ryansolid/solid>
  - nach eigenen Angaben das performanteste JS-Framework (12/2020; https://javascript.plainenglish.io/javascript-frameworks-performance-comparison-2020-cd881ac21fce)
- **turbolinks**
  - <https://github.com/turbolinks/turbolinks> <img loading="lazy" src="https://img.shields.io/github/stars/turbolinks/turbolinks?style=flat-square"/>
  - *Get the performance benefits of a single-page application without the added complexity of a client-side JavaScript framework.*
  - *Use HTML to render your views on the server side and link to pages as usual. When you follow a link, Turbolinks automatically fetches the page, swaps in its `<body>`, and merges its `<head>`, all without incurring the cost of a full page load.*
- **htmx**
  - <https://htmx.org/>
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
  - <https://github.com/single-spa/single-spa>
- **mitosis**
  - *Write components once, run everywhere. Compiles to Vue, React, Solid, Angular, Svelte, and more.*
  - <https://github.com/BuilderIO/mitosis>
- **qwik**
  - *designed for best possible time to interactive, by focusing on resumability of server-side-rendering of HTML, and fine-grained lazy-loading of code.*
  - <https://github.com/BuilderIO/qwik>
- **marko**
  - <https://github.com/marko-js/marko> <img loading="lazy" src="https://img.shields.io/github/stars/marko-js/marko?style=flat-square"/>
- **astro** -> Webdev/Static sites
- **wasp**
  - *Wasp (Web Application Specification Language) is a declarative DSL (domain-specific language) for developing, building and deploying modern full-stack web apps with less code.*
  - *Concepts such as app, page, user, login, frontend, production, etc. are baked into the language, bringing a new level of expressiveness and allowing you to get more work done with fewer lines of code.*
  - *While describing high-level features with Wasp, you still write the rest of your logic in your favorite technologies (currently React, NodeJS, Prisma).*
  - <https://github.com/wasp-lang/wasp> <img loading="lazy" src="https://img.shields.io/github/stars/wasp-lang/wasp?style=flat-square"/> 
