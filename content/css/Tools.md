---
tags: [Notebooks/CSS]
title: Tools
created: '2019-02-05T09:32:49.813Z'
modified: '2021-05-18T08:14:04.478Z'
parent: CSS
---

# Tools

## Build

### Preprocessors
- **SASS**
  - https://sass-lang.com/
  - cheat sheet: https://devhints.io/sass
- **LESS**
- **Stylus**
- **linaria**
  - https://github.com/callstack/linaria
  - *Zero-runtime CSS in JS library*
- **postcss**
  - https://postcss.org/
  - https://github.com/postcss/postcss
  - *lint your CSS, support variables and mixins, transpile future CSS syntax, inline images, and more.*
  - presets/polyfills: https://github.com/csstools/postcss-preset-env
  - autoprefixer (vendor prefixes): https://github.com/postcss/autoprefixer
  - https://www.npmjs.com/package/postcss-cssnext
- **Autoprefixer online**
  - https://autoprefixer.github.io/


### Responsive
- **rfs**
  - Responsive Font Size
  - https://github.com/twbs/rfs
  - *Automate your responsive workflow*
  - https://css-tricks.com/using-a-postcss-function-to-automate-your-responsive-workflow/


### Ungenutzte Style-Regeln entfernen
- **UnCSS**
  - https://github.com/uncss/uncss ⭐8000
  - *UnCSS is a tool that removes unused CSS from your stylesheets. It works across multiple files and supports Javascript-injected CSS.*
postcss✔️
- **PurgeCSS**
  - https://github.com/FullHuman/purgecss ⭐3000
  - https://www.purgecss.com/
  - *Purgecss was originally thought as the v2 of purifycss*
  - Webpack✔️ postcss✔️rollup✔️ js-api✔️ cli✔️
  - vs purify
    *PurifyCSS can work with any file type, not just HTML or JavaScript. PurifyCSS works by looking at all of the words in your files and comparing them with the selectors in your CSS. Every word is considered a selector, which means that a lot of selectors can be erroneously consider used. For example, you may happen to have a word in a paragraph that matches a selector in your CSS.
    PurgeCSS fixes this problem by providing the possibility to create an extractor. An extractor is a function that takes the content of a file and extracts the list of CSS selectors used in it. It allows a perfect removal of unused CSS.*
- **PurifyCSS**
  - https://github.com/purifycss/purifycss ⭐9000
  - Webpack✔️
  - https://purifycss.online/
- **DropCSS**
  - https://github.com/leeoniya/dropcss ⭐1900
  - nach eigenen Angaben kleiner und schneller als die anderen Tools


### Structural optimizers
- **clean-css**
- **csso**
- **cssnano**
  - https://github.com/cssnano/cssnano ⭐3.7k
  - *A modular minifier, built on top of the PostCSS ecosystem.*
- **crass**


### Lazy/critical CSS
- https://web.dev/extract-critical-css
- https://github.com/filamentgroup/loadCSS ("Polyfill" für link rel=preload)
- lazy load css:
```js
const loadCss = url => {
  const link = document.createElement('link');
  link.rel = 'stylesheet';
  link.href = url;
  link.type = 'text/css';
  document.head.appendChild(link);
}
```
- **critical**
  - https://github.com/addyosmani/critical ⭐9.100
  - *Critical extracts & inlines critical-path (above-the-fold) CSS from HTML*
- **penthouse**
  - https://github.com/pocketjoso/penthouse ⭐2.400


## Linter
- **stylelint**
  - https://github.com/stylelint/stylelint
- **doiuse**
  - *Lint CSS for browser support against Caniuse database*
  - https://github.com/anandthakker/doiuse
- **revenge.css**
  - http://heydonworks.com/revenge_css_bookmarklet/
  - *bookmarklet that reports bad html using pseudo content. If the page you use it with has malformed links, deprecated attributes, divs inside inline elements, inaccessible buttons, badly nested sections or other errors, you'll see some ugly, pink errors*
- **csscomb.js**
  - *coding style formatter*
  - https://github.com/csscomb/csscomb.js


## Debugging
- **Debucsser**
  - https://github.com/lucagez/Debucsser
  - Bei hover über ein Element wird dessen Box, Klassen, id und Dimensionen angezeigt.
  - Als Skript einbindbare JS-Lib, Browser Addon in Entwicklung [13.12.18]
- **pesticide**
  - http://pesticide.io/
  - *A chrome plugin for quickly debugging css layout issues by toggling different colored outlines on every element.*
  - CTRL -\> Elementinfo
- **mozilla grid inspector**
  - https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Examine_grid_layouts

