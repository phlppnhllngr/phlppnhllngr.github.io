---
tags: [Notebooks/Javascript]
title: Angular
created: '2019-02-20T15:43:47.656Z'
modified: '2020-12-16T13:48:27.520Z'
parent: JavaScript
---

# Angular

<style>
  details a:after {
    content: attr(href);
  }
</style>
<details>
  <summary>Artikel</summary>
  <ul>
    <li><a href="https://videos.ng-conf.org/videos/"></a></li>
    <li><a href="https://blog.angularindepth.com/top-10-ways-to-use-interceptors-in-angular-db450f8a62d6"></a></li>
    <li><a href="https://www.reddit.com/r/Angular2/comments/da16uo/template_syntax_expressions_statements_cheat_sheet/"></a></li>
    <li><a href="https://www.reddit.com/r/Angular2/comments/i3in0o/rxjs_angular_unsubscribe_like_a_pro/.compact"></a></li>
    <li><a href="https://blog.angularindepth.com/angular-question-rxjs-subscribe-vs-async-pipe-in-component-templates-c956c8c0c794"></a></li>
    <li><a href="https://blog.angularindepth.com/angular-show-loading-indicator-when-obs-async-is-not-yet-resolved-9d8e5497dd8"></a></li>
    <li><a href="https://jasonwatmore.com/post/2019/06/10/angular-8-user-registration-and-login-example-tutorial"></a></li>
    <li><a href="https://indepth.dev/component-features-with-angular-ivy/"></a></li>
    <li><a href="https://indepth.dev/a-thorough-exploration-of-angular-forms/"></a></li>
    <li><a href="https://www.dunebook.com/angular-opensource-projects/"></a></li>
    <li><a href="https://itnext.io/understanding-angular-modules-5f1215130bc8?sk=78c24f6ed62486fe5bb91ce1d14667b7"></a></li>
    <li><a href="https://indepth.dev/supercharge-event-management-in-your-angular-application/"></a></li>
    <li><a href="https://medium.com/better-programming/let-angular-manage-your-rxjs-subscriptions-better-9243073e94b0"></a></li>
    <li><a href="https://malcoded.com/posts/angular-best-of-2019/"></a></li>
    <li><a href="https://indepth.dev/top-15-angular-indepth-articles-of-2019/"></a></li>
    <li><a href="https://medium.com/bb-tutorials-and-thoughts/how-to-maintain-all-the-messages-in-one-place-in-angular-33db8348f804"></a></li>
    <li><a href="https://netbasal.com/give-your-modals-url-address-with-auxiliary-routes-in-angular-eb76497c0bca"></a></li>
    <li><a href="https://netbasal.com/effortless-web-storage-persistence-in-angular-forms-cfa81ad23e30"></a></li>
    <li><a href="https://blog.bitsrc.io/lazy-loading-auxiliary-routes-with-angular-why-and-how-9ceb2ddc6cae"></a></li>
    <li><a href="https://blog.w3radar.com/less-known-angular-features-probably-never-used/"></a></li>
    <li><a href="https://www.mokkapps.de/blog/the-last-guide-for-angular-change-detection-you-will-ever-need/"></a></li>
    <li><a href="https://blog.eyas.sh/2020/05/better-loading-and-error-handling-in-angular/"></a></li>
    <li><a href="https://auth0.com/blog/angular-9s-best-hidden-feature-strict-template-checking/"></a></li>
    <li><a href="https://sebastian-holstein.de/post/error-handling-angular-async-pipe/"></a></li>
    <li><a href="https://www.reddit.com/r/Angular2/comments/iql4k3/checklist_for_creating_complex_angular/"></a></li>
  </ul>
</details>


## scaffolding
- **jhipster**
- https://github.com/DanWahlin/Angular-JumpStart
- cli / ng new
- https://github.com/ngx-rocket/generator-ngx-rocket


## state management
- <https://www.reddit.com/r/angular/comments/j9xk4o/here_i_have_aggregated_all_7_ways_to_share_data/>
- **rxjs only**
  - https://dev.to/avatsaev/simple-state-management-in-angular-with-only-services-and-rxjs-41p8
- **ngxs**
  - https://ngxs.gitbook.io/ngxs
  - https://github.com/ngxs/store
- **ngrx**
  - https://ngrx.io/
  - https://github.com/ngrx/platform
- **akita**
  - https://github.com/datorama/akita
  - *Angular, React, Vue, Web Components or plain old vanilla JS*


## Test
- ~~Protractor~~
  - http://www.protractortest.org/#/
  - kaum Dokumentation zu Angular 2+, cypress wohl die bessere Alternative
- **testing-library**
  - https://testing-library.com/docs/angular-testing-library/intro
- **ngneat/speactator**
  - https://github.com/ngneat/spectator *550
  - *It allows you to write tests for components, directives, services, and more, without having to learn TestBed, ComponentFixture, and DebugElement APIs.*

