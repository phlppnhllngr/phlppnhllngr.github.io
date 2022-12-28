---
layout: default
title: CSS
has_children: true
---

# CSS
- <https://books.goalkicker.com/CSSBook/>
- <https://medium.freecodecamp.org/the-css-handbook-a-handy-guide-to-css-for-developers-b56695917d11>
- <https://moderncss.dev/>
- <https://github.com/you-dont-need/You-Dont-Need-JavaScript> - *CSS is powerful, you can do a lot of things without JS.*
- <https://adam-marsden.co.uk/css-cheat-sheet>
- <https://github.com/AllThingsSmitty/css-protips>
- <https://css-tricks.com/>
- <https://www.reddit.com/r/css/comments/r9e3i2/sometimes_you_just_need_to_target_safari_in_your/.compact>
- <https://www.reddit.com/r/css/comments/rj7cuw/writing_better_css_a_compilation_of_modern/.compact>
- <https://github.com/adamschwartz/magic-of-css>

## Performance
- <https://www.html5rocks.com/en/tutorials/speed/high-performance-animations/>
- **CSS Triggers**
  - <https://csstriggers.com/>
  - zeigt, wie performant Änderungen bestimmter Properties sind. Änderungen an `transform` sind z.B. relativ günstig, `width` teuer.


## BEM - Block Element Modifier
- <http://getbem.com/>
- Konventionen für CSS (z.B. Klassennamen)
- Bsp.:
  ```
  .person
      .person__head
          .person__eye.person__eye--blue
      .person__torso
  ```
- Do-s & Dont-s: <https://seesparkbox.com/foundry/bem_by_example>
- <https://9elements.com/bem-cheat-sheet/>
- `.person__torso` ist performanter als z.B. `.person .torso`, weil Browser die Regeln von rechts nach links parsen und anwenden. Es wird also zunächst nach ALLEN Elementen mit Klasse "torso" gesucht, und dann nur die behalten, die Parents mit Klasse "person" haben.


## Coverage
 - Anteil an tatsächlich verwendetem CSS: Chrome Devtools (Dot menu > more tools > coverage > type: CSS) oder Puppeteer `page.coverage.startCSSCoverage(); page.coverage.stopCSSCoverage();`


## Pseudo-Selektoren
- **:first-line**
- **:first-letter**
- **::selection**
  - highlighted text
- **:empty**
  - *element has no text or children*
- **:only-child**
- **:valid, :invalid**
  - *for inputs*
- **:not()**
- **:active**
  - *represents the state when the element is currently being activated by the user*
- **:focus**
  - *represents the state when the element is currently selected to receive input*
  - :focus -> *element receives any kind of focus (click, tab)*
  - :focus-visible -> *focused by keyboard*
  - :focus:not(:focus-visible) -> focused by mouse or touch
- <u>focus vs active</u>
  *By default, active and focus are both off.
  When you tab to cycle through focusable elements, they will enter :focus (without active).
  When you click on a non-focusable element, it enters :active (without focus).
  When you click on a focusable element it enters :active:focus (active and focus simultaneously).*
- **:placeholder-shown**
- **:-internal-autofill-selected***
- **:target**
  - *Element was targeted by `<a href="#thetarget">`*
- **:where**
- **:is**
  ```css
  div .button,
  div .image,
  div .foo {
    ...
  }
  ```
  -> `div :is(.button, .image, .foo) { ... }`
  <https://caniuse.com/css-matches-pseudo>
  
  
 ## Funktionen
- **attr**
  - liefert immer einen String zurück, und ist daher im Grunde nur in Verbindung mit Pseudo-Elementen und `content` verwendbar.
  - <https://developer.mozilla.org/de/docs/Web/CSS/attr()>
- **calc**
- **env**
  - <https://webkit.org/blog/7929/designing-websites-for-iphone-x/>
- **hsl**
  - <https://www.w3schools.com/cssref/func_hsl.asp>
- **min**
  - Syntax: `min(...values)`
  - e.g.: `width: min(100px, 25%, 50vh, 30ch);`
- **max**
- **clamp**
  - *clamps a value between an upper and lower bound*
  - *takes three parameters: a minimum value, a preferred value, and a maximum allowed value*
  - `clamp(MIN, VAL, MAX)` is resolved as `max(MIN, min(VAL, MAX))`
  - math inside clamp: `width: clamp(200px, 50% + 20px, 800px)`
  - nützlich z.B. für Schriftgröße abh. von viewport: <https://css-tricks.com/linearly-scale-font-size-with-css-clamp-based-on-the-viewport/>
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/clamp>
- **fit-content(arg)**
  - values for arg: absolute length (px, ch, rem, vw) or %
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/fit-content>
  - resolves to `min(maximum size, max(minimum size, argument))`
  - non grid: max and min size is content-size
  - in grid
    - max size is `max-content`
    - min size is `auto`
    - calculation
      1) take max of 'auto' (max available width) and arg
      2) take min of max-content and result from (1)
- **minmax(min, max)**
  - use with grid
  - max is ignored if < min
  - `grid-template-columns: repeat(2, minmax(1fr, 50%))` is an invalid rule (completely ignored)
  - values
    - absolute length, %, min-/max-content, fr
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/minmax>
- **repeat(n, x)**
  - use with grid
  - values für n
    - Ganzzahl
      - Bsp.: `grid-template-columns: repeat(12, 1fr)` -> 12 gleich breite Columns
    - auto-fit
      - <mark>create a flexible (unkown) number of columns (or rows), as few as possible</mark>
      - `repeat(auto-fit, minmax(100px, 1fr))` *will expand the grid items to fill the available space*
      - <https://ishadeed.com/assets/grid-minmax/auto-fit.mp4>
    - auto-fill
      - create a flexible (unkown) number of columns (or rows)
      - creates as many columns (or rows) as possible, even if the number of columns is then higher then the number of grid items
      - can create empty columns (or rows)
      - `repeat(auto-fill, minmax(100px, 1fr))`
        *won’t expand the items. Instead, auto-fill will keep the available space reserved without altering the grid items width*
      - <https://ishadeed.com/assets/grid-minmax/auto-fill.mp4>
    - auto-fit vs auto-fill
      - *difference for sizing columns is only noticeable when the row is wide enough to fit more columns in it*
      - *If you’re using auto-fit, the content will stretch to fill the entire row width*
      - *Whereas with auto-fill, the browser will allow empty columns to occupy space in the row like their non-empty neighbors*
      - both commonly used together with minmax, eg. `repeat(auto-fit, minmax(min, max))`
      - <https://ishadeed.com/assets/grid-minmax/auto-fit-fill.mp4>
      - <https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit/>
