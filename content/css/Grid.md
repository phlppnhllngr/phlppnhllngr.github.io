---
title: Grid
parent: CSS
---

# Grid
- standardmäßig wird bei `display: grid` pro child-Element eine Zeile angelegt (nicht etwa eine Spalte). Spalten anlegen statt rows: `grid-auto-flow: column`
- mehrere Elemente können in der selben Grid-Cell sein


## Grid-Container-Props
- **grid-template-columns**
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns>
  - default 1 Column
  - mögliche Werte
    - px, %, ch, ...
    - fraction units, z.B. `1fr` oder `1.2fr`
      - `2fr 3fr` bedeutet z.B., dass die 2. Spalte 3/5 der gesamten Breite einnimmt
      - fr vs %
        - fr verteilt nur den freien Platz, berücksichtigt also grid-gap
        - 5 Columns mit je 1fr und grid-gap => kein Overflow
        - 5 Columns mit 20% und grid-gap => Overflow
      - <https://css-tricks.com/introduction-fr-css-unit/>
    - `auto`
      - nimmt den nach Abzug der fixen Columns übrigen Platz ein
    - repeat(n, x) &rightarrow; css/funktionen
    - subgrid
  - den entstehenden Grid-Lines kann man beliebige Namen geben
    - z.B. `grid-template-columns: [first-line] 1fr [line-2] 5fr [line-3 last-line]`
      gibt allen 3 Column-Lines Namen (die mit `grid-column` referenziert werden können), wobei Line 3 sogar 2 versch. Namen hat
    - wenn man die Namen nach dem Schema x-start, x-end vergibt, z.B. content-start und content-end, dann kann man bei `grid-column` einfach nur `content` angeben
    - wenn es grid-row-lines mit gleichen Namen gibt, und ein Bereich des grid von 4 Lines mit zusammengehörigen Namen umgeben ist, kann man bei `grid-area` des Bereichs diesen Namen angeben, z.B. `content`
- **grid-template-rows**
  - Bsp.: `grid-template-rows: 3ch auto minmax(10px, 60px);`
  - values
    - masonry
      - <https://css-tricks.com/a-lightweight-masonry-solution/>
    - subgrid
    - ...
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-rows>
- **grid-auto-rows**
  - in einem Grid mit z.B. 2 Columns und 2 Rows, aber 8 Items, werden implizit 2 neue Rows gebildet (keine Columns!)
  - die implizit erzeugten Rows haben aber nicht die in `grid-template-rows` festgelegte Höhe (sondern je nach Content-Höhe)
  - mit grid-auto-rows kann die Höhe dieser Rows festgelegt werden, z.B. `grid-auto-rows: 100px;`
  - wenn `grid-auto-rows` vorhanden ist, kann auf `grid-template-rows` verzichtet werden
- **grid-auto-columns**
  - <https://developer.mozilla.org/de/docs/Web/CSS/grid-auto-columns>
- **grid-template x / y**
  - shorthand für grid-template-rows / grid-template-columns
  - `grid-template: repeat(4, 1fr) / repeat(2, 1fr);`
- **grid-template-areas**
  - ```css
      grid-template-areas:
        "head    head   "
        "sidebar content";
    ```
  - "." für empty cells
- **grid-row-gap**
- **grid-column-gap**
- **grid-gap**
  - shorthand für grid-row-gap und grid-column-gap
- **grid-auto-flow**
  - *controls how the auto-placement algorithm works, specifying exactly how auto-placed items get flowed into the grid*
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-flow>
  - row (default)
  - column
  - dense
    - *attempts to fill in holes earlier in the grid, if smaller items come up later. This may cause items to appear out-of-order, when doing so would fill in holes left by larger items.*
    - wenn das Grid Lücken enthält, z.B. weil die Items verschieden hoch oder Breit sind, wird das grid mit `grid-auto-flow: dense` versuchen, diese Lücken zu schließen. Es ändert dafür die Reihenfolge der Items automatisch, (relativ) unabhängig von ihrer Reihenfolge im Markup
    - nützlich für 'masonry panes'
  - row dense
  - column dense