### Mock, Stub
- **in-memory-web-api**
  - https://github.com/angular/in-memory-web-api *1000
  - *It intercepts Angular Http and HttpClient requests that would otherwise go to the remote server and redirects them to an in-memory data store that you control*
- **ng-mocks**
  - https://github.com/ike18t/ng-mocks
  - *Angular 5+ component, directive, and pipe mocking library*


## UI Frameworks
- **primeng**
  - https://www.primefaces.org/primeng/#/
  - https://github.com/primefaces/primeng *5.7k
  - *80+ Components*
- **ng-bootstrap**
  - https://ng-bootstrap.github.io/#/home
  - https://github.com/ng-bootstrap/ng-bootstrap *7.3k
- **ngx-bootstrap**
  - https://ngx-bootstrap.surge.sh/#/
  - https://github.com/valor-software/ngx-bootstrap *5k
- https://material.angular.io/
- https://github.com/angular/material2
- https://github.com/edcarroll/ng2-semantic-ui
- https://github.com/angular/flex-layout
- **onsen ui**
  - https://onsen.io/v2/guide/angular2/
  - https://github.com/OnsenUI/OnsenUI *7.8k (alle frameworks)
- **ng-zorro-antd**
  - https://github.com/NG-ZORRO/ng-zorro-antd *6k
- **element**
  - https://element-angular.faas.ele.me
  - https://github.com/ElemeFE/element-angular *450
  - doku teils nur chinesisch
  - 18.1.20: letzter commit 18.6.18
- **amexio**
  - https://github.com/meta-magic/amexio.github.io *170
  - *(170+) components*
- **ignite-ui**
  - https://www.infragistics.com/products/ignite-ui-angular
  - paid
- **clarity**
  - https://github.com/vmware/clarity
- **Ionic/Angular**
  - https://github.com/ionic-team/ionic *40k (alle frameworks)
- **nebular**
  - https://github.com/akveo/nebular *5.8k
  - *35+ Angular UI components*


## Libs
- https://github.com/ngneat
  - ngneat/from-event
    - https://github.com/ngneat/from-event
    ```js
    template: `<button #button></button>`
    @FromEvent('click')
    @ViewChild('button') 
    click$: Observable<MouseEvent>;
    ```
  - https://github.com/ngneat/until-destroy
- https://www.npmjs.com/package/ngx-webstorage
- <u>electron</u>
  - https://github.com/ThorstenHans/ngx-electron
  - https://github.com/maximegris/angular-electron
    - *Ultra-fast bootstrapping with Angular and Electron*
- https://github.com/2muchcoffeecom/ngx-restangular
- https://github.com/swimlane/ngx-charts
- https://github.com/ng-turkey/ngx-context
  - *Easy property binding for router outlet and nested component trees*
  - letzter commit 07/2019 (03/2020)
- **rx-angular**
  - *Reactive Extensions for Angular*
  - https://github.com/rx-angular/rx-angular
- **i18n**
  - https://github.com/ngneat/transloco (i18n)
  - https://github.com/rxweb/rxweb/tree/master/packages/translate (i18n)
- https://www.npmjs.com/package/@ngspot/ngx-errors
- https://github.com/ngneat/error-tailor

### Forms
- **ngx-sub-forms**
  - https://github.com/cloudnc/ngx-sub-form
  - *Utility library for breaking down an Angular form into multiple components*
- https://github.com/ng-select/ng-select
- https://www.npmjs.com/package/ngx-mask
- https://github.com/formly-js/ngx-formly
- https://github.com/ngneat/forms-manager
- https://www.npmjs.com/package/@rxweb/reactive-form-validators


## Devtools, Build
- window.ng (Angular 9+)
  - probe($0).componentInstance
- **Augury**
  - https://augury.angular.io/
  - https://github.com/rangle/augury
- **CLI**
  - https://github.com/angular/angular-cli
  - <u>Tooling</u>
    - ngx-build-plus
      - https://www.npmjs.com/package/ngx-build-plus
      - *Extend the Angular CLI's default build behavior without ejecting*
    - angularconsole
      - https://angularconsole.com/
      - 3rd party gui
- **compodoc**
  - https://github.com/compodoc/compodoc
- **codelyzer**
  - https://github.com/mgechev/codelyzer
  - Linter
- **angular-eslint**
  - https://github.com/angular-eslint/angular-eslint
- **storybook**
  - test components in isolation
  - https://alligator.io/angular/storybook-angular/
  - https://storybook.js.org/docs/guides/guide-angular
  - → javascript/diverse entwicklungstools
- **ng-run**
  - https://ng-run.com/
  - Online-Code-Editor
- **ng-bubble**
  - https://www.reddit.com/r/Angular2/comments/byjifs/introducing_ngbubble_an_npm_package_to_browse/
  - https://medium.com/@sandeepkgupta007/introducing-ng-bubble-your-angular-companion-f25dda56492
  - fügt ein skript in die seite ein, mit dem man per kontextmenü components inspizieren oder die entspr. component-datei direkt in der IDE öffnen kann
- **pretty-html-log**
  - https://github.com/angular-extensions/pretty-html-log
- **nx**
  - https://nx.dev/angular
  - https://github.com/nrwl/nx
  - *extensible dev tools for <mark>monorepos</mark>*
  - https://blog.nrwl.io/why-you-should-switch-from-lerna-to-nx-463bcaf6821
  - *Using Nx, you can add TypeScript, Cypress, Jest, Prettier, Nest.js, Storybook into your dev workflow. Nx sets up these tools and allows you to use them seamlessly*
  - *Angular CLI power-ups for modern development* (full-stack apps mit nestjs https://nx.dev/angular/fundamentals/build-full-stack-applications)
- **angular playground**
  - https://angularplayground.it/
  - test components in isolation
- **scully**
  - https://github.com/scullyio/scully
  - *The Static Site Generator for Angular apps*
- **angular state inspector**
  - chrome plugin
  - *Helps you debug Angular component state*
  - https://chrome.google.com/webstore/detail/angular-state-inspector/nelkodgfpddgpdbcjinaaalphkfffbem
- **JitBlox**
  - *visual prototyping tool and code generator for single-page applications*
  - <https://www.jitblox.com/blog/online-visual-prototyping-of-angular-apps-with-jitblox>


### environment
```ts
// environment.ts
export interface Environment {
  readonly name: 'dev' | 'test' | 'prod';
  readonly baseUrl: string;
}

