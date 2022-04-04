---
tags: [Notebooks/Javascript]
title: Libs
created: '2019-02-20T20:30:57.120Z'
modified: '2021-08-15T12:34:38.061Z'
parent: JavaScript
---

# Libs
UI → UI Libs

## node_modules-Verzeichnisse, best-ofs
- <https://www.npmjs.com/>
- <https://bestof.js.org/>
- <https://www.javascripting.com/>
- <https://hitup.wondertools.top/#/>
- <https://tooling.js.org/>
- <https://www.webcomponents.org/>
- <https://moiva.io/> (compare libs)


## Diverse
- **rxjs**
    - <https://github.com/ReactiveX/rxjs>
    - <https://github.com/btroncone/learn-rxjs>
    - <https://github.com/xripcsu/rxjs-watcher>
    - <https://rxmarbles.com/> - *Interactive diagrams of Rx Observables*
    - <https://medium.com/angular-in-depth/rx-js-best-practices-6a3b095ffb04>
- <https://github.com/mgechev/aspect.js>
- <https://immutable-js.github.io/immutable-js/> - *Immutable collections for JavaScript*
- <https://github.com/lukeed/dequal> - *A tiny (247B) utility to check for deep equality*
- <https://github.com/messageformat/messageformat>
- <https://github.com/wsmd/reattempt>
- **sugarjs**
  - <https://sugarjs.com/>
  - utility lib (date, array, number)
