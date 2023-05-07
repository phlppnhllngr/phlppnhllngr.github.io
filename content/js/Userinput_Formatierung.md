---
title: Userinput & Formatierung
parent: JavaScript
---

# Userinput & Formatierung
- [HTML - Inputs](@note/Inputs.md)
- <https://htmldom.dev>


## Verschiedene
- **window.Intl**
  - <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl>
  - *Creating instances of these Intl formats is an expensive operation, and the APIs are designed such that developers should re-use format instances instead of always creating new ones.*
  - *The API provides automatic localization of:
    dates and times
    relative periods such as yesterday and tomorrow
    numbers including currencies, percentages, and units
    names of languages, regions, scripts, and currencies
    lists with conjunctions (and) and disjunctions (or)
    plural helpers
    string comparisons, such as equating a with á*
- **formatjs**
  - <https://github.com/formatjs/formatjs> ⭐12k
  - Browser & Node
  - Dates, Numbers, Pluralisation
  - Polyfills für window.Intl


## Datum
- **Date**
  - <https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date>
  - [toLocaleString](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString)
    - `date.toISOString()` // 08.09.2021, 14:44 -> 2021-09-08T<mark>12:46:07</mark>.274Z; toISOString() beachtet User-Zeitzone nicht
    - `date.toLocaleString('de')` // 8.9.2021, <mark>14:46:07</mark>; beachtet User-Zeitzone
  - [toLocaleDateString](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleDateString)
    - `date.toLocaleDateString('de')` // 08.09.21 -> 8.9.2021
    - `date.toLocaleDateString('sv')` // 2021-09-08; Schweden hat ISO-8601
  - [toLocaleTimeString](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleTimeString)
- **Temporal**
  - *This proposes Temporal, a global Object that acts as a top-level namespace (like Math), that brings a modern date/time API to the ECMAScript language.*
  - <https://caniuse.com/temporal> (Stand 11.7.21 kein Browser support)
  - Polyfill: <https://www.npmjs.com/package/@js-temporal/polyfill>
  - <https://2ality.com/2021/06/temporal-api.html>
- <u>Intl</u>
  - **DateTimeFormat**
    - <https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat>
    - <https://beta.caniuse.com/?search=datetimeformat>

      ```js
      // format
      const date = new Date(); // 7.2.2020
      new Intl.DateTimeFormat('de-DE', {
        month: 'long',
        year: 'numeric',
        day: '2-digit'
      }).format(date); // "07. Februar 2020"
      
      // Uhrzeit hh:mm
      new Intl.DateTimeFormat('de-DE', { hour: 'numeric', minute: 'numeric', hour12: false });

      // formatToParts
      const date = new Date(); // 7.2.2020
      new Intl.DateTimeFormat('de-DE', {
        month: 'long',
        year: 'numeric',
        day: '2-digit'
      }).format(date)[2]; // { type: 'month', value: 'Februar' }
      ```

  - **RelativeTimeFormat**
    - <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RelativeTimeFormat>
    - <https://beta.caniuse.com/?search=relativetimeformat>
    ```js
    const rtf = new Intl.RelativeTimeFormat('en', { style: 'narrow' });
    rtf.format(-1, 'day'); // "1 day ago"
    ```
- **moment**
  - deprecated, Nachfolger: Luxon
  - <https://momentjs.com>
  - <https://github.com/you-dont-need/You-Dont-Need-Momentjs>
    - Recipes für Browser-APIs statt moment
    - mit Gegenüberstellung diverser Libs
    - *you can install a [ESLint] plugin that will help you identify places in your codebase where you don't (may not) need Moment.js*
- **Luxon**
  - <https://github.com/moment/luxon>
  - *DateTime, Duration, and Interval types. Parsing and formatting for common and custom formats.*
- **dayjs**
  - <https://github.com/xx45/dayjs>
- **date-fns**
  - <https://github.com/date-fns/date-fns>


