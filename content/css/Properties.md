---
layout: default
title: Properties
parent: CSS
---

# Properties
- <https://developer.mozilla.org/en-US/docs/Web/CSS/Reference#Keyword_index>
<br/>
- Kategorien
  - <a href="#text">text flow (white-space, word-break, ...)</a>
  - <a href="#pos">Positionierung (position, transform, ...)</a>
  - <a href="#font">font</a>
  - <a href="#scroll">scrolling</a>
  - <a href="#images">images & background</a>

## Diverse
- <u>@</u>
  - **@supports**
    ```css
    @supports (property: value) {}
    @supports (property1: value1) and (property2: value2) {}
    @supports (property1: value1) or (property2: value2) {}
    @supports not (property: value) {}
    ```
  - **@import**
  - **@media** -> @media
- <u>A</u>
  - **all**
    - Shorthand für alle Properties
    - nützlich z.B. für Resets (`all: unset`) oder `transition`
  - **animation-**
    - **animation-name**
    - **animation-direction**
    - **animation-fill-mode**
      - values
        - `none`
        - `forwards`
          - Element nimmt nach Ablauf die Werte des letzten Animationsschrittes an, unter der Berücksichtigung von animation-direction und animation-iteration-count
        - `backwards`
        - `both`
      - <https://developer.mozilla.org/de/docs/Web/CSS/animation-fill-mode>
    - **animation-play-state**
      - *whether an animation is running or paused*
    - **animation-duration**
    - **animation-delay**
  - **appearance**
    - *used to display an element using a platform-native styling*
    - *For instance, inputs with a type=search in WebKit browsers by default have rounded corners and are very strict in what you can alter via CSS. If you don't want that styling, you can remove it in one fell swoop with appearance*
  - **aspect-ratio**
    - aspect-ratio: width / height, `aspect-ratio: 16 / 9`
    - Stand 04/2021 nur Chromium (<https://caniuse.com/mdn-css_properties_aspect-ratio>)
    - <https://web.dev/aspect-ratio/>
    - <https://developer.mozilla.org/en-US/docs/Web/CSS/@media/aspect-ratio>
- <u>B</u>
  - **backdrop-filter**
    - Hintergrund-Effekte (zB blur, grayscale, contrast, ...)
    - -> filter, box-shadow 
    - <https://developer.mozilla.org/en-US/docs/Web/CSS/backdrop-filter>
  - **background-**
    - -> images & background
  - **border-**
    - borders with gradient: <https://css-tricks.com/gradient-borders-in-css/>
    - **color**
      - shorthand
      - <https://developer.mozilla.org/de/docs/Web/CSS/border-color>
      - values
        - rgb(), rgba(), `<name>`, currentColor, ...
        - kein Gradient
    - **spacing**
      -  legt die Abstände zwischen Tabellenzellen (`display: table`) fest
    - **style**
    - **width**
    - **image-**
      - shorthand
        - <https://developer.mozilla.org/de/docs/Web/CSS/border-image>
        - <https://css-tricks.com/almanac/properties/b/border-image/>
        - nimmt Liste an Werten
      - **source**
        - values: none, `<url>`, linear-gradient(), radial-gradient()
        - *incompatible with border-radius*
      - **slice**
      - **width**
      - **outset**
        -* Place the border image outside the border edges of an element*
      - **repeat**
  - **box-shadow**
    - -> filter, backdrop-filter
    - `box-shadow: 1px 1px 1px 1px green`
      offset-x | offset-y | blur-radius | spread-radius | color
      offset-x = px / rem / ... / 'inset' / 'outset'
    - mehrere möglich:
      ```
      box-shadow:
        0 0 0 10px hsl(0, 0%, 80%),
        0 0 0 15px hsl(0, 0%, 90%);
      ```
    - <https://css-tricks.com/almanac/properties/b/box-shadow/>
    - <https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow>
- **C**
  - caret-color
    - `<color> | auto | transparent`
    - https://developer.mozilla.org/en-US/docs/Web/CSS/caret-color
  - cursor
    - [codepen mit allen values](https://codepen.io/rebelchris/pen/jOqyVaB)
  - clip
    - DEPRECATED
    - https://developer.mozilla.org/de/docs/Web/CSS/clip
  - clip-path
    - https://developer.mozilla.org/de/docs/Web/CSS/clip-path
    - nur Ausschnitt des Elements wird angezeigt. Auch hover und Clicks werden nur für diesen Ausschnitt registriert.
    - values
      - polygon()
      - inset()
      - circle()
      - fill-box
      - url()
      - linear-gradient()
      - view-box
      - stroke-box
      - path()
      - ellipse()
    - &rightarrow; tools/codegen
  - color-scheme
  - column-* (-span, -width, -fill, -gap, -rule)
    - column-count
      - *specifies the number of columns an element's text should be divided into*
      - funktioniert nicht nur mit Text, man kann damit z.B. leicht ein [masonry-Layout für Bilder](https://css-tricks.com/seamless-responsive-photo-grid/) erzeugen
      - https://www.w3schools.com/cssref/css3_pr_column-count.asp
      - sehr guter browser support (https://caniuse.com/mdn-css_properties_column-count)
  - contain
    - *indicate that an element and its contents are, as much as possible, independent of the rest of the document tree (...) leading to obvious performance benefits.*
    - https://developer.mozilla.org/en-US/docs/Web/CSS/contain
  - content-visibility
    - Performancesteigerung durch Lazy-rendern von Inhalten außerhalb des Viewports
    - https://web.dev/content-visibility/
    - https://caniuse.com/css-content-visibility
  - content
    - für :before und :after
    - eg. `div:after { content: 'foo'; }`
    - line break mit `\A`: `content: "hello \A world"; white-space: pre;`
    - values
      - open-quote
      - close-quote
      - Funktionen
        - attr
          - `content: attr(title)`
          - line break innerhalb attr: `<div title="hello &#xa; world">` `content: attr(title); white-space: pre;`
        - counter, counters
        - url
          - Bild, video, sound
- D
  - display
    - values
      - contents
        - macht Element, wenn innerhalb eines Grids, "unsichtbar". Die Kinder des Elements werden dann zu den eigentlichen grid items.
        - https://blog.kulturbanause.de/2018/04/css-display-contents/
        - https://caniuse.com/css-display-contents (Stand 12/2020 partieller Browser-support)
      - run-in
      - grid &rightarrow; CSS/Grid
      - inline-grid
        - alle modernen Browser unterstützt
      - flex
      - table
      - none
      - ...
    - https://developer.mozilla.org/de/docs/Web/CSS/display
- G
  - gap
    - Abstand; flex und grid
    <details>
      <summary>caniuse</summary>
      <picture>
        <source type="image/webp" srcset="https://caniuse.bitsofco.de/image/flexbox-gap.webp">
        <source type="image/png" srcset="https://caniuse.bitsofco.de/image/flexbox-gap.png">
        <img src="https://caniuse.bitsofco.de/image/flexbox-gap.jpg" alt="Data on support for the flexbox-gap feature across the major browsers from caniuse.com">
      </picture>
    </details>
- H
  - height
    - set height equal to width
      - `width: auto; padding-bottom: 100%;` (https://codepen.io/pigparlor/pen/jOVZvEO)
      - &rightarrow; aspect-ratio
- I
  - inset
    - shorthand für top,right,bottom,left
    - Stand 17.6.21 kein Support in Edge
    - https://developer.mozilla.org/docs/Web/CSS/inset
    - https://caniuse.com/mdn-css_properties_inset
  - isolation
    - defines whether an element must create a new stacking context &rightarrow; z-index
    - Note: The isolation property is helpful when used with background-blend-mode or mix-blend-mode.
- L
  - line-height
    - *sets the height of a line box. It's commonly used to set the distance between lines of text. On block-level elements, it specifies the minimum height of line boxes within the element. On non-replaced inline elements, it specifies the height that is used to calculate line box height.* (mdn)
    - values
      - normal
        - *Depends on the user agent. Desktop browsers (including Firefox) use a default value of roughly 1.2, depending on the element's font-family.*
      - float
        - line-height = float-value * font-size
        - *In most cases, this is the preferred way to set line-height* (mdn)
      - %
        - *Relative to the font size of the element itself.*
      - px, rem, inherit, initial, unset
    - a11y
      - *Use a minimum value of 1.5 for line-height for main paragraph content.* (mdn)
    - https://developer.mozilla.org/en-US/docs/Web/CSS/line-height
- M
  - margin
    - *Margin is meant to increase the distance between siblings*
    - Margins aneinandergrenzender Elemente [können unter Umständen zusammenfallen](https://www.joshwcomeau.com/css/rules-of-margin-collapse/)
      (nur vertikale margins, auch genestete Elemente)
  - mask
    - https://developer.mozilla.org/de/docs/Web/CSS/mask
    - *allows users to alter the visibility of an item by either partially or fully hiding the item. This is accomplished by either masking or clipping the image at specific points.*
  - mix-blend-mode
- O
  - object-fit
    - wie bilder sich dem umgebenden container anpassen sollen, wenn sie nicht die genau gleichen maße (pixel) haben. ob aspect ratio erhalten bleiben soll.
    - *sets how the content of a replaced element, such as an `<img>` or `<video>`, should be resized to fit its container*
    - https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit
  - outline
    - shorthand für: width, style, color
    - kein radius möglich
    - mögliche alternativen: box-shadow, filter:drop-shadow
  - outline-offset
    - sets the amount of space between an outline and the edge or border of an element
    - https://developer.mozilla.org/en-US/docs/Web/CSS/outline-offset
  - overflow
    - *In order for overflow to have an effect, the block-level container must have either a set height (height or max-height) or white-space set to nowrap.*
    - *Setting one axis to visible (the default) while setting the other to a different value results in visible behaving as auto.*
      ```css
      overflow-x: visible;
      overflow-y: auto;
      ```
      wird zu:
      ```css
      overflow-x: auto;
      overflow-y: auto;
      ```
    - https://developer.mozilla.org/en-US/docs/Web/CSS/overflow
  - overflow-x
    - https://developer.mozilla.org/en-US/docs/Web/CSS/overflow-x
- P
  - perspective
    - https://css-tricks.com/almanac/properties/p/perspective/
    - *gives an element a 3D-space by affecting the distance between the Z plane and the user*
    - *you can use the transform property to move and rotate objects in a 3D space (with the X, Y, and Z axes), then use perspective to control depth*
  - pointer-events
    - `pointer-events: none` führt dazu, dass `cursor` nicht mehr greift. Workaround:
      ```html
      <div style="cursor: not-allowed;">
        <button style="pointer-events: none;">Some Text</button>
      </div>
      ```
- R
  - resize
    - Sets whether an element is resizable, and if so, in which directions
- S
  - shape-outside
    - Defines a shape—which may be non-rectangular—around which adjacent inline content should wrap
    - wird i.d.r. dazu verwendet, text in einer best. form um etwas herum laufen zu lassen.
- T
  - text-decoration-thickness
  - translate &rightarrow; Positionierung
  - transform
    - translate &rightarrow; Positionierung
    - rotate
    - scale
    - mehrere `transform: translate(100px 100px) rotate(180deg)`
    - moderne Alternativen: `translate`, `rotate`, `scale` (eigenständige Properties)
      https://webkit.org/blog/11420/css-individual-transform-properties/
      Stand 12/2020 schlechter browser support (https://caniuse.com/mdn-css_properties_rotate)
- U
  - user-select
    - https://codersblock.com/blog/using-css-to-control-text-selection/
- W
  - width
    - does not include padding, borders, or margins &rightarrow; box-sizing
  - will-change
    - *hints to browsers how an element is expected to change. Browsers may set up optimizations before an element is actually changed. These kinds of optimizations can increase the responsiveness of a page by doing potentially expensive work before they are actually required.*
    - *intended to be used as a last resort, in order to try to deal with existing performance problems. It should not be used to anticipate performance problems.*
    - https://developer.mozilla.org/en-US/docs/Web/CSS/will-change
- z-index
  - used to specify:
    - The stack order/level of the element/box in the current stacking context
    - Whether the box establishes a stacking context
  ```html
  <body>
    <div id="div1" style="position:relative; z-index:10"></div>
    <div id="div2" style="position:relative; z-index:5">
        <div id="div3" style="position:absolute; z-index:100"></div>
    </div>
  </body>
  ```
  - div1 ist VOR div3; *a child’s z-index has no effect outside its group*
  - Element muss `position` != `static` haben, damit sich z-index auswirkt
  - auch opacity und andere properties beeinflussen stacking-context (siehe MDN-Link)
    <br/><blockquote>
      <h4>A stacking context is formed, anywhere in the document, by any element in the following scenarios:</h4>
      <ul>
        <li>Root element of the document (html).</li>
        <li>Element with a <mark>position</mark> value absolute or relative and z-index value other than auto.</li>
        <li>Element with a <mark>position</mark> value fixed or sticky (sticky for all mobile browsers, but not older desktop).</li>
        <li>Element that is a child of a <mark>flex</mark> container, with z-index value other than auto.</li>
        <li>Element that is a child of a <mark>grid</mark> container, with z-index value other than auto.</li>
        <li>Element with a <mark>opacity</mark> value less than 1 (See the specification for opacity).</li>
        <li>Element with a <mark>mix-blend-mode</mark> value other than normal.</li>
        <li>Element with any of the following properties with value other than none:
        <mark>transform, filter, perspective, clip-path, mask / mask-image / mask-border</mark></li>
        <li>Element with a <mark>isolation</mark> value isolate.</li>
        <li>Element with a <mark>-webkit-overflow-scrolling</mark> value touch.</li>
        <li>Element with a <mark>will-change</mark> value specifying any property that would create a stacking context on non-initial value (see this post).</li>
        <li>Element with a <mark>contain</mark> value of layout, or paint, or a composite value that includes either of them (i.e. contain: strict, contain: content).</li>
      </ul><br/>
      Within a stacking context, child elements are stacked according to the same rules previously explained. Importantly, the z-index values of its child stacking contexts only have meaning in this parent. Stacking contexts are treated atomically as a single unit in the parent stacking context.
    </blockquote><br/>
  - https://philipwalton.com/articles/what-no-one-told-you-about-z-index/
  - https://thirumanikandan.com/posts/learn-z-index-using-a-visualization-tool
  - https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context
  - https://www.joshwcomeau.com/css/stacking-contexts/
  - &rightarrow; isolation


## text flow
<span id="text"></span>
- https://www.cjcid.com/articles/wrapping-long-words-css-html/
- https://css-tricks.com/where-lines-break-is-complicated-heres-all-the-related-css-and-html/
- [playground (codepen)](https://codepen.io/chriscoyier/pen/qoLLpN)
<br/>
- letter-spacing
- line-clamp
  - truncates text at a specific number of lines
  - nicht supported in Firefox (6.7.19), FF understützt aber **-webkit-line-clamp**
  - https://caniuse.com/#feat=css-line-clamp
  - nur Verwendung zusammen mit `display: -webkit-box; -webkit-box-orient: vertical; overflow: hidden;` möglich
- hyphens
  - overflow wird verhindert, indem an definierten stellen (manual: `&shy;`, `&hyphen;`) oder automatisch (auto) Trennstriche in Wörter eingefügt werden
  - https://caniuse.com/#feat=css-hyphens
  - der browser-support (von `auto`) ist auch abh. von der user-sprache (?)
  - https://developer.mozilla.org/de/docs/Web/CSS/hyphens
  - https://www.w3schools.com/cssref/css3_pr_hyphens.asp
  - http://clagnut.com/blog/2395
- tab-size
- text-indent
- text-overflow
  - https://www.w3schools.com/cssref/css3_pr_text-overflow.asp
  - ellipsis
  - clips
  - `<string>`
    - user defined value
    - firefox only
- white-space
  - https://www.cjcid.com/articles/wrapping-long-words-css-html/#white-space
  - is managing how spaces are rendered
  - The default normal value renders text based on the following rules: The text is wrapped to fit the container. MULTIPLE SPACES and TABS are collapsed to a single space. SOFT BREAK LINES are converted to single space.
  - *To make words break within themselves, use overflow-wrap, word-break, or hyphens instead.*
  - values
    - normal
    - nowrap
      - *Collapses white space as for normal, but suppresses line breaks (text wrapping) within the source.*
    - pre
    - pre-wrap
    - pre-line
    - break-spaces
  - https://developer.mozilla.org/en-US/docs/Web/CSS/white-space
- word-break
  - https://developer.mozilla.org/en-US/docs/Web/CSS/word-break
  - https://www.cjcid.com/articles/wrapping-long-words-css-html/#word-break
  - is managing how line breaks are rendered
  - values
    - normal
      - *Use the default line break rule.*
    - break-all
      - *To prevent overflow, word breaks should be inserted between any two characters*
      - *In contrast to word-break: break-word and overflow-wrap: break-word (see overflow-wrap), word-break: break-all will create a break at the exact place where text would otherwise overflow its container (even if putting an entire word on its own line would negate the need for a break).*
    - keep-all
      - *Non-CJK text behavior is the same as for normal*
    - break-word (deprecated)
- word-spacing
  - https://developer.mozilla.org/de/docs/Web/CSS/word-spacing
- overflow-wrap <small>(legacy name: word-wrap)</small>
  - https://www.cjcid.com/articles/wrapping-long-words-css-html/#overflow-wrap
  - https://developer.mozilla.org/en-US/docs/Web/CSS/overflow-wrap
  - is enabling the line breaks
  - *In contrast to word-break, overflow-wrap will only create a break if an entire word cannot be placed on its own line without overflowing.*
  - values
    - normal
      - *Lines may only break at normal word break points (such as a space between two words).*
    - anywhere
      - *To prevent overflow, an otherwise unbreakable string of characters — like a long word or URL — may be broken at any point if there are no otherwise-acceptable break points in the line. No hyphenation character is inserted at the break point. Soft wrap opportunities introduced by the word break are considered when calculating min-content intrinsic sizes.*
    - break-word
- line-break
  - is managing how line breaks are rendered mainly for CJK (chinese, japanese, korean) languages
- text-space-collapse <small>(legacy name: white-space-collapse)</small>
  - will allow to control further how the spaces and line breaks are rendering
  - https://caniuse.com/#search=text-space-collapse


## scrolling
<span id="scroll"></span>
- scroll-behavior
  - wie der Browser zum Ziel springt, bei `<a href="#id">`. Default: Direkter "Sprung" ohne Scroll (`auto`)
  - `auto | smooth`
  - https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior
- scroll-padding
  - setzt scroll-offset für alle children, parent braucht overflow-*-property
  - *Set the offset for in-page anchors links*
  - https://codepen.io/pawelgrzybek/pen/rbMrRY
- scroll-margin
  - setzt scroll-offset für ein element
  - https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-margin
- scroll-snap-*
  - scroll-snap-type
    - "Einrastpunkte" für Scroll-Elemente, ähnlich denen eines range-sliders
  - scroll-snap-align
  - scroll-snap-destination
  - scroll-snap-points-x
  - scroll-snap-coordinate
  - scroll-snap-stop
    - https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-snap-stop
- overscroll-behavior
  - https://developer.mozilla.org/en-US/docs/Web/CSS/overscroll-behavior
  - values: none | contain | auto
  - *By default, mobile browsers tend to provide a "bounce" effect or even a page refresh when the top or bottom of a page (or other scroll area) is reached.*
  - *You may also have noticed that when you have a dialog box with scrolling content on top of a page of scrolling content, once the dialog box's scroll boundary is reached, the underlying page will then start to scroll — this is called scroll chaining.*
  - *Problem with this solution [contain, none] is that it only works if overlay is scrollable. If you have a modal and it all fit on screen so there is no scroll inside — it will not stop the body scroll.*


## @import
https://developer.mozilla.org/en-US/docs/Web/CSS/@import
`@import url('landscape.css') screen and (orientation:landscape);`
*So that user agents can avoid retrieving resources for unsupported media types, authors may specify media-dependent @import rules.*
```css
@import url;
@import url list-of-media-queries;
@import url supports( supports-query );
@import url supports( supports-query ) list-of-media-queries;
```


## images & background
<span id="images"></span>
- background
  - shorthand
  - https://www.freecodecamp.org/news/learn-css-background-properties/
  - https://developer.mozilla.org/de/docs/Web/CSS/background
  - &rightarrow; tools/codegen
- background-color
  - values
    - Farbwert
- background-image
  - https://developer.mozilla.org/de/docs/Web/CSS/background-image
  - https://css-tricks.com/a-complete-guide-to-css-gradients/
  - Man kann mehrere Werte hintereinander angeben. Das zuerst definierte Hintergrundbild ist dabei das Oberste.
  - values
    - linear-gradient()
      - https://drafts.csswg.org/css-images-3/#linear-gradients
      - https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/linear-gradient()
      - values
        - 0deg = to top
      - Examples
        `l-g(yellow, orange)`
        `l-g(0.25turn, yellow, 10%, orange)`
        `l-g(to right, yellow, orange)`
        `l-g(217deg, rgba(...), rgba(...) 70%)`
        `l-g(45deg, red 0 50%, blue 50% 100%)`
    - radial-gradient()
      - https://drafts.csswg.org/css-images-3/#radial-gradients
      - https://css-tricks.com/radial-gradient-recipes/
      - https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/radial-gradient()
      - Examples
        `r-g(circle at center, ...)`
        `r-g(ellipse at 100%, ...)`
        `r-g(cyan 0%, yellow 20%, salmon 40%)`
        `r-g(farthest-corner at 40px 40px, pink 0%, blue 100%)`
    - url()
    - conic-gradient()
      - https://caniuse.com/css-conic-gradients (alle modernen browser; 13.04.2021)
      - https://www.digitalocean.com/community/tutorials/css-conic-gradients
      - https://www.geeksforgeeks.org/css-conic-gradient-function/
    - image-set()
      - neue bildformate für moderne browser, fallbacks für ältere
      - https://caniuse.com/css-image-set
      - js detection für nicht unterstützte browser (html attrs): https://github.com/leechy/imgsupport
- background-position
  - *bestimmt die Position des Hintergrundbildes*
  - *Standardwert: 0% 0%*
  - https://developer.mozilla.org/de/docs/Web/CSS/background-position
- background-size
  - values
    - contain
    - 50% 50%
- background-repeat
  - round
  - no-repeat
- background-attachment
- background-clip
  - &rightarrow; -webkit-background-clip
  - *This is the same as the background-origin property. The main difference is that background-clip CUTS the image to fit inside the box, while background-origin PUSHES the content inside the box to fit*
  - values
    - border-box (default)
    - text
      ```css
      color: transparent;
      background-image: linear-gradient(to right, orange, purple);
      -webkit-background-clip: text;
      background-clip: text;
      ```
      <div style=" display: inline-block; font-size: 2rem; font-weight: bold; color: transparent; background-image: linear-gradient(to right, orange, purple); -webkit-background-clip: text;">hello world</div>
      <br/>
      example: <a href="https://pmugf.csb.app/">https://pmugf.csb.app/</a>
    - ...
  - https://developer.mozilla.org/de/docs/Web/CSS/background-clip
  - https://www.freecodecamp.org/news/learn-css-background-properties/#background-clip
- background-origin
  - *legt den Bereich des Hintergrundbildes fest (bzw. den Ausgangspunkt eines background-image). background-origin hat keinen Effekt, wenn background-attachment auf fixed gesetzt wurde.*
  - values: border-box | padding-box | content-box | inherit
  - https://www.freecodecamp.org/news/learn-css-background-properties/#background-origin
  - https://developer.mozilla.org/de/docs/Web/CSS/background-origin
<br/><hr/><br/>
- image-rendering
  - values
    - -webkit-optmize-contrast
    - pixelated
    - ...
- mask-image
  - ermöglicht z.B. nicht-rechteckige Bilder oder Image-Overlays
  - values
    - url()
    - linear-gradient()
  - https://css-tricks.com/almanac/properties/m/mask-image/
- object-fit
  - *sets how the content of a replaced element, such as an \<img> or \<video>, should be resized to fit its container* (mdn)
  - *You can alter the alignment of the replaced element's content object within the element's box using the object-position property.*
  - img sollte width und height jeweils 100% haben
  - values
    - contain
    - fill
       - fill container, dont preserve aspect ratio, stretch if needed
    - cover
      - fill container, resize content, preserve aspect ratio, clip if needed
    - scale-down
    - none
      - fill container, dont resize content, clip if needed
    - revert, unset, initial, inherit
  - https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit
- object-position
  - https://developer.mozilla.org/en-US/docs/Web/CSS/object-position


## font
<span id="font"></span>
- @font-face
  - https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face
  ```
  @font-face {
    font-family: "Roboto"
    src: local("Roboto"),
          url("./path/to/Roboto.woff2") format("woff2"),
          url("./path/to/Roboto.woff") formtat("woff")
  }
  body {
    font-family: "Roboto"
  }
  ```
- font-family
- unicode-range
  - sets the specific range of characters to be used from a font defined by @font-face and made available for use on the current page. If the page doesn't use any character in this range, the font is not downloaded; if it uses at least one, the whole font is downloaded.
  - `unicode-range: U+00DF;` font nur runtergeladen wenn "ß" auf Seite vorhanden. Funktioniert mit später eingefügtem Text.
  - Nur Zeichen der spezifizierten Range werden in der Schriftart dargestellt.
  - https://developer.mozilla.org/en-US/docs/Web/CSS/%40font-face/unicode-range
- font-display
  - determines how a font face is displayed based on whether and when it is downloaded and ready to use
  - font-display is used inside of a @font-face
  - values
    - Wenn ein Browser eine Font anwenden will, die noch nicht geladen wurde, wartet er einen kurzen Moment (font block period). Während dieser Zeit ist der Text unsichtbar (Flash of invisible text; FOIT). Wenn nach dieser kurzen Wartezeit die Font noch nicht da ist, wird der Text mit Fallback-Font dargestellt (font swap period, Flash of unstyled text; FOUT). Wenn die Font dann später geladen wurde, wird der Text mit der neuen Font dargestellt.
    - auto
      - font display strategy is defined by the user agent
    - block
      - short block period, infinite swap period
    - swap
      - extremely small block period, infinite swap period
    - fallback
      - extremely small block period, short swap period
    - optional
      -  extremely small block period, no swap period
  - https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display
- font-size
  - use vw and vh and clamp() to get responsive text without @media
    https://www.w3schools.com/howto/howto_css_responsive_text.asp
    https://css-tricks.com/linearly-scale-font-size-with-css-clamp-based-on-the-viewport/
  - was font-size und line-height bedeuten: https://tonsky.me/blog/font-size/
- font-weight
- font-style
  - normal | italic | oblique
- font-stretch
- **variable fonts**
  - font-variation-settings
    - `font-weight: bold` funktioniert mit VF nicht, weil `bold` nicht vordefiniert ist. Stattdessen: `font-variation-settings: 'wght' 700`


## Positionierung
<span id="pos"></span>
- position (& top, left, bottom, right)
  - https://www.chenhuijing.com/blog/understanding-positioning-in-css/
  - https://ishadeed.com/article/learn-css-positioning
  - https://developer.mozilla.org/de/docs/Web/CSS/position
  - values
    - relative
      - specify element's offset from its normal position
    - absolute
      - specify the element's offset from its containing block
      - For absolute positioning, the <u>containing block is the closest positioned ancestor</u> (An element with a position other than static)
      - *Das Element wird aus dem normalen Fluss gelöst und unabhängig verschoben. Dabei können andere Elemente verdeckt werden. Diese verhalten sich so, als ob das Element nicht vorhanden wäre und lassen keinen Platz für das Element.*
      - *Absolutely positioned elements are completely removed from the document flow, and thus their dimensions cannot alter the dimensions of their parents.*
    - fixed
      - specify element's offset from its containing block
      - The containing block for fixed positioned elements is the viewport, <u>except</u> when an element's parent has one of the following properites applied to it: transform, filter or perspective (Der Wert muss dabei etwas anderes sein als initial|inherit|none etc.)
      - *Beim Drucken wird das Element auf jeder Seite an der positionierten Stelle angezeigt.*
      - Wenn ein Element mit `position: fixed` auch `width: 100%` hat, beziehen sich die 100% nicht auf den parent, sondern auf den nächstgelegenen container (mit transform/filter/perspective; wenn nicht vorhanden: document/viewport). Damit das Kind-Element die gleiche Breite hat wie der parent, sollte der parent `width: x` und das child `width: inherit` haben.
    - static
      - the default behavior
      - *Die Eigenschaften top, right, bottom oder left haben keine Auswirkungen.*
    - sticky
      - *Eine Mischung zwischen fixed und relative: Das Element wird vom normalen Fluss aus verschoben und hat keinen Einfluss auf andere Elemente, solange es sich innerhalb des Viewports befindet. Sobald es sich ausserhalb befindet, wird das Element aus dem normalen Fluss gelöst und bleibt so beim Scrollen an seiner fest definierten Position.* (mdn)
- transform
  - will use hardware acceleration where possible
  - values
    - translate
      - performanter als position (siehe css triggers)
    - translate3d(x, y, z)
- translate
  - specify translation transforms individually and independently of the `transform` property
  - Stand 15.08.20 nur Firefox (https://caniuse.com/mdn-css_properties_translate)
  - https://developer.mozilla.org/en-US/docs/Web/CSS/translate
- top: bei %-Angaben: siehe CSS/Units
- right
- bottom 
- left
