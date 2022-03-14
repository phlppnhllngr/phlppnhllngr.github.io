---
tags: [Notebooks/CSS]
title: '@media'
created: '2020-02-01T19:46:14.725Z'
modified: '2021-05-18T08:04:01.029Z'
parent: CSS
---

# @media
- <https://css-tricks.com/a-complete-guide-to-css-media-queries/>
- <https://developer.mozilla.org/en-US/docs/Web/CSS/@media>


## Diverses
- man kann verschiedene Stylesheets je nach media angeben
  ```html
  <link rel="stylesheet" media="screen and (min-width: 900px)" href="widescreen.css">
  <link rel="stylesheet" media="screen and (max-width: 600px)" href="smallscreen.css">
  <link rel="stylesheet" href="dark.css" media="(prefers-color-scheme: dark)">
  <link rel="stylesheet" href="light.css" media="(prefers-color-scheme: no-preference), (prefers-color-scheme: light)">
  <link media="print" ...>
  ```


## Breakpoints
- <https://www.reddit.com/r/css/comments/hrkoh7/css_breakpoints_used_by_popular_css_frameworks/>
- Bootstrap
  - <https://getbootstrap.com/docs/4.0/layout/overview/#responsive-breakpoints>
  - xs <  576px ~ handy portrait
  - sm >= 576px ~ handy landscape
  - md >= 768px ~ tablet portrait
  - lg >= 992px ~ tablet landscape
  - xl >= 1200px ~ monitor
- devices (css width & height)
  - <https://viewportsizer.com/devices/>
  - phones
    - iphone x (375x812)
    - iphone 6/7/8 plus (414x736)
    - pixel 2 (414x731)
    - pixel 2 xl (411x823)
    - galaxy 5 (360x640)
    - iphone 6/7/8 plus (736x414, landscape)
  - tablets
    - ipad (768x1024)
    - iphone x (812x375, landscape)
    - ipad (1024x768, landscape)
    - ipad pro (1024x1366)
  - larger screens
    - pc monitor
    - laptop
    - ipad pro (1366x1024, landscape)


## User-Präferenzen
- **prefers-reduced-motion**
  - *detect if the user has requested that the system minimize the amount of non-essential motion it uses*
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion>
- **prefers-color-scheme**
  - ob dark- oder light-theme oder nichts bevorzugt
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme>
- **scripting**
  - *can be used to test whether scripting (such as JavaScript) is available*
  - 03/22 kein Browser-Support
  - <https://developer.mozilla.org/en-US/docs/Web/CSS/@media/scripting>


## Input
- **any-hover**
  - none: primary input cannot hover
- **any-pointer**
  - fine: mouse
  - coarse: input device with limited accuracy (e.g. touch screen)
  ```css
  @media (any-pointer: fine) { }
  @media (any-pointer: coarse) { }
  ```
- width: The viewport width
- max-width: maximum width of the display area, such as a browser window
- ...