// env.ts
export const env = {} as Environment;

// env.dev.ts
export const env: Environment = {
  name: 'dev',
  baseUrl: '/api'
}

// env.prod.ts
export const env: Environment = {...}

// logger.ts
interface Logger {}

// logger.dev.ts
class DevLogger implements Logger

// logger.prod.ts
class ProdLogger implements Logger

// app.module.ts
import { Environment } from 'environment.ts';
import { env } from 'env.ts'; // replaced (fileReplacements)
import DevLogger
import ProdLogger

function loggerFactory(env: Environment): Logger {
  return env.name === 'dev' ? new DevLogger() : new ProdLogger();
}

// muss interface als InjectionToken providen
export const ENV = new InjectionToken<Environment>('env');
providers: [
  { provide: Environment, useValue: ENV },
  { provide: Logger, useFactory: loggerFactory, deps: [Environment] } // todo: provide singleton
]

// some.class.ts
import ENV
import Environment
// dependency injection statt direkter import für leichteres mocken
constructor(@Inject(ENV) private env: Environment) {}
```
für diese Herangehensweise muss jedoch pro Env ein build durchgeführt werden.
**Alternativen**
1) env vom webserver laden (z.B. spezifisches env.json in docker image einfügen)
2) env von einem separaten backend server laden (frontend server proxied zum backend)


## Performance
- aot compilation
- https://github.com/mgechev/angular-performance-checklist
- https://netbasal.com/getting-to-know-the-attribute-decorator-in-angular-4f7c9fb61243
- https://theinfogrid.com/tech/developers/angular/angular-cli-budgets-angular-6/
- https://christianlydemann.com/the-complete-guide-to-angular-performance-tuning/
- https://www.reddit.com/r/Angular2/comments/bzsotu/printable_angular_performance_cheat_sheet/
- https://netbasal.com/optimizing-angular-change-detection-triggered-by-dom-events-d2a3b2e11d87
- https://github.com/mgechev/ngx-quicklink

### Lazy loading
- https://blog.angularindepth.com/network-aware-preloading-strategy-for-angular-lazy-loading-b883a0fbbaf0
- https://medium.com/wishtack/angular-lazy-loading-without-router-471166580c86
- https://blog.angular.io/angular-tools-for-high-performance-6e10fb9a0f4a
  - lazy loading ohne router (hero-loader, ngx-loadable)
- https://netbasal.com/welcome-to-the-ivy-league-lazy-loading-components-in-angular-v9-e76f0ee2854a
- https://blog.bitsrc.io/angular-maximizing-performance-with-the-intersection-observer-api-23d81312f178
- https://netbasal.com/lazy-load-modal-components-in-angular-8cb54bba7bf7

### Cache
- → service worker
- https://github.com/luckyseven/ngx-liquid-cache
- advanced caching with rxjs - https://www.youtube.com/watch?v=j7Gb1qw23ks
- https://nrempel.com/guides/angular-httpclient-httpinterceptor-cache-requests/
- https://www.reddit.com/r/Angular2/comments/86bqif/using_publishreplay1_and_refcount_with_httpclient/
- https://blog.thoughtram.io/angular/2018/03/05/advanced-caching-with-rxjs.html
- https://github.com/mgechev/memo-decorator
- https://github.com/angelnikolov/ngx-cacheable
- https://www.prestonlamb.com/blog/rxjs-cache-and-refresh-in-angular
- https://github.com/ngneat/cashew
