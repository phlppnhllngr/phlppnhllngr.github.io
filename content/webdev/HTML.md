---
tags: [Notebooks, Notebooks/HTML]
title: HTML
created: '2019-02-14T20:08:49.949Z'
modified: '2020-09-19T13:40:01.327Z'
parent: Webdev
---

# HTML
- **ct.css**
  - *Your `<head>` is the single biggest render-blocking part of your page—ensuring it is well-formed is critical. ct.css is a diagnostic CSS snippet that exposes potential performance issues in your page’s `<head>` tags.*
  - <https://csswizardry.com/ct/>


## Preprocessors
- **pug**
  - <https://github.com/pugjs/pug>
- **haml**
  - <https://haml.info/>


## Zeichen & Entitäten
- **soft hyphen**
  - `&shy;`
  - Stelle, an der getrennt werden darf, falls das Wort bei der Bildschirmanzeige am Ende der Zeile steht und der Platz für eine vollständige Darstellung nicht mehr ausreicht. Der Browser sollte das Wort an dieser Stelle mit einem Umbruch trennen und einen Trennstrich einfügen.
- **hypen**
  - `&hyphen;`
- **zero-width space**
  - `&#8203;`
- **non-breaking space**
  - `&nbsp;`
  - verhindert einen automatischen Zeilenumbruch an der Position des Leerzeichens, der die Leserlichkeit verschlechtern und den Lesefluss stören könnte


## Tags
- <https://developer.mozilla.org/en-US/docs/Web/HTML/Element>
- (semantisch) wichtige
  - main
    - *represents the dominant content of the <body> of a document.*
  - header
    - *represents introductory content, typically a group of introductory or navigational aids. It may contain some heading elements but also a logo, a search form, an author name, and other elements*
  - footer
  - aside
    - *represents a portion of a document whose content is only indirectly related to the document's main content*
  - address
  - nav
  - section
    - *represents a standalone section — which doesn't have a more specific semantic element to represent it*
  - hgroup
    - <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hgroup>
    - represents a multi-level heading for a section of a document. It groups a set of h1–h6 elements
  - form & related
    - form
      - <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form>
      - Http-Request verhindern mit `onsubmit="event.preventDefault();"`
      - <https://thecodeangle.com/a-detailed-breakdown-of-html-form-event-attributes/>
    - fieldset
      - used to group several controls as well as labels within a web form
    - input -> HTML/Inputs
    - label
    - output
      - (of calculation)
      - <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/output>
        ```
          <form oninput="...">
            <input id="a" name="a"/>
            <span>+</span>
            <input id="b" name="b"/>
            <span>=</span>
            <output for="a b"></output>
          </form>
        ```
  - img
    - loading (eager/lazy)
      - <https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/loading>
    - decoding (sync/async)
      - <https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/decoding>
    - -> picture
- andere
  - picture
    - srcset: wann welches Bild geladen wird
      - <https://www.mediaevent.de/html/srcset.html>
    - sizes: wann welches Bild angezeigt wird
  - progress --> <progress value="70" max="100">70 %</progress>
  - meter -->
    ```html
    <meter id="fuel1" min="0" max="100" low="33" high="66" optimum="80" value="24">at 24/100</meter>
    <meter id="fuel2" min="0" max="100" low="33" high="66" optimum="80" value="50">at 50/100</meter>
    <meter id="fuel3" min="0" max="100" low="33" high="66" optimum="80" value="70">at 70/100</meter>
    <meter id="fuel4" min="0" max="100" low="33" high="66" optimum="80" value="80">at 80/100</meter>
    ```
  - details & summary
    - verhalten sich in etwa so wie ein accordion
  - datalist
  - dialog
    - <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog>
    - ein Dialog-Fenster mit Methoden show, showModal und close
    - `<form>` innerhalb `<dialog>` unterstützt den `method`-Attributwert `dialog` was bewirkt, dass der Dialog bei submit geschlossen wird
  - mark --> <mark>test</mark>
  - abbr --> <abbr title='National Space Agency'>NASA</abbr>
    - <https://modernweb.com/enhancing-the-html-abbr-element-on-mobile/>
  - menu
    - schlechter Browser-Support
    - ~~menuitem~~ deprecated
  - small
    - represents side-comments and small print, like copyright and legal text
  - strong
    - contents have strong importance, seriousness, or urgency
  - em
  - q
    - enclosed text is a short inline quotation
    - Zeichen kann geändert werden mit CSS-quotes-Attribut
  - time
    - <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/time>
    - It may represent one of the following: A time on a 24-hour clock.A precise date in the Gregorian calendar (with optional time and   timezone information). A valid time duration.
  - wbr
    - represents a word break opportunity—a position within text where the browser may optionally break a line, though its line-breaking rules would not otherwise create a break at that location
  - map
    - *defines an image map. An image map is an image with clickable areas*


## Head
- <https://htmlhead.dev/> - *A free guide to HTML5 `<head>` elements*
- <https://github.com/joshbuchea/HEAD>

### Meta
- <https://wiki.selfhtml.org/wiki/HTML/Kopfdaten/meta>
- <https://metatags.io/>
- open graph
  - für twitter, fb, ... embeds
  - <https://ogp.me/>
- color-scheme

### PWA
- <https://developer.mozilla.org/de/docs/Web/Manifest>
```html
<link rel="manifest" href="manifest.json"/>
```

- <https://goo.gl/qRE0vM>
```html
<meta name="theme-color" content="#269AD1">
```

*Add to homescreen for Chrome on Android. Fallback for manifest.json*
```html
<meta name="mobile-web-app-capable" content="yes">
<meta name="application-name" content="xyz">
```

*Add to homescreen for Safari on iOS*
```html
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="xyz">
```

*Homescreen icons*
```html
<link rel="apple-touch-icon" sizes="32x32" href="images/manifest/icon-32x32.png">
<link rel="apple-touch-icon" href="images/manifest/icon-48x48.png">
<link rel="apple-touch-icon" sizes="72x72" href="images/manifest/icon-72x72.png">
<link rel="apple-touch-icon" sizes="96x96" href="images/manifest/icon-96x96.png">
<link rel="apple-touch-icon" sizes="144x144" href="images/manifest/icon-144x144.png">
<link rel="apple-touch-icon" sizes="192x192" href="images/manifest/icon-192x192.png">
<link rel="apple-touch-icon" sizes="192x192" href="images/manifest/icon-512x512.png">
```

*Tile icon for Windows 8 (144x144 + tile color)*
```html
<meta name="msapplication-TileImage" content="images/manifest/icon-144x144.png">
<meta name="msapplication-TileColor" content="#00b4f0">
<meta name="msapplication-tap-highlight" content="no">
```
