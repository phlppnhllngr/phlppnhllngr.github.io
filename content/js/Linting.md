---
tags: [Notebooks/Javascript]
title: Linting
created: '2019-10-09T10:52:22.323Z'
modified: '2021-05-08T13:08:52.302Z'
parent: JavaScript
---

# Linting

## Tooling
- **lint-staged**
  - https://github.com/okonet/lint-staged
- **prettier**
  - https://prettier.io
  - pretty-quick
    - https://github.com/azz/pretty-quick
    - *Runs Prettier on your changed files.* (Git)
- **ESLint**
  - https://eslint.org
  - presets
    - eslint-config-airbnb(-base)
  - plugins
    - eslint-plugin-spellcheck
      - https://www.npmjs.com/package/eslint-plugin-spellcheck
      - Das Plugin bringt nur Englisch mit. Da es auf [hunspell] basiert, könnte man aber eigene dictionaries in sein Verzeichnis kopieren.
    - ~~https://www.npmjs.com/package/eslint-plugin-polymer~~
    - eslint-plugin-prefer-logger
      - https://github.com/wreulicke/eslint-plugin-prefer-logger
    - eslint-plugin-fp
      - (functional programming)
      - https://github.com/jfmengels/eslint-plugin-fp
    - eslint-plugin-import
      - https://github.com/benmosher/eslint-plugin-import
      - *import/export syntax, and prevent issues with misspelling of file paths and import names*
    - eslint-plugin-you-dont-need-lodash-underscore
    - eslint-plugin-standard
      - deprecated
      - https://www.npmjs.com/package/eslint-plugin-standard
    - eslint-plugin-html
      - *lint and fix inline scripts contained in HTML files*
      - https://www.npmjs.com/package/eslint-plugin-html
    - eslint-plugin-promise
      - https://www.npmjs.com/package/eslint-plugin-promise
    - eslint-plugin-jsdoc
      - https://www.npmjs.com/package/eslint-plugin-jsdoc
    - eslint-plugin-unicorn
      - *Various awesome ESLint rules*
      - https://github.com/sindresorhus/eslint-plugin-unicorn
  - eslint-friendly-formatter
    - formatter/reporter
    - https://www.npmjs.com/package/eslint-friendly-formatter
  - eigene Regeln
    - https://blog.theodo.com/2020/04/create-your-own-eslint-rules/
- **standard**
  - https://github.com/standard/standard *22400
  - *JavaScript Style Guide, with linter & automatic code fixer*
  - 0-config
- **rslint**
  - https://github.com/rslint/rslint
  - rust based


### prettier vs Linter
- prettier behandelt nur Formatierung (z.B. max line length), aber nichts wie z.B. 'no unused vars' [(Quelle)](https://prettier.io/docs/en/comparison.html)
- prettier kann im Zusammenspiel mit Lintern so konfiguriert werden, dass es sich um Formatting kümmert, und die Linter um Code-Quality; z.B. eslint-config-prettier [(Quelle)](https://prettier.io/docs/en/integrating-with-linters.html)
- *they have an overlap in functionality, which makes integrating and enforcing them challenging*


### VSCode + prettier + eslint
- *ESLint’s JSON files also allow JavaScript-style comments*
- kann eslint config auch in package.json stehen haben
- commit-hook → run lint-staged
- https://www.youtube.com/watch?v=SydnKbGc7W8 - traversy media 19.7.19
- https://silvenon.com/blog/integrating-and-enforcing-prettier-and-eslint - 25.3.19
- <u>VSCode-Plugins</u>
  - **prettier**
    - settings (→ inwiefern überschneidet/beißt sich das mit .prettierrc?)
      - format on save: true
      - semi: true
      - single quote: true
      - tab width: 2
- **npm modules**
  - `npm i -D eslint prettier eslint-plugin-prettier eslint-config-prettier`
  - eslint-plugin-node, eslint-config-node
  - eslint-config-airbnb-base `npm install-peerdeps --dev eslint-config-airbnb-base`
- create .prettierrc
<br/>
- disable conflicting rules
- eslintrc#extends: prettier at the bottom/end so it can disable conflicting rules introduced by previous configs
- check conflicts between prettier and eslint (e.g. prettier auto adds semicolon and eslint has rule semi→error)
- rules must be enforced → husky git hooks + lint-staged
- *eslint-plugin-prettier’s recommended configuration, which does three things:
adds itself to plugins | enables the prettier/prettier rule | adds eslint-config-prettier to extends*
    ```
    {
      "extends": [
        "airbnb",
        "plugin:prettier/recommended"
      ]
    }
    ```
    ```
    {
      "scripts": {
        "check-eslint-config": "eslint --print-config . | eslint-config-prettier-check",
        "check-code": "eslint src"
      },
      "husky": {
        "hooks": {
          "pre-commit": "lint-staged",
          "pre-push": "yarn check-eslint-config && yarn check-code"
        }
      },
      "lint-staged": {
        "*.js": [
          "eslint --fix",
          "git add"
        ]
      }
    }
    ```
