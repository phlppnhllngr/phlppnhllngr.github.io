---
parent: Webdev
title: Fonts
---

# Fonts
- -> CSS/Properties/Font
- -> UI Design/Resourcen/Fonts
- *Only fonts that are covered by both operating systems are considered to be <mark>web-safe fonts</mark>. Only five fonts are considered universal:
Arial, Courier New, Georgia, Times New Roman, Verdana*
- <https://css-tricks.com/snippets/css/system-font-stack/>
- Die System-Fonts von Windows (10) liegen unter `C:/Windows/Fonts`
- Dieses Browser-Tool lässt einen den Inhalt einer Font-Datei betrachten: <https://fontdrop.info/> (09/20 kein woff2)
- Fonts gibt es oft als "hinted" oder "unhinted" Version (<https://en.wikipedia.org/wiki/Font_hinting>)


## Formate
- **ttf**
  - TrueType font
  - very good support in older browsers
- **otf**
  - OpenType font
- **woff**
  - *Woff is a compressed (zipped) form of the TrueType - OpenType font.*
  - very good support in older browsers
- **woff2**
  - *WOFF 2.0, based on the Brotli compression algorithm and other improvements over WOFF 1.0 giving more than 30 % reduction in file size*
  - konvertierung von ttf zu woff2
    - woff2 cli tool
      - https://github.com/google/woff2
      - `apt install woff2`
      - `woff2_compress myfont.ttf`
      - funktioniert auch mit variable fonts
- **eot**
- svg
- *[<mark>Only use WOFF2</mark>, or if you need legacy support, WOFF. Do not use any other format (svg and eot are dead formats, ttf and otf are full system fonts, and should not be used for web purposes)](https://stackoverflow.com/a/11002874)* (05/2019)


## Performance
- [prüfen, ob Font lokal verfügbar vor Download](<https://www.reddit.com/r/css/comments/fxsjjm/til_css_can_check_for_a_font_installed_locally/>)
- <https://www.zachleat.com/web/font-checklist/>
- -> Webdev/Performance/Preloading
  ```
  <link rel="preload" href="/fonts/myfont.woff2" as="font" type="font/woff2" crossorigin="anonymous"/>
  ```
  `crossorigin` wird bei Font-preload immer gebraucht, auch bei same-origin-Requests
- **subsetting**
  - *removing unneeded characters from fonts*
  - <https://bytes.zone/posts/reducing-asset-size-with-subsetting/>
  - <https://github.com/filamentgroup/glyphhanger>
  - <https://transfonter.org/>


## Variable Fonts
  - bei herkömlichen Fonts muss man pro "Variante" eine Datei runterladen; z.B. für italic, weight-300, weight-900, ...
  - caniuse 09/20: alle modernen Browser (<https://caniuse.com/variable-fonts>)
  - usage
    ```css
    @font-face {
      font-family: "Roboto";
    }
    @supports (font-variation-settings: normal) {
      @font-face {
        font-family: "Roboto VF";
        src: local("Roboto VF") local("Roboto-VF") url("fonts/Roboto-VF.woff2") format('woff2-variations');
        font-style: normal;
        font-weight: 100 900; /* oblique 0deg 12deg; */
        font-stretch: 75% 125%;
        font-display: swap
      }
    }
    body {
      font-family: "Roboto";
    }
    @supports (font-variation-settings: normal) {
      body {
        font-family: "Roboto VF";
        font-variation-settings: "wght" 300;
      }
    }
    ```
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Fonts/Variable_Fonts_Guide>
  - <https://www.thatsanegg.com/blog/stop-importing-multiple-fonts-and-start-using-variable-fonts/>
  - Library: <https://v-fonts.com/>
  - <https://medium.com/clear-left-thinking/how-to-use-variable-fonts-in-the-real-world-e6d73065a604>
  - <https://www.viget.com/articles/beginners-guide-to-variable-fonts-2/>
  - <https://blog.logrocket.com/variable-fonts-is-the-performance-trade-off-worth-it/>
    - *In general, variable fonts improve performance because you only have to use one font file.*
    - *On the other hand, a variable font file is huge, precisely because it contains all the variations. The Roboto Variable Font, for instance, is 3.36MB in TTF format, while a static Roboto font variant is around 165–175KB in TTF format.*
    - *Ultimately, the performance trade-off of variable fonts depends on how these two metrics — the number of HTTP requests and the total size of font files — balance each other out.* 
  - <https://thetrevorharmon.com/blog/how-to-prepare-and-use-variable-fonts-on-the-web>
  - <https://systemfontstack.com/>
