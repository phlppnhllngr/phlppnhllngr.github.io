---
tags: [Notebooks/SCM]
title: Commits
created: '2019-04-07T19:14:21.679Z'
modified: '2020-12-05T20:49:53.939Z'
parent: SCM
---

# Commits

## Konventionen
- **commit-messages-guide**
  - [https://github.com/RomuloOliveira/commit-messages-guide](https://github.com/RomuloOliveira/commit-messages-guide) *6k
  - *A guide to understand the importance of commit messages and how to write them well*
  - Regeln
    - capitalize first letter
    - use imperative form
    - why, what, how
- **conventional commits**
  - [https://www.conventionalcommits.org](https://www.conventionalcommits.org)
  - [https://github.com/conventional-commits/conventionalcommits.org](https://github.com/conventional-commits/conventionalcommits.org)
  - *A specification for adding human and machine readable meaning to commit messages*
  - *The commit message should be structured as follows:*
    ```
    <type>[optional scope]: <description>
    [optional body]
    ```
  - [Tools](https://www.conventionalcommits.org/en/v1.0.0/#tooling-for-conventional-commits)
    - standard version
      - [https://github.com/conventional-changelog/standard-version](https://github.com/conventional-changelog/standard-version)
      - *Automate versioning and CHANGELOG generation, with semver.org and conventionalcommits.org*
    - commitlint
      - https://github.com/conventional-changelog/commitlint
      - *commitlint checks if your commit messages meet the conventional commit format*
      - node_module, Integration mit husky
    - ...
- **commitizen**
  - [https://github.com/commitizen](https://github.com/commitizen)
  - CLI
    - *When you commit with Commitizen, you'll be prompted to fill out any required commit fields at commit time*
    - [https://github.com/commitizen/cz-cli](https://github.com/commitizen/cz-cli)
    - node_module
    - Plugins
      - [https://github.com/KnisterPeter/vscode-commitizen](https://github.com/KnisterPeter/vscode-commitizen)
- **Angular Commit Guidelines**
  - [https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits)
    - commit message
      ```
      <type>(<scope>): <subject>
      <BLANK LINE>
      <body>
      <BLANK LINE>
      <footer>
      ```
    - examples
      `chore(*): update Node.js from 8 to 12`
      `docs(.editorconfig): change link to use https`
    - <mark>types: feat, test, fix, chore, ci, build, docs, refactor, perf</mark>
    - *subject: use the imperative, present tense. don't capitalize first letter. no dot (.) at the end*
    - *body: use the imperative, present tense*
  - [https://nitayneeman.com/posts/understanding-semantic-commit-messages-using-git-and-angular/](https://nitayneeman.com/posts/understanding-semantic-commit-messages-using-git-and-angular/)
- **semantic-release**
  - [https://github.com/semantic-release/semantic-release](https://github.com/semantic-release/semantic-release)
  - *Fully automated version management and package publishing*
  - *automates the whole package release workflow including: determining the next version number, generating the release notes and publishing the package*
  - *uses the commit messages to determine the type of changes in the codebase*
  - Plugins für Maven (→; Java/Maven/Plugins) und Gradle


## Hooks
- Problem lokaler git hooks: .git wird nicht committed, daher Tools zum Teilen mit Team
- **pre-commit**
  - [https://pre-commit.com/](https://pre-commit.com/)
  - *framework for managing and maintaining multi-language pre-commit hooks*
- **Husky**
  - [https://github.com/typicode/husky](https://github.com/typicode/husky) *16k
  - node_module
- **lefthook**
  - *polyglot Git hooks manager (any environment)*
  - Go binary / node_module
  - [https://github.com/Arkweid/lefthook](https://github.com/Arkweid/lefthook) *800
  - [https://evilmartians.com/chronicles/lefthook-knock-your-teams-code-back-into-shape](https://evilmartians.com/chronicles/lefthook-knock-your-teams-code-back-into-shape)
  - nach eigenen Angaben leichtgewichtiger + schneller als husky (+lint-staged)
  - *supports parallel execution*
- **overcommit**
  - [https://github.com/sds/overcommit](https://github.com/sds/overcommit) *3100
  - Ruby binary
