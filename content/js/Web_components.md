---
tags: [Notebooks/Javascript]
title: Web components
created: '2019-02-20T09:43:04.537Z'
modified: '2021-09-02T10:36:56.404Z'
parent: JavaScript
---

# Web components
- <https://github.com/obetomuniz/awesome-webcomponents>
- <https://github.com/nepaul/awesome-web-components>
- [The Flaws Of Web Components (And Possible Solutions)](https://www.thinktecture.com/de/web-components/flaws/)
- **open-wc**
  - <https://github.com/open-wc/open-wc>
  - <https://open-wc.org/>
- https://developers.google.com/web/fundamentals/web-components/
- https://developer.mozilla.org/de/docs/Web/Web_Components/Using_custom_elements
- **web-component-analyzer**
  - https://www.npmjs.com/package/web-component-analyzer
  - *CLI that makes it possible to easily analyze web components*
  - *supports web components built with the following libraries: lit-element, polymer, stencil (partial)*


## DOM-Spec und Proposals
- <https://dom.spec.whatwg.org/>
- **DocumentOrShadowRoot.adoptedStyleSheets**
  - Teilen von Styles zwischen Webcomponents
  ```js
    const body = document.querySelector('body');
    const shadow = body.attachShadow({ mode: 'open' });
    const p = document.createElement('p');
    p.textContent = 'hello world';
    shadow.appendChild(p);

    const sheet = new CSSStyleSheet();
    sheet.addRule('p', 'color: red; font-size: 2rem;');

    shadow.adoptedStyleSheets = [sheet];
  ```
  - https://wicg.github.io/construct-stylesheets/
  - https://developers.google.com/web/updates/2019/02/constructable-stylesheets
  - Status
    - 8.8.20: *collection of ideas, no standard, not even a draft.* (nur Chrome)
    - [caniuse DocumentOrShadowRoot.adoptedStyleSheets](https://caniuse.com/#search=adoptedstyle)
    - Polyfill: https://www.npmjs.com/package/construct-style-sheets-polyfill
- **scoped custom elements**
  - *This proposal allows for multiple custom element definitions for a single tag name to exist within a page.*
  - https://github.com/justinfagnani/scoped-custom-elements (von einem Google-er)
- **HTML imports**
  - https://github.com/w3c/webcomponents/issues/645
  - Status: https://www.chromestatus.com/feature/4854408103854080
- **CSS imports**
  - `import sheet from './styles.css' assert { type: 'css' }`
    `document.adoptedStyleSheets = [sheet]`


## Frameworks
- <https://custom-elements-everywhere.com/> (Bewertung versch. WC-Libs)
- **lit**
  - https://github.com/lit/lit
  - [property updates playground](https://lit.dev/playground/#project=W3sibmFtZSI6InNpbXBsZS1ncmVldGluZy50cyIsImNvbnRlbnQiOiJpbXBvcnQge2h0bWwsIGNzcywgTGl0RWxlbWVudCwgUHJvcGVydHlWYWx1ZXN9IGZyb20gJ2xpdCc7XG5pbXBvcnQge2N1c3RvbUVsZW1lbnQsIHByb3BlcnR5LCBzdGF0ZX0gZnJvbSAnbGl0L2RlY29yYXRvcnMuanMnO1xuXG5cbmNsYXNzIEZvbyB7XG4gIGJhcjogc3RyaW5nID0gTWF0aC5yYW5kb20oKS50b1N0cmluZygpO1xufVxuXG5cbkBjdXN0b21FbGVtZW50KCdhLWEnKVxuZXhwb3J0IGNsYXNzIEEgZXh0ZW5kcyBMaXRFbGVtZW50IHtcblxuICBAc3RhdGUoKVxuICBmb28gPSBuZXcgRm9vKCk7XG5cbiAgcmVuZGVyKCkge1xuICAgIHJldHVybiBodG1sYFxuICAgICAgICA8YnV0dG9uIEBjbGljaz0ke3RoaXMuY2xpY2tlZEF9PmNsaWNrPC9idXR0b24-XG4gICAgICAgIDxzcGFuPiR7dGhpcy5mb28uYmFyfTwvc3Bhbj5cbiAgICAgICAgPGJyLz48YnIvPjxoci8-PGJyLz5cbiAgICAgICAgPGItYiAuZm9vPSR7dGhpcy5mb299IEBpbnB1dGNoYW5nZWQ9JHt0aGlzLmlucHV0Q2hhbmdlZH0-PC9iLWI-XG4gICAgYDtcbiAgfVxuICBcbiAgLy8gdXBkYXRlZCBhbGxlczpcbiAgY2xpY2tlZEEoZSkge1xuICAgIGNvbnNvbGUubG9nKGUpO1xuICAgIHRoaXMuZm9vID0gbmV3IEZvbygpOyAgIFxuICB9XG4gIFxuICAvLyBvaG5lIHJlcXVlc3RVcGRhdGUga2VpbmUgdXBkYXRlczpcbiAgY2xpY2tlZEIoZSkge1xuICAgIHRoaXMuZm9vLmJhciA9IE1hdGgucmFuZG9tKCkudG9TdHJpbmcoKTtcbiAgICAvLyB1cGRhdGV0IGltbWVyaGluIGVpZ2VuZXMgc3BhbjpcbiAgICB0aGlzLnJlcXVlc3RVcGRhdGUoKTtcbiAgfVxuICBcbiAgLy8gdXBkYXRldCBhbGxlc1xuICBpbnB1dENoYW5nZWQoZSkge1xuICAgIHRoaXMuZm9vID0gT2JqZWN0LmFzc2lnbih7fSwgdGhpcy5mb28sIGUuZGV0YWlsKTtcbiAgfVxuIFxufVxuXG5cbkBjdXN0b21FbGVtZW50KCdiLWInKVxuY2xhc3MgQiBleHRlbmRzIExpdEVsZW1lbnQge1xuICBcbiAgICBAcHJvcGVydHkoKVxuICAgIGZvbzogRm9vO1xuICBcbiAgICAgcmVuZGVyKCkge1xuICAgIHJldHVybiBodG1sYFxuICAgICAgICA8aW5wdXQgLnZhbHVlPSR7dGhpcy5mb28uYmFyfSBAY2hhbmdlPSR7dGhpcy5jaGFuZ2VkQ30gLz5cbiAgICAgICAgPHNwYW4-JHt0aGlzLmZvby5iYXJ9PC9zcGFuPlxuICAgICAgIGA7XG4gIH1cbiAgXG4gICAgLy8gRWluZ2FiZW4gdXBkYXRlbiBuaWNoczpcbiAgY2hhbmdlZEEoZSkge1xuICAgIHRoaXMuZm9vLmJhciA9IGUudGFyZ2V0LnZhbHVlO1xuICB9XG4gIFxuICAvLyBFaW5nYWJlbiB1cGRhdGVuIG51ciBlaWdlbmVzIHNwYW46XG4gIGNoYW5nZWRCKGUpIHtcbiAgICB0aGlzLmZvbyA9IHtcbiAgICAgIC4uLnRoaXMuZm9vLFxuICAgICAgYmFyOiBlLnRhcmdldC52YWx1ZVxuICAgIH1cbiAgfVxuICBcbiAgLy8gXCJwcm9wZXJ0aWVzIGRvd24sIGV2ZW50cyB1cFwiXG4gIGNoYW5nZWRDKGUpIHtcbiAgICBjb25zdCBkZXRhaWwgPSB7IGJhcjogZS50YXJnZXQudmFsdWUgfTtcbiAgICB0aGlzLmRpc3BhdGNoRXZlbnQobmV3IEN1c3RvbUV2ZW50KCdpbnB1dGNoYW5nZWQnLCB7IGRldGFpbCB9KSk7XG4gIH1cbiAgXG59XG5cblxuIn0seyJuYW1lIjoiaW5kZXguaHRtbCIsImNvbnRlbnQiOiI8IURPQ1RZUEUgaHRtbD5cbjxoZWFkPlxuICA8c2NyaXB0IHR5cGU9XCJtb2R1bGVcIiBzcmM9XCIuL3NpbXBsZS1ncmVldGluZy5qc1wiPjwvc2NyaXB0PlxuPC9oZWFkPlxuPGJvZHk-XG4gIDxhLWE-PC9hLWE-XG48L2JvZHk-XG4ifV0)
- **stencil**
  - https://stenciljs.com/
  - https://github.com/mappmechanic/awesome-stenciljs
- **skatejs**
  - https://github.com/skatejs/skatejs
  - *Skate is a functional reactive abstraction over the web component standards as a set of packages that enables you to write small, fast and scalable web components using popular view libraries such as React, Preact and LitHTML.*
- **relift**
  - https://relift-html.js.org/
- **Angular elements**
- **Polymer** → JavaScript/Polymer
- **Haunted**
  - https://github.com/matthewp/haunted
  - *React's Hooks API but for standard web components and lit-html or hyperHTML.*


## UI/Component Libs
- **vaadin**
  - https://vaadin.com/components
- **material-components**
  - https://github.com/material-components/material-components-web-components
- **elix**
  - https://component.kitchen/elix
  - https://github.com/elix/elix
- **ui5**
  - https://sap.github.io/ui5-webcomponents/
- **patternfly**
  - https://patternfly.github.io/patternfly-elements/demo
- **lightning**
  - https://developer.salesforce.com/docs/component-library/overview/components
- **shoelace**
  - https://shoelace.style/
