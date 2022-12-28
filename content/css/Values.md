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
  - -> CSS/Funktionen
  - fit-content, min, max, minmax, clamp, ...