- **justify-content**
  - horizontale Anordnung des gesamten Inhalts des Grids, falls die Gesamtbreite aller Columns weniger ist als die Breite des Grid selbst
  - values
    - start (default, wie `left`): Anordnung am linken Rand
    - end (wie `right`)
    - center
      - Kombination mit `align-content: center` um den Inhalt zu zentrieren
    - space-between
      - Abstände zwischen den Spalten werden gleichmäßig verteilt, kein Abstand der beiden äußeren Spalten zum Grid
    - space-evenly
      - Abstände zwischen den Spalten genauso groß wie Abstand der beiden äußeren Spalten zum Grid-Rand
    - space-around
      - Abstand zur grid-Kante ist halb so groß wie Abstand zw. 2 Spalten
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content>
- **align-content**
  - vertikale Anordnung des gesamten Inhalts des Grids, falls der Gesamtinhalt kürzer (weniger hoch) als das Grid selbst ist
  - values
    - start
    - end
    - center
    - stretch
    - space-around, space-evenly, space-between
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/align-content>
- **justify-items**
  - horizontale Ausrichtung der Items steuern
  - Wert individuell pro Item setzen: siehe `justify-self`
  - values
    - stretch (default)
      - Items nehmen die genze Breite ihrer grid-Column ein
    - center
      - Items zentriert innerhalb ihrer grid-Column. Nehmen nur die Breite ein, wie es ihr Content erfordert
    - start
      - nur erforderliche Breite, linksbündig
    - end
      - nur erforderliche Breite, rechtsbündig
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/justify-items>
- **align-items**
  - vertikale Ausrichtung der Items steuern
  - Wert individuell pro Item setzen: siehe `align-self`
  - values
    - center
    - start: Elemente werden am oberen Rand ihrer row angeordnet
    - end
    - stretch: Elemente nehmen gesamte Höhe ihrer Zelle (bzw. row) ein
    - ...
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/align-items>
- **place-items**
  - `place-items: y x`
  - shorthand für align-items justify-items
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/place-items>
- **place-content**
  - shorthand für align-content justify-content
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/place-content>


## Grid-Item-Props
- **grid-column-start**
  - Werte
    - n (n ist die Column-Line, entweder Index (beginnend bei 1) oder Name (siehe grid-template-columns))
- **grid-column-end**
  - Werte
    - n (n ist die Column-Line, NICHT die Column. Ein Grid mit 2 Columns hat z.B. 3 Column-Lines: |abc|xyz|)
    - `grid-column-end: -1` um Item in letzter Spalte zu platzieren
- **grid-column**
  - `grid-column: a`, `grid-column: a / b`, `grid-column: a / span b`
  - shorthand für grid-column-start / grid-column-end
  - wenn b den Wert `-1` hat, ist die letzte Column-Line gemeint (nützlich z.B. wenn sich die Anzahl Columns ändert)
  - a kann den Wert `auto` annehmen
- **grid-row**
  - span x
- **grid-area**
  - value: Name, so wie in `grid-template-areas` definiert
- **justify-self**
  - eigene horizontale Anordnung innerhalb der Zelle ("alignment container")
  - um die Anordnung für alle Items des Grid zu setzen: siehe `justify-items`
  - values
    - basic
      - start | end | center | stretch
    - advanced
      - auto | normal | flex-start | flex-end | self-start | self-end | left | right
      - baseline | first baseline | last baseline
      - safe center | unsafe center
      - **Hinweise**
        - start == flex-start, end == flex-end
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/justify-self>
- **align-self**
  - eigene vertikale Anordnung innerhalb der Zelle
  - um die Anordnung für alle Items des Grid zu setzen: siehe `align-items`
  - values: start, center, end, auto, stretch, ...
- **place-self**
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/place-self>


## subgrid
- Stand 09/20 nur Firefox
- <https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Subgrid>
- <https://caniuse.com/#feat=css-subgrid>


## Lernen
- <https://css-tricks.com/snippets/css/complete-guide-grid/>
- <https://gridbyexample.com/>
- <https://cssgridgarden.com/>
- <https://www.youtube.com/watch?v=t6CBKf8K_Ac>
- <https://scrimba.com/g/gR8PTE>
- <https://tympanus.net/codrops/css_reference/grid/>
- <https://medium.com/@js_tut/the-ultimate-guide-to-css-grid-ac05c236a2ad>
- <https://semicolon.hashnode.dev/css-grid-tutorial>
- <https://jst.hashnode.dev/css-grid-tutorial?v=3>
- <https://learncssgrid.com/>
- <https://www.euismod.dev/#/>
- <https://semicolon.dev/tutorial/css/complete-css-grid-tutorial?tutorial>
- <https://www.reddit.com/r/webdev/comments/m0gpnl/an_interactive_guide_to_css_grid/>
- <https://www.reddit.com/r/css/comments/ki68y5/mastering_css_grid_model_in_2021_build_5_layouts/>
