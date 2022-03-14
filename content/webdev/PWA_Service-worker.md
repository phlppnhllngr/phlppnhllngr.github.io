---
tags: [Notebooks/Webdev]
title: 'PWA, Service worker'
created: '2019-04-20T10:24:05.743Z'
modified: '2020-08-24T12:13:39.810Z'
parent: Webdev
---

# PWA, Service worker

## Service worker
- <https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers>
- <https://developers.google.com/web/fundamentals/primers/service-workers/>
- <https://www.reddit.com/r/javascript/comments/ek4811/how_to_fix_the_refresh_button_when_using_service/>
- <https://fullstack-developer.academy/progressive-web-applications-free-handbook/> [31.5.18]
- 'Google Chrome Developers'-Youtube-Kanal
- serviceworke.rs
  - <https://serviceworke.rs/>
  - The Service Worker Cookbook
- <https://ultimatecourses.com/blog/ultimate-guide-pwa-workbox>
- Requests von ES6-Imports unterscheiden sich von fetch-Requests. Wenn also ein JS-Modul vom SW statisch gecached wurde (z.B. `cache.addAll`),
dann wird ein abgefangenes ES6-import-fetch-Event bei `cache.match(event.request)` nicht zu einem Cache-Treffer führen. (<https://medium.com/@filipbech/the-gotchas-of-caching-es-modules-f92c9429fe26>) 


### Libs
- **workbox**
  - <https://developers.google.com/web/tools/workbox/>
  - <https://github.com/GoogleChrome/workbox> *8.8k


## PWA  
- **pwa**
  - *(WIP) Universal PWA Builder*
  - <https://github.com/lukeed/pwa> (inaktiv seit 05/2020)
- **pwabuilder.com**
  - <https://www.pwabuilder.com/>
  - *Quickly and easily turn your website into an app! It's super easy to get started. Just enter the URL of your website below / Already have a PWA?: Expert mode*
