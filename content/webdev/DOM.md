---
title: DOM
parent: Webdev
---

# DOM

## Lifecycle & Resource Loading

### Lifecycle
- <https://javascript.info/onload-ondomcontentloaded>
  - document.readyState
    - loading
    - interactive
    - complete
    - readystatechange-Event
- DOMContentLoaded
  - *the browser fully loaded HTML, and the DOM tree is built, but external resources like pictures `<img>` and stylesheets may not yet have loaded.*
  - *DOM is ready, so the handler can lookup DOM nodes, initialize the interface.*
  - *blocked by `<script>`s (if not async or dynamic)*
  - *browsers autofill forms on DOMContentLoaded.*
- load
  - *not only HTML is loaded, but also all the external resources: images, styles etc.*
  - *external resources are loaded, so styles are applied, image sizes are known etc.*
  - *window.onload, window.addEventListener('load')*
  - *blocked by `<script>`s (even async)*
- The typical output:
  [1] initial readyState: loading
  [2] readyState: interactive
  [2] DOMContentLoaded
  [3] iframe onload
  [4] img onload
  [4] readyState: complete
  [4] window onload
- beforeunload
- unload

### Resource Loading
- <https://whistlr.info/2020/understanding-load/>
- critical and non-critical resources can by inspected in chrome (more tools > coverage)
- scripts
  - scripts (inline or external (src)) are blocking
  - The script is fetched and executed immediately, before the browser continues parsing the page
  - dom building stops; they can not access dom defined below them
  - best practice is to put scripts right before closing `</body>` tag, so that the dom is fully rendered as fast as possible
    - downside: script execution delayed
  - async / defer
    - There are several ways an external script can be executed:
      - defer
        - script downloaded in background, executed when dom ready (html parsed)
        - Scripts with defer always execute when the DOM is ready, but before DOMContentLoaded event.
        - Deferred scripts keep their relative order
        - only works with external scripts (`src`)
        - dom access in defer scripts is safe
        - defer is ignored when async specified (but used as fallback if browser does not support async)
      - async
        - Loaded in background, executed when loaded (execution is then blocking the html parsing!)
        - DOMContentLoaded does not wait for async scripts
        - async scripts dont wait for other scripts
        - async scripts can run in any order ("load first, run first")
        - dom access in async scripts is dangerous
        - dynamic `document.createElement('script')`-Scripts behave as “async” by default
    - <https://bitsofco.de/async-vs-defer/>
    - <https://javascript.info/script-async-defer>
  <img loading="lazy" src="https://i.stack.imgur.com/wfL82.png" width="700px"/>
- css
  - `<link rel="stylesheet">` and `<link rel="import">` are render-blocking (blocken auch nachfolgendes js)
  - critical, "above the fold" css should be included inline inside the head-tag of the document
  - non-critical css should be moved to the bottom, before the closing `</body>`-tag
  - non-critical css can also by loaded with js (-> Webdev/Performance)
  - media types/queries: link-attribute `media` can make the link non-blocking (default/implicit value = `all`)
- images
  - not render-blocking
- fonts
  - not render-blocking


## Events
- A click event propagates in 3 phases:
  - **Capture phase** — Starting from window, document and the root element, the event dives down through ancestors of the target element
  - **Target phase** — The event gets triggered on the element on which the user made a click
  - **Bubble phase** — Finally, the event bubbles up through ancestors of the target element until the root element, document, and window.
- <https://domevents.dev/>
- use event delegation where possible (attaching listeners to parent/container elements instead of to each individual (list-)item element)

### addEventListener
- <https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener>
- options
  - once
    - listener should be invoked at most once after being added. If true, the listener would be automatically removed when invoked
    - <https://caniuse.com/#search=once>
    <details>
      <summary>caniuse</summary>
      <picture>
        <source type="image/webp" srcset="https://caniuse.bitsofco.de/image/once-event-listener.webp" loading="lazy">
        <source type="image/png" srcset="https://caniuse.bitsofco.de/image/once-event-listener.png" loading="lazy">
        <img src="https://caniuse.bitsofco.de/image/once-event-listener.jpg" alt="Data on support for the once-event-listener feature across the major browsers from caniuse.com" width="600"/>
      </picture>
    </details>
