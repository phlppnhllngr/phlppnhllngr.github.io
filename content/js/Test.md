---
tags: [Notebooks/Javascript]
title: Test
created: '2019-02-14T20:50:41.681Z'
modified: '2021-05-18T11:06:43.244Z'
parent: JavaScript
---

# Test
- https://github.com/goldbergyoni/javascript-testing-best-practices *9.8k
  - *Comprehensive and exhaustive JavaScript & Node.js testing best practices*

## Frameworks, Runners
- Karma
  - https://karma-runner.github.io/latest/index.html
- Jasmine
  - https://jasmine.github.io/
- Wallaby
  - https://wallabyjs.com/
- Mocha
  - https://mochajs.org/
- cypress
- ava
  - https://github.com/avajs/ava ⭐17.4k
- Jest
  - https://facebook.github.io/jest/
  - https://github.com/facebook/jest ⭐29k
  - Tipps
    - manche flags sind nur als cli-args möglich, und nicht im config-file (z.B. `detectOpenHandles` und `runInBand`)
    - `--bail` führt dazu, dass nach der ersten fehlgeschlagenen suite (=file) abgebrochen wird. um schon nach dem ersten fehlgeschlagenen it/test abzubrechen, braucht man `jest-circus`: https://github.com/facebook/jest/issues/6527#issuecomment-734917527
  - tooling
    - https://github.com/jest-community/awesome-jest
    - majestic
      - https://github.com/Raathigesh/majestic ⭐4800
      - *Zero config GUI for Jest*
    - jest-extended
      - https://github.com/jest-community/jest-extended
      - expect().toBeEmpty(), toBeNil()
      - Array: expect(Array).toIncludeAllMembers([members]), .toIncludeAnyMembers([members])
      - boolean: .toBeTrue(), .toBeFalse()
      - Date: .toBeAfter(date)
      - number: .toBeNumber(), .toBeNaN(), .toBePositive(), .toBeWithin(start, end)
      - String: toStartWith, toInclude
      - ...
    - vscode-jest
      - https://github.com/jest-community/vscode-jest
      - *The optimal flow for Jest based testing in VS Code*
    - jest-dom
      - https://github.com/testing-library/jest-dom
      - https://testing-library.com/docs/ecosystem-eslint-plugin-jest-dom
    - jest-expect-message
      - https://www.npmjs.com/package/jest-expect-message
      - *With jest-expect-message this will fail with your custom error message*
    - jest-stare
      - https://github.com/dkelosky/jest-stare
      - *HTML Reporter and Results Processor*
    - jest-html-reporter
      - https://github.com/Hargne/jest-html-reporter
    - jest-html-reporters
      - https://github.com/Hazyzh/jest-html-reporters
    - jest-junit
      - *reporter that creates compatible junit xml files*
      - https://github.com/jest-community/jest-junit
    - jest-image-snapshot
      - *Jest matcher for image comparisons. Most commonly used for visual regression testing.*
      - *using pixelmatch; https://github.com/mapbox/pixelmatch*
      - ```js
        const image = await page.screenshot();
        expect(image).toMatchImageSnapshot();
        ```
      - https://github.com/americanexpress/jest-image-snapshot
- testing-library
  - https://testing-library.com/
  - Erweiterungen für Angular, Vue, svelte, cypress, puppeteer, ...
  - dom-testing-library
    - https://github.com/testing-library/dom-testing-library
- testem
  - https://github.com/testem/testem ⭐2.9k
  - *Support for Jasmine, QUnit, Mocha, Others, through custom test framework adapters. Run tests in all major browsers as well as Node and PhantomJS*
- cucumber
  - https://cucumber.io/
  - https://github.com/cucumber/cucumber-js


## Assertions
- Chai
- jest
- jasmine
- cypress


## Mock, Spy
- https://www.npmjs.com/package/faker
- http://sinonjs.org/
- https://github.com/Netflix/pollyjs (Http)
- https://github.com/jsdom/jsdom
- jasmine
- jest
- enzyme


## Code coverage
- istanbul
