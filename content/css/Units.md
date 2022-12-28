---
title: Units
parent: CSS
---

# Units
- <https://smazee.com/blog/css-units-px-em-rem-vh-vw-vmin-vmax>

## px
- *this means "CSS pixel", not screen pixel. On @2x ("Retina") screens it covers ~4 screen pixels (2x2). On some Android phones @3x, therefore ~9px. This applies mostly to images, they'll show blurry on mobile devices. But also a border-width might show up as thicker or thinner as intended.*
- *px is not an absolute pixel. It depends on the scale factor of the device*

## %
- <https://wattenberger.com/blog/css-percents>
- unterschiedliche Bedeutung je nach Kontext
- width und height: bezieht sich auf Parent
- top und left
  - `top: 50%` bedeutet, die obere Kante fängt nach 50% der Höhe des Parents an
  - `left: 50%` bedeutet, die linke Kante fängt nach 50% der Breite des Parents an
- margin
  - margins (auch -top und -bottom!) beziehen sich auf die BREITE des Parents
- padding
  - wie margin beziehen auch sie sich auf die BREITE des Parents
  - wenn ein mit `padding-top: x%` berechneter Wert die Höhe des Elements überschreitet, wird das Element höher (mit `box-sizing: border-box`)
  - wenn ein mit `padding-left: x%` berechneter Wert die Breite des Elements überschreitet, wird das Element breiter (mit `box-sizing: border-box`)
  - Bsp: width: 10%, padding-left: 100% => Element nimmt gesamte Breite ein
- transform: translate
  - %-Werte beziehen sich auf EIGENE Höhe und Breite
  - `transform: translate-top: 50%` bewirkt, dass das Element um eine halbe Höhe nach unten verschoben wird. 100% => ganze Höhe, 200% => 2 Höhen, ...

## ch
- *Number of characters (1 character is equal to the width of the current font's 0/zero)*

## ex
- *Relative to height of the current font's lowercase "x"*

## em
- *relative to the closest element that has font-size set, by dev or browser default (e.g. h1). It can be self, parent or any ancestor, up to root.*

## rem
- 1rem = 16px

## vw, vh
- 1vh = 1% of viewport width (not browser width)
