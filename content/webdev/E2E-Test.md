---
tags: [Notebooks/Webdev]
title: E2E-Test
created: '2019-02-14T15:21:55.517Z'
modified: '2021-08-14T13:41:23.510Z'
parent: Webdev
---

# E2E-Test
- <https://storybook.js.org/blog/how-to-actually-test-uis/>
- <https://css-tricks.com/front-end-testing-is-for-everyone/>

## Tools
- **puppeteer & playwright**
  - ~~Puppeteer~~Headless Recorder
    - *Chrome extension that records your browser interactions and generates a Puppeteer/playwright script*
    - Stand 27.11.20 kein Support für Shadow-DOM <https://github.com/checkly/headless-recorder/issues/51>
    - <https://github.com/checkly/headless-recorder>
  - theheadless.dev
    - <https://theheadless.dev/>
    - *open source knowledge base for Puppeteer and Playwright*
- **playwright**
  - <https://github.com/microsoft/playwright>
  - <https://github.com/microsoft/playwright-java>
  - alle Browser (playwright) oder individuell (playwright-chrome, ...) oder mit vorinstalliertem Browser (playwright-core) nutzbar
  - Docs
    - <https://github.com/microsoft/playwright/blob/master/docs/api.md>
    - [troubleshooting](https://github.com/microsoft/playwright/blob/master/docs/troubleshooting.md)
  - Tipps
    - [browser launch options](https://github.com/microsoft/playwright/blob/master/docs/api.md#browsertypelaunchoptions)
      - `args: [--start-maximized]` um Chrome fullscreen zu starten (`contextConfig.viewport = null`)
  - Tools
    - docker-image
      - <https://playwright.dev/docs/docker/>
    - @playwright/test
      - *Browser automation, Jest-like assertions and built-in support for TypeScript*
      - junit test reports
      - <https://playwright.dev/docs/test-intro/>
    - inspector
      - *GUI tool that helps authoring and debugging Playwright scripts*
      - <https://playwright.dev/docs/inspector>
  - Tools (3rd party)
    - <https://github.com/mxschmitt/awesome-playwright>
    - <https://playwright.dev/docs/showcase/>
    - ~~https://github.com/mmarkelov/jest-playwright-example~~
    - expect-playwright
      - (Erweiterung von) `expect` für playwright (mit oder ohne jest)
      - `await expect(page).toHaveText("#foo", "my text")`
      - `toHaveSelector, toHaveSelectorCount, toHaveText, toEqualText, toEqualValue`
      - <https://github.com/playwright-community/expect-playwright>
    - jest-playwright
      - <https://github.com/mmarkelov/jest-playwright>
      - *Jest preset to run Playwright tests with Jest*
      - <https://dev.to/mxschmitt/using-jest-with-playwright-28dh>
    - <https://github.com/alisterscott/playwright-jest-demo>
    - qawolf
      - https://github.com/qawolf/qawolf
      - Wrapper um playwright
      - generiert Tests mit jest
      - *Record and create Playwright tests and then run them in CI*
      - Stand 27.11.20 kein Support für Shadow-Dom
    - https://github.com/e2e-boilerplate/playwright-typescript-ts-jest-jest-expect
    - → Puppeteer/Tools (z. T. kompatibel)
- **CodeceptJS**
  - http://codecept.io/
  - https://codecept.io/docker/
  - https://github.com/Codeception/CodeceptJS ⭐2150
  - *CodeceptJS is a testing framework that takes a scenario-driven, behaviour driven development (BDD) approach, with an API language that is easy for non-engineers to understand and use. However, perhaps even more importantly, it is backend agnostic. It is written on top of several popular testing libraries (WebDriverIO or Puppeteer, for example) and its single high level API communicates to whichever one you choose.*
      ```js
      Feature('My First Test');

      Scenario('test something', (I) => {
        I.amOnPage('https://github.com');
        I.see('GitHub');
      });
      ```
- **Selenium**
  - https://www.seleniumhq.org/
  - <u>Tools</u>
    - Selenium IDE
      - https://selenium.dev/selenium-ide/
      - *record and playback test automation for the web*
      - Fallback-Selektoren
      - Plugins für Chrome und Firefox
    - zalenium
      - https://github.com/zalando/zalenium
      - *Selenium Grid extension to scale your local grid dynamically with docker containers*
      - *uses docker-selenium to run your tests in Firefox and Chrome locally, if you need a different browser, your tests can get redirected to a cloud testing provider*
    - webdrivermanager
      - https://github.com/bonigarcia/webdrivermanager
      - *allows to automate the management of the binary drivers (e.g. chromedriver, geckodriver, etc.) required by Selenium WebDriver*
    - selenide
      - *Simple configuration*
      - https://selenide.org/
- **Webriver.io**
  - http://webdriver.io/
  - *WebDriver bindings for Node.js*
  - https://github.com/webdriverio/webdriverio/ ⭐5.3k
  - wird von <a href="https://github.com/admc/wd"><b>wd</b></a> als neuere Alternative empfohlen
- **Puppeteer**
  - https://github.com/GoogleChrome/puppeteer ⭐47.400
  - installiert Chromium (kann übersprungen werden; `PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true`) für die jeweilige Plattform
  - puppeteer-core
    - nur puppeteer, ohne Chromium
    - *connect to installed or remote browser*
  - puppeteer-firefox
    - https://www.npmjs.com/package/puppeteer-firefox
    - https://aslushnikov.github.io/ispuppeteerfirefoxready/
    - `node e2e.js puppeteer-firefox` → `const puppeteer = require(process.argv[2]);`
  - Tools
    - Stand 27.11.20 hat Chrome Canary einen Recorder eingebaut (experimental)
    - https://github.com/thomasdondorf/puppeteer-cluster ⭐550
      - *run a cluster of instances in parallel*
    - https://puppeteersandbox.com/
    - https://chrome.browserless.io/ (browser repl)
    - https://github.com/checkly/puppeteer-examples
    - https://github.com/smooth-code/jest-puppeteer ⭐2400
    - https://github.com/berstend/puppeteer-extra ⭐850
      - stealth, adblock, flash, captcha solving, ...
    - shadow dom
      - query-selector-shadow-dom
        - https://github.com/Georgegriff/query-selector-shadow-dom
    - a11y
      - https://developers.google.com/web/updates/2020/11/puppetaria
  - https://addyosmani.com/blog/puppeteer-recipes/
- **nightmare**
  - https://github.com/segmentio/nightmare ⭐17.000
  - *A high-level browser automation library.*
  - basiert auf electron
  - record-to-test-script: https://github.com/segmentio/daydream
- **cypress**
  - https://www.cypress.io/
  - *All-in-one testing framework, assertion library, with mocking and stubbing, all without Selenium.*
  - headless oder headed
  - mögliche Browser: Electron (default), Chrome/Chromium, Firefox, Edge
  - https://github.com/cypress-io/cypress ⭐31.7k
    - https://github.com/cypress-io/cypress-realworld-app
  - https://github.com/cypress-io/cypress-docker-images
  - benutzt intern mocha
  - Plugins
    - https://github.com/cypress-io/code-coverage
- **gauge**
  - https://gauge.org/
  - https://github.com/getgauge/gauge
- **taiko**
  - *A node.js library to automate chrome/chromium browser*
  - https://github.com/getgauge/taiko ⭐1000
- **TestProject**
  - https://testproject.io/
- **browserless**
  - https://github.com/joelgriffith/browserless
  - *Chrome as a service in docker. browserless is a web-service that allows for remote clients to connect, drive, and execute headless work; all inside of docker. It offers first-class integrations for puppeteer, selenium's webdriver, and a slew of handy REST API's for doing more common work*
- **nightwatch**
  - http://nightwatchjs.org/
  - https://github.com/nightwatchjs/nightwatch ⭐9.150
  - js, webdriver based
- **testcafe**
  - https://github.com/DevExpress/testcafe ⭐7400
  - https://devexpress.github.io/testcafe/
  - npm package, docker image
  - eigene no-code-GUI (https://www.devexpress.com/products/testcafestudio) (💰)
  - alle üblichen Browser, headed/headless, Plugins für saucelabs und browserstack
- **hermione**
  - https://github.com/gemini-testing/hermione ⭐340
  - *utility for integration testing of web pages using WebdriverIO v4 and Mocha.*
- **smashtest**
  - https://smashtest.io/
  - https://github.com/smashtestio/smashtest ⭐485
  - <mark>no-code/low-code</mark>-Wrapper um Selenium (Code optional)
  - *Smashtest is a language for rapidly describing and deploying test cases.*
- **galen**
  - http://galenframework.com/
  - *test location of objects relatively to each other on page. Using a special syntax and comprehensive rules you can describe any layout you can imagine*
  - https://github.com/galenframework/galen
- **web test runner**
  - https://modern-web.dev/docs/test-runner/overview/
- **Testsigma**
  - *test automation platform that works out of the box. Rapidly(5X faster) automate web, mobile app, and API tests in plain English*
  - *Smart test recorder auto-converts user actions into editable steps.*
  - *Automate end-to-end testing for web, mobile apps & APIs.*
  - <https://github.com/testsigmahq/testsigma>


### Cloud, SaaS
- **browserstack** 💰
  - https://www.browserstack.com/
  - selenium (java, js, ...)
- **lambdatest** 💰
  - https://www.lambdatest.com/
  - java, js, ...
- **testingbot** 💰
  - https://testingbot.com/
  - java, js, ...
- **saucelabs** 💰
  - https://saucelabs.com/
- **ghost inspector** 💰
  - https://ghostinspector.com/
- **crossbrowsertesting** 💰
  - https://crossbrowsertesting.com/
- **endtest** 💰
  - https://endtest.io/
  - *codeless automated testing, powered by ML*
  - "self healing" (Selektoren)
- **testcraft**
  - https://www.testcraft.io/
  - *CODELESS SELENIUM WITH AI MAINTENANCE*
- **HeadlessTesting** 💰
  - https://headlesstesting.com/
  - *Run your Puppeteer and Playwright tests on headless instances in our cloud.*
- **perfecto**
  - https://www.perfecto.io/
- **testproject**
  - https://testproject.io/
- **accelq**
  - https://www.accelq.com/


### Visual Regression
- https://project-awesome.org/mojoaxel/awesome-regression-testing
- Resemble.js, jsdifflib, Visual Center, Review, Spectre, CSS Critic, Gemini, Reg-cli, Differencify, Kobold, Happo
- **applitools**
  - https://applitools.com/
  - *Intelligent Functional and Visual Testing Through Visual AI*
  - 💰 & free
- **percy**
  - https://percy.io/
  - Integrationen für viele e2e-Frameworks
  - gut dokumentiert
- **wraith**
  - http://bbc-news.github.io/wraith/
- **webdrivercss**
  - https://github.com/webdriverio-boneyard/webdrivercss
- **BackstopJs**
  - https://github.com/garris/BackstopJS *4600
  - *automates visual regression testing of your responsive web UI by comparing DOM screenshots over time*
- **jlineup**
  - https://github.com/otto-de/jlineup *40
- **jest-image-snapshot** → js/test


### Recorder
- **Chrome Recorder Panel**
  - <https://www.youtube.com/watch?v=rMUayh1QPYs>
- **rrweb**
  - Zeichnet Events (Klicks, Mausbewegungen, ...) auf. Kann als json gespeichert und dann wieder abgespielt werden.
  - <https://github.com/rrweb-io/rrweb> ⭐5.7k