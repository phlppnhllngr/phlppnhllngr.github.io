---
tags: [Notebooks/Webdev]
title: Performance
created: '2019-02-20T15:30:05.335Z'
modified: '2021-09-05T12:16:01.899Z'
parent: Webdev
---

# Performance
- gzip (noch besser: brotli)
- cdn
- http2 pipelining
- browser apis: navigator.connection
- webworker


## Tipps
- <https://github.com/thedaviddias/Front-End-Performance-Checklist>
- <https://tj.ie/improving-client-side-performance/>
- [Web performance made easy (Google I/O '18) - youtube](https://www.youtube.com/watch?v=Mv-l3-tJgGk)
- <https://3perf.com/talks/web-perf-101/>
- <https://web.dev/>
- <https://addyosmani.com/blog/performance-budgets/>
- <https://medium.com/@Charles_Stover/boost-your-page-speed-reduce-parse-time-d2a380907de5>
- <https://3perf.com/blog/link-rels/>
- <https://andydavies.me/blog/2019/02/12/preloading-fonts-and-the-puzzle-of-priorities/>
- <https://developers.google.com/web/fundamentals/performance/resource-prioritization>
- <https://calendar.perfplanet.com/2019/>
- <https://itnext.io/high-performance-web-apps-2a469cfd3550>


## case studies
- <https://www.reddit.com/r/webdev/comments/b2xjdm/who_has_the_fastest_f1_website_a_deepdive_into/> (19.3.19)
- <http://iamakulov.com/notes/walmart/> (27.4.18)
- <https://techblog.wikimedia.org/2020/11/23/web-performance-case-study-wikipedia-page-previews/>
- <https://www.reddit.com/r/programming/comments/kiq0ih/we_rendered_a_million_web_pages_to_find_out_what/>


## Messung
- <u>globalThis</u>
  - **console**
    - `time(), timeLog(), timeEnd()`
    - `memory`
    - `profile(), profileEnd()`
  - **performance**
    - <https://developer.mozilla.org/en-US/docs/Web/API/Window/performance>
    - navigation timing api
      - <https://developer.mozilla.org/en-US/docs/Web/API/Navigation_timing_API>
    - user timing api
      - <https://developer.mozilla.org/en-US/docs/Web/API/User_Timing_API>
      - `mark()`
      - `measure()`
    - resource timing api
      - <https://developer.mozilla.org/en-US/docs/Web/API/Resource_Timing_API>
    - `eventCounts`
    - `memory`
    - `measureUserAgentSpecificMemory()`
- <u>Chrome</u>
  - <https://developers.google.com/web/tools/chrome-devtools/evaluate-performance>
  - F12 > Lighthouse tab -> Google/Lighthouse
  - F12 > Memory tab
    - memory usage, heap snapshots
  - F12 > Performance tab
  - F12 > Triple dots > More tools
    - JavaScript Profiler
    - Performance monitor
- <https://www.reddit.com/r/webdev/comments/8fn4zn/website_auditing_tools/>
- <u>Google</u>
  - **test my site**
    - <https://www.thinkwithgoogle.com/feature/testmysite/>
    - *compare your mobile site speed*
    - Chrome Profiling
  - **URL Inspection tool**
    - <https://support.google.com/webmasters/answer/9012289>
  - **Lighthouse**
    - <https://developers.google.com/web/tools/lighthouse/>
    - <https://github.com/GoogleChrome/lighthouse>
    - ~~chrome extension~~ jetzt in Chrome eingebaut & CLI (nodejs 10+)
    - Lighthouse CI
      - <https://github.com/GoogleChrome/lighthouse-ci>
        - Instruktionen u.A. für Jenkins
      - *a set of commands that make continuously running, asserting, saving, and retrieving Lighthouse results as easy as possible.*
      - <https://github.com/Pixboost/lighthouse-ci-docker> (unofficial)
  - **PageSpeed**
    - <https://developers.google.com/speed/>
- **siteaudit**
  - <https://github.com/thecreazy/siteaudit>
  - CLI für pagespeed, lighthouse & a11y
- **speedcurve** 💰
  - <https://speedcurve.com/>
- **sitespeed.io**
  - <https://www.sitespeed.io/>
  - <https://github.com/sitespeedio/sitespeed.io> *3600
  - *the complete <mark>toolbox</mark> to test the web performance of your web site*
  - speed, a11y, lighthouse, mobile phones, WebPageTest, ...
  - docker, node_module
- **WebPageTest**
  - <https://www.webpagetest.org/>
  - load time metrics, best practice check
  - <https://nooshu.github.io/blog/2019/10/02/how-to-read-a-wpt-waterfall-chart/>
  - Browser-Tool, mit REST-API (konfigurierbarer Nrowser, internet speed, lighthouse integration, ...)
- **performancebudget**
  - <https://www.performancebudget.io/>
  - man gibt an in wievielen Sekunden eine Website mit Netzwergeschwindigkeit x geladen werden soll, und erhält dafür ein Maximum an Dateigrößen für HTML, JS, CSS, ...
- **size-limit**
  - <https://github.com/ai/size-limit>
  - *performance budget tool for JavaScript*
- **webhint.io**
  - <https://webhint.io/>
  - performance, a11y, cross browser compat, http headers
- YSlow, LGTmetrics, LogRocket, DareBoost


## Preloading

### predictive prefetching
- consider navigator.connection(.saveData) 

### link rel-Attr
- <https://3perf.com/blog/link-rels/>
- <https://www.ctrl.blog/entry/dns-prefetch-preconnect.html> (mit Browser-Support-Tabelle)

<details>
  <summary>preload</summary>
  <ul>
    <li>focuses on fetching a resource for the current navigation</li>
    <li>tells the browser to download and cache a resource (like a script or a stylesheet) as soon as possible.</li>
    <li>It’s     
    helpful when you need that resource a few seconds after loading the page, and you want to speed it up.
    </li>
    <li>The browser doesn’t do anything with the resource after downloading it. Scripts aren’t executed, stylesheets aren’t applied. It’s <mark>just cached</mark> – so that when something else needs it, it’s available immediately.</li>
    <li>Browser bestimmt die Prio anhand des `as`-Attributs => will not delay more important resources, nor tag along behind less important resources
    </li>
    <li>`as` beeinflusst außerdem: CSP, accept-Header, caching</li>
    <li>neuer als `prefetch` und feuert im Gegensatz dazu ein `onload`-Event</li>
    <li><a href="https://web.dev/preload-critical-assets/">https://web.dev/preload-critical-assets - 5.11.18</a></li>
  </ul>
</details>
<details>
  <summary>prefetch</summary>
  <ul>
    <li>asks the browser to download and cache a resource (like, a script or a stylesheet) in the background.</li>
    <li>The download happens with a <mark>(very) low priority</mark>, so it doesn’t interfere with more important resources.</li>
    <li>It’s helpful when you know you’ll need that resource on a subsequent page, and you want to cache it ahead of time.</li>
    <li>works only with link-tags</li>
    <li>values for "as"-Attr: document, script, image, font, fetch, style <a href="https://www.w3.org/TR/preload/#as-attribute">and more</a></li>
  </ul>
</details>
<details>
  <summary>preconnect</summary>
  <ul>
    <li>asks the browser to perform a connection to a domain in advance. It’s helpful when you know you’ll download  
    something from that domain soon, but you don’t know what exactly, and you want to speed up the initial connection</li>
    <li>A browser has to set up a connection when it retrieves something from a new third-party domain. This may happen when a site uses a font from Google Fonts, loads React from a CDN, or requests a JSON response from an API server.</li>
    <li>Use it to slightly speed up some third-party script or style.</li>
    <li>You don’t need to use DNS prefetch when you’re using preconnect. The domain name will be resolved as the first step of the browser establishing the connection.</li>
    <li>The requirements for which domains to preconnect to are slightly different than for dns-prefetch: The domain is a chained dependency not already loaded by the webpage itself. The domain is expected to be required within ten seconds of the document being loaded.</li>
  </ul>
</details>
<details>
  <summary>dns-prefetch</summary>
  <ul>
    <li>asks the browser to perform a DNS resolution of a domain in advance. It’s helpful when you know you’ll connect to  
    that domain soon, and you want to speed up the initial connection</li>
    <li>Using both of these tags for the same domain is not really useful – preconnect already includes everything 
    dns-prefetch does, and more. However, it can still make sense in two cases:</li>
    <li>Browsers go through documents as they’re loaded and start to resolve domain names and establish connections to all the domains that their document preload scanners find. This includes URLs in iframe img, link, script, and other such elements. DNS-prefetching is, however, useful for domain names that the browser’s pre-processor can’t possibly know about at the time it starts to render the document. Any external resources that are required by a frame, script, or stylesheet are prime candidates. For example, an ad network may be embedded in your webpage as "script src='https://example.com/'". You don’t need to prefetch this domain name. However, that script then tries to fetch a resource from `https://example.org/`. That’s the domain name that will benefit from being DNS-prefetching.</li>
    <li>You should only DNS-prefetch domains that meet the following requirements: The domain is a chained dependency not already loaded by the webpage itself. The domain is expected to be required within one minute of the document being loaded.</li>
  </ul>
</details>
<details>
  <summary>prerender</summary>
  <ul>
    <li>asks the browser to load a URL and render it in an invisible tab. When a user clicks on a link to that URL, the   
    page should be rendered immediately. It’s helpful when you’re really sure a user will visit a specific page next, and you want to render it faster. Despite (or because of?) its power, in 2019, prerender has bad support in major browsers
    </li>
  </ul>
</details>

**Summing up**
Use:
- preload – when you’ll need a resource shortly / in a few seconds
- prefetch – when you’ll need a resource later / on a next page
- preconnect – when you know you’ll need a resource soon, but you don’t know its full url yet
- dns-prefetch – also when you know you’ll need a resource soon, but you don’t know its full url yet (for older browsers)
- prerender – when you’re certain users will navigate to a specific page, and you want to speed it up


### Libs
- <https://blog.logrocket.com/faster-page-load-times-with-link-prefetching/>
- **instant.page**
  - *Before a user clicks on a link, they hover their mouse over that link. When a user has hovered for 65 ms there is one chance out of two that they will click on that link, so instant.page starts preloading at this moment, leaving on average over 300 ms for the page to preload.*
  - <https://github.com/instantpage/instant.page> ⭐4.2k
  - <https://instant.page/>
  - funktioniert nicht mit dynamisch erzeugten Links
- **quicklink**
  - <https://github.com/GoogleChromeLabs/quicklink> ⭐8k
  - Benutzt IntersectionObserver, um Inhalte von Links innerhalb des Viewports vorzeitig zu laden. Einschränkbar, z.B.  mit requestIdleCallback oder abhängig von Verbindungsgeschwindigkeit.

### CSS
- -> CSS/Tools/lazy/critical css
- -> Webdev/DOM
- Referencing CSS stylesheets with link[rel=stylesheet] or @import causes browsers to delay page rendering while a stylesheet loads.
- *your page will only render as quickly as your slowest stylesheet*
- *we have to make assumptions about what above the fold even is, it’s hard to capture edge cases*
- Möglichkeit: Stylesheets per media
  ```css
  <link rel="stylesheet" href="all.css" media="all" />
  <link rel="stylesheet" href="small.css" media="(min-width: 20em)" />
  <link rel="stylesheet" href="medium.css" media="(min-width: 64em)" />
  <link rel="stylesheet" href="large.css" media="(min-width: 90em)" />
  <link rel="stylesheet" href="extra-large.css" media="(min-width: 120em)" />
  <link rel="stylesheet" href="print.css" media="print" />
  ```
  hier werden immer noch alle Stylesheets geladen, aber die mit nicht zutreffenden `media` mit Prio niedrig
  *The browser will still download all of the CSS files, but it will only block rendering on files needed to fulfil the current context.*
- **async css loading**
  - `<link rel="preload" as="style" href="async_style.css" onload="this.rel='stylesheet'">`
  - Wrapper-Lib: <https://github.com/filamentgroup/loadCSS/>
- `content-visibility` -> CSS/Properties
- <https://blog.bitsrc.io/improve-page-rendering-speed-using-only-css-a61667a16b2>
 


## Caching
- <https://www.mnot.net/cache_docs/>


## Debouncing, Throttling
- .


## Scalability
- <https://github.com/binhnguyennus/awesome-scalability>


## Server side rendering (SSR)
- <https://github.com/GoogleChrome/rendertron>
- <https://github.com/prerender/prerender>
