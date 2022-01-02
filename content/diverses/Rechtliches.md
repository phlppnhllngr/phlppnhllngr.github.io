---
tags: [Notebooks/Diverses]
title: Rechtliches
created: '2019-10-16T21:29:09.505Z'
modified: '2021-09-02T09:26:51.657Z'
parent: Diverses
---

# Rechtliches

## Commercial use
- *(...) internal use which improves (...) ability to compete in the market - is a commercial purpose. As such, you cannot use non-commercial licenses for internal work at any company that competes in a commercial market.*
  (<https://workplace.stackexchange.com/a/117992>)
- *Commercial use means that is is used for a business. An entity that practices commerce, selling products or services.
  This is commercial use even if the ACTUAL use is not for sale, as long as the use itself supports the business.*
  (<https://www.quora.com/What-does-commercial-use-of-software-mean-exactly>)


## Software-Lizenzen
- Software ohne Lizenz darf nicht kommerziell eingesetzt werden [(Quelle)](https://choosealicense.com/no-permission/)
- <https://choosealicense.com/licenses/>
- <http://tldrlegal.com/>
- <https://opensource.org/licenses/>
- <https://opensource.google/docs/thirdparty/licenses/>
  - mit Einteilung in Kategorien (nach Freiheit)
- **ScanCode**
  - *detects licenses, copyrights, package manifests & dependencies and more by scanning code ... to discover and inventory open source and third-party packages used in your code.*
  - *standalone command-line tool*
  - *detects licenses, copyrights, package manifests, direct dependencies, and more both in source code and binary files*
  - *can save your scan results as JSON, HTML, CSV*
  - *can process these packages, build manifest and lockfile formats to extract metadata:  Java EAR/WAR/JAR,  Apache Maven, JavaScript npm packages, package-lock.json, yarn.lock, ...*
  - python based
  - options
    - `--ignore`
      - default wird nichts ignored
      - funktioniert nicht: `--ignore "*.{jpg,png}"`, `--ignore "*.(jpg|png)"`
      - funktioniert: `--ignore "*.jpg" --ignore "*.png"`
    - `--include`
      - wenn nicht angegeben, werden alle dateitypen durchsucht
      - `--include "*.md" --include ".txt"`
  - <https://github.com/nexB/scancode-toolkit> *1.2k
- **fossology**
  - license compliance software system and toolkit
  - can run license, copyright and export control scans from the command line
  - a database and web ui are provided to give you a compliance workflow
  - <https://github.com/fossology/fossology> *474


## Datenschutz

### DSGVO / GDPR