## Eingabefeld-Formatierung
- **imaskjs**
  - kann auch nur JS-API zum Formatieren benutzen, ohne HTML (siehe [pipe](https://imask.js.org/guide.html#pipe))
  - <https://unmanner.github.io/imaskjs> ⭐2.5k
- **text-mask**
  - *Input mask for React, Angular, Ember, Vue, & plain JavaScript*
  - undmaintained und verweist auf imask
  - <https://github.com/text-mask/text-mask> ⭐7.9k
- **cleave**
  - <https://nosir.github.io/cleave.js>
- **Inputmask**
  - <https://github.com/RobinHerbots/Inputmask> ⭐5.2k


## Zahlen
- `const n = 12.30; console.log(n); // 12.3!`
- <u>Web-APIs</u>
  - **Intl.NumberFormat**
    - <https://v8.dev/features/intl-numberformat>
    - <https://beta.caniuse.com/?search=numberformat>
    - styles: currency, unit, ...
    - units: percent, byte, durations, mass, temperature, volume, ...
    - display value with '+' or '-'
  - **Number.prototype**
    - toLocaleString(locale, options)
      - options
        - notation
        - compactDisplay
          ```js
          { notation: 'compact', compactDisplay: 'long' } // 123456789 => "123 Millionen"
          { notation: 'compact', compactDisplay: 'short' } // 123456789 => "123 Mio."
          ```
        - style
          - currency
          - percent
            ```js
            { style: 'percent', minimumFractionDigits: 2 } // 0.1234 => "12.34 %"
            ```
          - decimal
        - `minimumFractionDigits` und `maximumFractionDigits` dürfen sich nicht widersprechen, sonst error ('value is out of range')
        - <https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString>
    - toFixed
  - Intl.NumberFormat ist bei großer Anzahl an (gleichen) Formatierungen `toLocaleString` vorzuziehen. Die/eine Formatter-Instanz sollte wiederverwendet werden.
  - **BigInt**
    - <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt>
- **numeraljs**
  - <http://numeraljs.com>
- **numbrojs**
  - <http://numbrojs.com>
- **autoNumeric**
  - <http://autonumeric.org>
  - <https://github.com/autoNumeric/autoNumeric> ⭐1300
  - vue-autonumeric
- **dinero**
  - *Create, calculate, and format money*
  - <https://github.com/dinerojs/dinero.js> ⭐4.6k


## Strings
- **Intl.Collator**
  - <https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Collator>
  - <https://beta.caniuse.com/?search=collator>
  - kann z.B. sprachspezifisch sortieren
  ```js
  console.log(Intl.Collator.supportedLocalesOf(['de-DE'], { localeMatcher: 'lookup' }));
  function letterSort(lang, letters) {
      letters.sort(new Intl.Collator(lang).compare);
      return letters;
  }
  console.log(letterSort('de', ['a','z','ä']));
  // expected output: Array ["a", "ä", "z"]
  ```
- **Intl.ListFormat**
  - *language-sensitive list formatting*
  - <https://beta.caniuse.com/?search=listformat>
  - <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/ListFormat>
  ```js
  const vehicles = ['Bus', 'Auto'];
  const formatter = new Intl.ListFormat('de', { style: 'short', type: 'disjunction' });
  formatter.format(vehicles); // "Bus oder Auto"
  ```
- **Intl.PluralRules**
  - <https://caniuse.com/#search=pluralrules>
  ```js
  console.log(Intl.PluralRules.supportedLocalesOf(['de-DE'], { localeMatcher: 'lookup' }));
  const plural = new Intl.PluralRules('de-DE');
  console.log(
      plural.select(0),
      plural.select(1),
      plural.select(2),
      plural.select(6),
      plural.select(18),
  )
  ```


## Validierung

### Email
- **mailcheck**
  - <https://github.com/mailcheck/mailcheck>
  - Checkt Email-Eingaben und macht Verbesserungsvorschläge (hotnail.con -> hotmail.com)

### Telefon
- **libphonenumber**
  - <https://github.com/google/libphonenumber>
- **intl-tel-input**
  - <https://github.com/jackocnr/intl-tel-input> *5.7k
  - *entering and validating international telephone numbers*
  - *It adds a flag dropdown to any input, detects the user's country, displays a relevant placeholder and provides formatting/validation methods.*

### Komplex/Gemischt
- <https://validatejs.org/>
- <https://www.npmjs.com/package/validator> (nur Strings; Farben, Zahlen, Email, ...)
- **joi**
  - *schema validation*
  - <https://github.com/hapijs/joi> ⭐15.9k
  - diverse Extensions
  - Codepen: `import 'https://unpkg.com/joi@17.2.1/dist/joi-browser.min.js?module'; window.joi`
- <https://github.com/oussamahamdaoui/forgJs>
- <https://github.com/flexdinesh/typy>
- <https://github.com/sindresorhus/ow>
- <https://github.com/imbrn/v8n>
- <https://github.com/jquense/yup> ⭐5800 - browser & server
- **objectmodel**
  - <https://objectmodel.js.org/>
- <https://github.com/validatorjs/validator.js>


## Key binds
- **Hotkey**
  - <https://github.com/github/hotkey> ⭐1400
- **Hotkeys**
  - <https://github.com/jaywcjlove/hotkeys> ⭐3300
- **tinykeys**
  - <https://github.com/jamiebuilds/tinykeys>
  - *~400 B*
- **Kontextmenü**
  - <https://mionskowski.pl/positioning-a-context-menu-using-pure-css>


## Autocomplete
- **autoComplete.js**
  - *Simple autocomplete pure vanilla Javascript library*
  - <https://github.com/TarekRaafat/autoComplete.js>