- [lodash / lodash-es / lodash/fp](https://lodash.com/)
  - <https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore>
  - <https://springload.github.io/lodash-function-finder/> (man gibt den Input und den gewünschten Output an)
  - <https://github.com/lodash/lodash/wiki/FP-Guide>
- <u>EventBus</u>
  - <https://www.npmjs.com/package/js-event-bus>
  - <https://www.npmjs.com/package/simple-events-bus>
- **p-event**
  - <https://github.com/sindresorhus/p-event>
  - promisify events
  - ```await pEvent(document, 'DOMContentLoaded')```
- **uid**
  - <https://github.com/lukeed/uid>
  - *A tiny (134B) and fast utility to generate random IDs of fixed length*
- **heapify**
  - <https://github.com/luciopaiva/heapify>
  - priority queue
- **class-transformer**
  - <https://github.com/typestack/class-transformer>
  - *Proper decorator-based transformation / serialization / deserialization of plain javascript objects to class constructors*
- **super-expressive**
  - <https://github.com/francisrstokes/super-expressive>
  - *build regular expressions in almost natural language*
- **json-rules-engine**
  - <https://github.com/CacheControl/json-rules-engine>


## User input
→ JavaScript/User input


## State management & persistence
- **immer**
  - <https://github.com/mweststrate/immer>
- **rxdeep**
  - *provides fast and precise reactive state management*
  - <https://loreanvictor.github.io/rxdeep/> *42
- **rxdb**
  - *A realtime Database for JavaScript Applications*
  - *you can not only query the current state, but subscribe to all state changes like the result of a query or even a single field of a document. This is great for UI-based realtime applications in way that makes it easy to develop and also has great performance benefits*
  - <https://github.com/pubkey/rxdb>
- **sqljs**
  - *run SQLite on the web*
  - <https://github.com/sql-js/sql.js>
- **localforage**
  - *Wraps IndexedDB, WebSQL, or localStorage using a simple but powerful API*
  - <https://github.com/localForage/localForage> *19.3k
- **PouchDB**
  - *store data locally while offline, then synchronize it with CouchDB and compatible servers when the application is back online*
  - <https://github.com/pouchdb/pouchdb> *14.3k
- **Jsynchronous**
  - *Data synchronization for games and real-time web apps*
  - *Create an array or object in Node.js. Jsynchronous will create an identical variable in connected browsers. Changes to that variable will be automatically communicated to the browser so that they always stay in-sync.*
  - <https://github.com/siriusastrebe/jsynchronous/> *26
- **xstate**
  - *finite state machines and statecharts*
  - <https://github.com/statelyai/xstate>


## Polyfills
- <https://github.com/Modernizr/Modernizr/> / <https://modernizr.com/>
- <https://github.com/zloirock/core-js>
- <https://jasonformat.com/modern-script-loading/> (module/nomodule)
- **polyfill.io**
  - <https://polyfill.io/v3/>
  - *service which accepts a request for a set of browser features and returns only the polyfills that are needed by the requesting browser*
  - e.g. `https://polyfill.io/v3/polyfill.min.js?features=es2018%2CAbortController%2CIntl.RelativeTimeFormat.%7Elocale.de` 


## PDF
- siehe auch 
  - <https://developer.mozilla.org/en-US/docs/Web/Guide/Printing>
  - @media print
- **jsPDF**
  - <https://github.com/MrRio/jsPDF> ⭐16.000
  - <https://parall.ax/products/jspdf> 
  - Client-side JavaScript <mark>PDF generation</mark>
  - Plugins
    - <https://github.com/simonbengtsson/jsPDF-AutoTable>
- **PDFKit**
  - <https://github.com/foliojs/pdfkit> ⭐4.500
  - <mark>PDF generation</mark> library for Node and the browser
- **PDFMake**
  - <http://pdfmake.org>
  - <https://github.com/bpampuch/pdfmake> ⭐7.000
  - based on pdfkit
- **pdf-lib**
  - *Create and modify PDF documents in any JavaScript environment.*
  - *other PDF libraries can only create documents, they cannot <mark>modify existing</mark> ones*
  - <https://github.com/Hopding/pdf-lib> ⭐3.8k
- **hummus**
  - <https://github.com/galkahana/HummusJS> ⭐500
  - *Node.js module for high performance <mark>creation, modification and parsing</mark> of PDF files and streams*
- **pdfassembler**
  - <https://github.com/DevelopingMagic/pdfassembler> ⭐164
  - (5.7.19: inaktiv)
  - Browser✅ node❌
  - *PDF Assembler <mark>disassembles PDF files into editable JavaScript objects</mark>, then assembles them back into PDF files. If you want a simple way to edit existing PDFs in a browser, try pdf-lib. PDF Assembler offers more direct control over the PDF structure than pdf-lib. This allows you to do more complex editing (essentially anything you can do to a PDF, you can do with PDF Assembler), but it also requires you to have a good understanding of how the logical structure of a PDF works.*
- **PDFNetJS** 💰
  - <https://www.pdftron.com/blog/webviewer/pdfnetjs-html5-pdf-viewer-and-editor/>
  - *Complete Browser-Side <mark>PDF Viewer and Editor</mark>*
  - *In contrast with pdf.js, it offers correct rendering and a wide variety of PDF creation/modification APIs.*
- **pdf.js**
  - <https://mozilla.github.io/pdf.js/>
  - <https://github.com/mozilla/pdf.js> ⭐25.500
  - <mark>parsing and rendering PDFs</mark>
- **pdfform**
  - <https://github.com/phihag/pdfform.js> ⭐65
  - *<mark>Fill out PDF forms</mark> in pure JavaScript*
  - Browser✅ node✅
  - 25.1.20: inaktiv seit 9 Monaten
- **html2pdf**
  - <https://github.com/eKoopmans/html2pdf.js> ⭐1.1k
  - wrappt html2canvas und jsPDF
- **pspdfkit** 💰
  - <https://pspdfkit.com/>
  - *features like annotating, signing, and form filling*
  - <mark>pdf viewer & editor</mark>
- **paged.js**
  - <https://www.pagedjs.org/documentation/>
  - *If you use Paged.js, you’ll be able to see in your browser a preview of how your styles will appear when printing.*
  - tutorial: <https://pdf.math.dev/>
- <https://www.smashingmagazine.com/2019/06/create-pdf-web-application/>



## Http-Client
- window.fetch
- <https://github.com/elbywan/wretch>
- **axios**
  - <https://github.com/axios/axios> *67.5k
  - Browser & Node
- **redaxios**
  - <https://github.com/developit/redaxios> *900
  - *The Axios API, as an 800 byte Fetch wrapper.*
- **apisauce**  
  - <https://github.com/infinitered/apisauce>
  - *Axios + standardized errors + request/response transforms.*
- <https://github.com/sindresorhus/got> (node)
- <https://github.com/sindresorhus/ky> (browser)
- **node-fetch**
