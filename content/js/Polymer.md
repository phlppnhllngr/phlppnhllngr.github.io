---
tags: [Notebooks/Javascript]
title: Polymer
created: '2020-08-06T09:49:20.589Z'
modified: '2020-11-02T11:06:31.879Z'
parent: JavaScript
---

# Polymer
- https://github.com/polymer/polymer
- https://polymer-library.polymer-project.org/3.0/docs/about_30
- https://github.com/StartPolymer/awesome-polymer *40
- https://github.com/Granze/awesome-polymer *380

## Libs
  - UI
    - https://www.predix-ui.com/#/elements/
    - https://www.webcomponents.org/collection/Polymer/elements
  - State management
    - https://github.com/tur-nr/polymer-redux *450 (@next für Polymer 3!)
    - https://github.com/google/uniflow-polymer *170 (Polymer 2!)


## Settings
- https://polymer-library.polymer-project.org/3.0/docs/devguide/settings#settings-summary
- `window.polymerSkipLoadingFontRoboto = true;`


## Styling
- https://polymer-library.polymer-project.org/3.0/docs/devguide/style-shadow-dom
- Styles zwischen Components teilen (shared styles)
  - https://polymer-library.polymer-project.org/3.0/docs/devguide/style-shadow-dom#share-styles-between-elements
  - → constructed style sheets


## CLI

### build
- Dependency: polymer-build
- lazy loading, code splitting, dynamic imports
  - https://polymer-library.polymer-project.org/3.0/docs/apps/build-for-production#dynamic
  - *You don't need to list dynamic imports as fragments. The latest Polymer build tools analyze your code and find your dynamic imports, provided they are expressed with static strings.*
  - Listung als fragment nötig, wenn kein String sondern Variable innerhalb `import` (sonst wird das File komplett ignoriert)
    ```js
    const lazy = './path/to/lazy.js'
    await import(lazy)
    // polymer.json
    { "fragments": ["src/path/to/lazy.js"] }
    ```
    führt zu (Linter-) `warning [non-literal-import] - Cannot analyze dynamic imports with non-literal arguments`
    =>
    ```json
    "lint": {
      "ignoreWarnings": [
        "non-literal-import"
      ]
    }
    ```
  - wenn innerhalb 2er lazy geladener Views die gleiche Dependency jeweils statisch importiert wird, dann wird diese Dependency beim Build dem Main-Bundle (my-app.js) hinzugefügt (nicht immer?), es sei denn man gibt diese Dependency explizit in polymer.json->fragments an; dann wird ein separater Chunk daraus
- mit `js->compile=false` in polymer.json werden Template-Strings überhaupt nicht mehr minified (weder Whitespace noch Comments), mit `compile=es5` zumindest einigermaßen (whitespace bleibt erhalten)
- `"css": { minify: true }` minified CSS in (index).html und dort referenzierten `<link href>` (unter "sources" listen nicht vergessen!), aber nicht in js-Files

### serve
- Dependency: polyserve (https://github.com/Polymer/tools/tree/master/packages/polyserve)


## build
- https://polymer-library.polymer-project.org/3.0/docs/apps/build-for-production
- polymer-cli
- polymer-build
  - https://polymer-library.polymer-project.org/3.0/docs/apps/build-for-production#buildwithlibrary
  - *Consider using polymer-build instead of Polymer CLI if you want to customize your build(s) without using the Polymer CLI*
  - https://github.com/Polymer/tools/tree/master/packages/build
  - der `HtmlSplitter` hat seinen Namen wohl aus Polymer2-Zeiten, funktioniert laut Doku aber auch mit JS (Polymer 3) und kann JS-Files in js und css spalten
- webpack
  - polymer3-webpack-starter (inoffiziell)
      - https://github.com/web-padawan/polymer3-webpack-starter/tree/master/
      - [codesandbox.io-Link](https://codesandbox.io/s/polymer3-webpack-starter-0utkq)
- polymer-starter-kit
  - https://github.com/Polymer/polymer-starter-kit
  - letzter Commit Dez. 2018, installiert nicht mehr die neuesten Version(en)!
- pwa-starter-kit
  - https://github.com/Polymer/pwa-starter-kit (archived)


## Codeschnipsel

**iron-pages: auf Seitenwechsel reagieren**
```html
<iron-pages attr-for-selected="page" selected-attribute="selected" selected="a">
  <page-a page="a"></page-a>
  <page-b page="b"></page-b>
<iron-pages>
```
```js
// page-a.js
properties: {
  selected: {
    type: Boolean,
    value: false,
    reflectToAttribute: true,
    observer: 'observeSelected'
  }
}

observeSelected(newVal, oldVal) {
  const pageWasLeft = oldVal === true && newVal === false;
}
```

**iron-pages: restamping**
<br/>[https://github.com/PolymerElements/iron-pages/issues/53#issuecomment-403629036](https://github.com/PolymerElements/iron-pages/issues/53#issuecomment-403629036)

**imports**
<br/>Server-Kontext = /

wenn in File src/importmeta/importmeta.js:
```html
<img src="./images/image.jpg"/>
<-- Request geht nach: /images/image.jpg (src relativ zum Server-Kontextpfad (root)) -->
```

mit `importMeta()` und `[[importPath]]`:
```js
static get importMeta() {
  return import.meta;
}
```
```html
<img src="[[importPath]]images/image.jpg"/>
<-- Request geht nach: /src/importmeta/images/image.jpg (src relativ zum Verzeichnispfad) -->
```

**@apply**
```css
:host {
  --my-mixin: {
    color: red;
    white-space: nowrap;
  }
}
selector {
  @apply --my-mixin;
}
```
wird zu:
```css
:host {
  --my-mixin_-_color: red;
  --my-mixin_-_white-space: nowrap;
}
selector {
  color: var(--my-mixin_-_color);
  white-space: var(--my-mixin_-_white-space);
}
```