- statt einer Funktion kann man als erstes Argument auch ein Objekt mit `handleEvent`-property (Funktion) übergeben


## window.location & window.history
- **location**
  - `https://www.foo.bar:8080/abc?baz=qux#xyz`
    - href: `https://www.foo.bar:8080/abc?baz=qux#xyz`
    - protocol: `https:`
    - hash: `#xyz`
    - origin: `https://www.foo.bar:8080`
    - pathname: `/abc`
    - search: `?baz=qux`
    - host: `www.foo.bar:8080`
    - hostname: `www.foo.bar`
    - port: `"8080"`
  - reload(bool)
  - replace()
    - does not create history entry
  - assign(url: string)
    - reloads
    - creates history entry
  - `location = ...`
  - `location.href = ...`
    - reloads the page
    - creates history entry
- history
  - pushState()
  - replaceState()

  
## IntersectionObserver
- <https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API>
- guter Browser-Support; kein IE11, Safari ab 12.1 (iOS-Safari 12.2)
- <https://caniuse.com/#search=intersectionobserver>
  ```js
  const options= {
    root: document.querySelector('#scrollArea'),
    rootMargin: '0px',
    threshold: 1.0 // 1.0 means that when 100% of the target is visible within
    // the element specified by the root option, the callback is invoked
  }

  // Whenever the target meets a threshold specified for the IntersectionObserver, the callback is invoked.
  // The callback receives a list of IntersectionObserverEntry objects and the observer:
  const callback = (entries, observer) => { 
    entries.forEach(entry => { // <https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserverEntry>
      // Each entry describes an intersection change for one observed
      // target element:
      //   entry.boundingClientRect
      //   entry.intersectionRatio
      //   entry.intersectionRect
      //   entry.isIntersecting
      //   entry.rootBounds
      //   entry.target
      //   entry.time
    });
    // if only 1 target is observed: entries[0]
  };
  // Be aware that your callback is executed on the main thread.
  // It should operate as quickly as possible; if anything time-consuming needs to be done, use Window.requestIdleCallback()

  const observer = new IntersectionObserver(callback, options);

  const target = document.querySelector('#elementInScrollArea');

  // Watch for intersection.
  observer.observe(target);

  // Stop watching.
  observer.unobserve(target);

  // destroy observer
  observer.disconnect();
  ```


## Diverses
- MutationObserver
  - <https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver>
- ResizeObserver
  - reports changes to the dimensions of an Element's content or border box
  - da es keine CSS-Selektoren für die Größe eines Elements gibt, kann man damit z.B. Attribute je nach eigener Größe setzen, die dann wieder verschiedene CSS-Regeln aktivieren
  - <https://developer.mozilla.org/en-US/docs/Web/API/Resize_Observer_API>
- Web worker
  - <https://github.com/GoogleChromeLabs/comlink>
- [Writing a Simple MVC App in Plain JavaScript](https://www.taniarascia.com/javascript-mvc-todo-app/)
- requestAnimationFrame
  - The callback function is passed one single argument, a DOMHighResTimeStamp
  - <https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame>
- requestIdleCallback
  - <https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback>
  - Stand 09/20 kein Support in Safari
  - [shim](https://gist.github.com/paullewis/55efe5d6f05434a96c36), [polyfill](https://www.npmjs.com/package/requestidlecallback-polyfill) 
  - <https://caniuse.com/#feat=requestidlecallback>
  - <details>
      <summary>caniuse</summary>
      <img src="https://caniuse.bitsofco.de/image/requestidlecallback.jpg" width="600" loading="lazy"/>
    </details>
