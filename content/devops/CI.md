---
tags: [Notebooks/DevOps]
title: CI
parent: DevOps
---

# CI

## Produkte
- **Jenkins**
- **CircleCI**
- **appveyor**
  - <https://www.appveyor.com>
- **TravisCI**
- **ConcourseCI**
  - <https://concourse-ci.org>
  - *Concourse is an open-source continuous thing-doer*
  - <https://github.com/concourse/concourse>
- **codeship**
  - <https://codeship.com>
- **codefresh**
  - <https://codefresh.io>
- **buildkite**
  - <https://buildkite.com>
- **earthly**
  - *build automation tool for the container era*
  - *use Earthly to create Docker images and artifacts (e.g., binaries, packages, arbitrary files).*
  - *meant to be used both on your development machine and in CI. It can run on top of popular CI systems (like Jenkins, Circle, GitHub Actions). It is typically the layer between language-specific tooling (like maven, gradle, npm, pip, go build) and the CI build spec.*
  - <https://github.com/earthly/earthly>
- **Woodpecker**
  - *uses docker containers to execute pipeline steps*
  - <https://github.com/woodpecker-ci/woodpecker>
- **dagger**
  - *portable devkit for CICD*
  - *can develop powerful CICD pipelines with minimal effort, then run them anywhere*
  - *can be used with any CI environment (with Docker pre-installed)*
  - *does not replace your CI: it improves it by adding a portable development layer on top of it.*


## Build steps
- SCM
- Lint
- Audit (Dependencies)
- Lizenzprüfung (3rd Party)
- Test
    - Unit, Integration, E2E
    - Ergebnisse veröffentlichen
- Artefakte
    - Build
    - Archivierung
    - Deployment
- Benachrichtigen (im Fehlerfall)
