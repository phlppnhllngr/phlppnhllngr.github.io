---
tags: [Notebooks/Javascript]
title: neuere Web APIs
created: '2019-04-07T14:22:18.871Z'
modified: '2021-09-02T10:10:33.363Z'
parent: JavaScript
---

# neuere Web APIs
- <https://www.chromestatus.com/features>
- <https://github.com/luruke/browser-2020>
- <https://fugu-tracker.web.app/>
- <https://whatwebcando.today/><br/>
- **(Web) Worker**
  - <https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers>
- **background sync**
  - <https://developers.google.com/web/updates/2015/12/background-sync>
  - <https://developers.google.com/web/tools/workbox/modules/workbox-background-sync>
  - *lets you defer actions until the user has stable connectivity*
- **background fetch**
  - *like background sync, for larger data*
- **web authn**
- **badging api (pwa)**
- **import maps & built-in modules**
  - <https://github.com/WICG/import-maps>
- ```<img loading="lazy"/>```
- **web share, share target**
- **shape detection (face, qr, barcode, text)**
- **matchMedia**
  - addListener, onchange
  - `window.matchMedia('(prefers-color-scheme: dark)').matches // true / false`
  - *use this over window.onresize events*
- **page visibility**
- **navigator.onLine**
  - `window.addEL('online' / 'offline' , e => ...)`
- **navigator.connection**
- **window.caches**
- **fullscreen**
- **async clipboard**
- **Image Capture API**
  - setzt auf navigator.mediaDevices.getUserMedia auf
  - <https://developer.mozilla.org/en-US/docs/Web/API/ImageCapture>
- **file system access**
  - <https://fjolt.com/article/javascript-new-file-system-api>
  - <https://web.dev/file-system-access/>
- **idle detection**
  - <https://web.dev/idle-detection/>
