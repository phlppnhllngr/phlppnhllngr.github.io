---
title: Values
parent: CSS
---

# Values
- **inherit**
  - Wert soll von nächst höherem Parent mit diesem Prop geerbt werden
- **initial**
  - Wert soll den initialien Wert haben (laut spec)
  - spec != browser default; div::`display` ist z.B. `inline` per spec und `block` per browser default
- **unset**
  - bei vererbbaren Props (z.B. `font-size`) = inherit
  - bei nicht vererbbaren Props (z.B. `border`) = initial
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/unset>
- **revert**
  - Wert auf inherited oder als Fallback auf user-agent-default zurücksetzen (z.B. div::display -> `block`)
  - <https://caniuse.com/css-revert-value>
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/revert>
- **min-content**
  - für (min-/max-)width, height, flex-basis
  - die Box nimmt die Breite ihres längsten Kind-Elements (oder Wortes) an
  - die Box overflowt ihren Container wenn nötig
- **max-content**
  - alle Kinder/Wörter in einer Zeile
  - die Box overflowt ihren Container wenn nötig
- **Funktionen**
  - fit-content, min, max, minmax, clamp, ...


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
  - Verwendung mit Grid
  - ungültige Werte werden ignoriert (z. B. max < min)
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
