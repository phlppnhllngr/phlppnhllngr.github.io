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
  
