---
tags: [Notebooks/IDEs]
title: VS Code
created: '2019-02-20T20:27:28.336Z'
modified: '2021-09-29T13:27:50.211Z'
parent: IDE
---

# VS Code
- <https://viatsko.github.io/awesome-vscode/>
- Online/Browser: <https://vscode.dev/>

## Snippets
- <https://code.visualstudio.com/docs/editor/userdefinedsnippets>
- global oder pro Workspace
- eigene
  - <https://code.visualstudio.com/docs/editor/userdefinedsnippets#_create-your-own-snippets>
- → Plugins/snipsnap


## Plugins

### diverse
- **toggler**
  - <https://marketplace.visualstudio.com/items?itemName=hideoo.toggler>
  - *Toggle words and symbols in VS Code using a user defined configuration.*
  - ```
    "toggler.toggles": [
      ["!=","=="], ["!==","==="], ["&&","||"], ["<",">="], ["'","`","\""], ["false","true"], ["1","0"], ["+","],    
      ["resolve","reject"], ["development","production"], ["dev", "prod"], ["create","delete"], ["yes","no"],
      ["min","max"], ["set","get"], ["import","export"], ["left","right"], ["down","up"],["to","from"]
    ]
    ```
- **vscode-live-server**
  - <https://github.com/ritwickdey/vscode-live-server> ⭐1300
  - *Launch a development local Server with live reload feature for static & dynamic pages*
- **vscode-browser-preview**
  - https://github.com/auchenberg/vscode-browser-preview ⭐4.1k
  - *A real browser preview inside your editor that you can debug*
- **Todo+**
  - `"todo.statistics.project.enabled": "false"`
- **Bookmarks**
- <span>~~Bracket Pair Colorizer 2~~</span>
  - ~~UID: CoenraadS.bracket-pair-colorizer-2~~
  - ~~https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer-2~~
  - <https://code.visualstudio.com/blogs/2021/09/29/bracket-pair-colorization>
- **REST Client**
- **Thunder Client**
  - *lightweight Rest Client for Testing APIs*
  - unterstüzt HTTP/2
  - <https://www.thunderclient.com/>
  - <https://github.com/rangav/thunder-client-support#features>
- **Windows Explorer Context Menu**
- **Docker**
- **DotENV**
- **Indent Rainbow**
  - <https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow>
  - Grautöne:
    ```
    "indentRainbow.colors": [
    "rgba(16,16,16,0.1)",
    "rgba(16,16,16,0.2)",
    "rgba(16,16,16,0.3)",
    "rgba(16,16,16,0.4)",
    "rgba(16,16,16,0.5)",
    "rgba(16,16,16,0.6)",
    "rgba(16,16,16,0.7)",
    "rgba(16,16,16,0.8)",
    "rgba(16,16,16,0.9)",
    "rgba(16,16,16,1.0)"
    ```
- **Create tests**
  - <https://marketplace.visualstudio.com/items?itemName=hardikmodha.create-tests>
  - erzeugt für src-File ein test-File in einem Test-Verzeichnis mit automatischem Import, spiegelt die Verzeichnisstruktur von /src in /test
- ~~Settings Sync~~
  - jetzt Teil von VSCode
- **Project Manager**
  - <https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager>
- **SVG Viewer**
- **Trailing Spaces**
- **Fabulous**
  - <https://github.com/Raathigesh/fabulous>
  - css properties sidebar
- **auto-open markdown preview**
- **Sort lines**
  - <https://marketplace.visualstudio.com/items?itemName=Tyriar.sort-lines>
- **EditorConfig**
  - *attempts to override user/workspace settings with settings found in .editorconfig files*
- **path intellisense**
  - für Dateipfade im Workspace
- **msjsdiag.debugger-for-chrome**
  - <https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome>
  - <https://code.visualstudio.com/docs/nodejs/nodejs-debugging>
  - attach to already running server (running on localhost:8081)
    1) configure .vscode/launch.json
      ```json
      {
        "version": "0.1.0",
        "configurations": [
            {
                "name": "attach to chrome",
                "type": "chrome",
                "request": "attach",
                "port": 9222,
                "urlFilter": "http://localhost:8081", // or localhost:8081/*
                "webRoot": "${workspaceFolder}",
                "skipFiles": [
                  "${workspaceFolder}/node_modules/**/*.js",
                  "<node_internals>/**/*.js"
                ]
            }
        ]
      }
      ```
    2) launch chrome with `--remote-debugging-port=9222` and go to locahost:8081
    3) start the debugger in vscode
  - launch chrome
    1) launch.json
      ```json
      {
        "version": "0.1.0",
        "configurations": [
            {
                "name": "launch chrome",
                "type": "chrome",
                "request": "launch"
            }
        ]
      }
      ```
- **firefox-devtools.vscode-firefox-debug**
  - <https://marketplace.visualstudio.com/items?itemName=firefox-devtools.vscode-firefox-debug>
- **Assistant**
  - <https://marketplace.visualstudio.com/items?itemName=tomasz-smykowski.assistant>
  - eigene Linter-Regeln per Regex
  - *Realtime Linter & Quality Assurance For Your Team*
  - <https://itnext.io/8-visual-studio-code-assistant-rules-for-nasty-angular-bugs-9f186277e0ab>
  - <https://medium.com/@tomaszs2/12-assistant-rules-to-boost-productivity-a0c12bea3d19> (ng)
- **SonarLint**
  - UID: sonarsource.sonarlint-vscode
  - JS, Java, TS, ...
  - erfordert Java 11+
- **Blockman**
  - Highlight Nested Code Blocks
  - <https://marketplace.visualstudio.com/items?itemName=leodevbro.blockman>
- **vscode-database-client**
  - cweijan.vscode-mysql-client2
  - *supports MySQL/MariaDB, Microsoft SQL Server, PostgreSQL, SQLite, MongoDB, Redis, and ElasticSearch.*
  - <https://github.com/cweijan/vscode-database-client>
- **vscode-pdf**
  - PDF Viewer 

### Rechtschreibung
- **Spell Right**
  - <https://github.com/bartosz-antosik/vscode-spellright/>
  - prinzipiell jede (Programmier-)Sprache unterstützt
  - sehr konfigurierbar: kann Sprachen pro Dateiformat mischen, kann pro "Dateisektion" (Kommentar, body, string literal) Sprache festlegen, Ignores, ...
  - hat Probleme mit Umlauten (Encodingproblem?)
  - Quellen für Wörter:
    - user dictionary ($HOME/.config/Code/User/spellright.dict); stattdessen kann auch zum 'system default dict' hinzugefügt werden -> wo ist das?
    - workspace dictionary (.vscode/spellright.dict)
    - language dictionary ($HOME/.config/Code/Dictionaries/*.dic), zB de_DE.dic, de_AT.dic
    - man kann mehrere lang dicts gleichzeitig verwenden:
      "spellright.language": ["de_DE", "de_mystuff", ...]
  - markiert Fehler nach Save
  - basiert auf hunspell (linux package) → [Diverses/Rechtschreibprüfung](@note/Rechtschreibprüfung.md)
- **code spell checker**
  - <https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker>
  - hat Addon für DE
  - funktioniert mit vielen, aber nicht allen Progr.sprachen bzw. Dateitypen
  - funktioniert auch mit camelCase, ALLCAPS, snake_case
  - excludes/ignores
  - macht wesentlich bessere Korrekturvorschläge als 'spell right'
  - mehrere Sprachen gleichzeitig möglich
  - markiert Fehler schon während Eingabe
  - Quellen für Wörter
    - workspace (Knoten in .vscode/settings.json)
    - user (Knoten in $HOME/.config/Code/User/settings.json)
    - .vscode/cSpell.json oder ${workspace}/cSpell.json
    - extension's default dictionaries
  - basiert auf cspell (node_module) → [Diverses/Rechtschreibprüfung](@note/Rechtschreibprüfung.md)


### SCM
- **GitLens**
  - <https://github.com/eamodio/vscode-gitlens>
- **Git History**
- **SVN**

### sprachspezifische
- **Auto Import**
  - <https://marketplace.visualstudio.com/items?itemName=steoates.autoimport>
  - TypeScript
- **shellcheck**
  - wie Sonarlint für Linux-Shell-Skripte
  - [benötigtes Binary für Windows](https://storage.googleapis.com/shellcheck/shellcheck-latest.zip)
- **XML Tools**
- **redhat.vscode-xml**
- **sort json objects**
- **vscode-groovy-lint**
  - *lint, correct and format groovy and Jenkinsfile*
  - <https://github.com/nvuillam/vscode-groovy-lint>

#### JS
- **Import Cost**
- **Jest**
  - <https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest>
- **JS Parameter Annotations**
  - <https://marketplace.visualstudio.com/items?itemName=lannonbr.vscode-js-annotations>
  - buggy (Annot. fehlen manchmal)
- **Vetur**
  - für Vue
- **ESLint**
- **Yo**
  - <https://marketplace.visualstudio.com/items?itemName=samverschueren.yo>
- **npm**
- **npm Intellisense**
- **Quokka.js**
  - <https://quokkajs.com/>
  - *for rapid JavaScript / TypeScript prototyping. Runtime values are updated and displayed in your IDE next to your code, as you type*
- ~~wallaby.js~~ 💰
  - <https://wallabyjs.com/>
  - *tool that runs your JavaScript and TypeScript tests immediately as you type, highlighting results in your IDE right next to your code*
- **version lens**
  - zeigt neue Versionen von Deps in package.json
- **snipsnap**
  - <https://github.com/snipsnapdev/snipsnap>
  - *automatically exposes all available snippets for every library you are using in your project*
- **vuln cost**
  - Vulnerability scanning (js, ts, html)
  - <https://marketplace.visualstudio.com/items?itemName=snyk-security.vscode-vuln-cost>


##### Polymer
- **polymer.polymer-ide**
  - einigermaßen Code-Completion für Polymer
  - buggy (versteht kein dynamic import)
- ~~jonwolfe.language-polymer~~
  - nicht für template-function geeignet
- ~~[lit-html](https://marketplace.visualstudio.com/items?itemName=bierner.lit-html)~~
  - UID: bierner.lit-html
  - Syntax-Highlights für template-function
- ~~pushqrdx/vscode-inline-html~~
- [lit-plugin](https://marketplace.visualstudio.com/items?itemName=runem.lit-plugin)
  - UID: runem.lit-plugin
  - basiert auf bierner.lit-html


#### CSS
- **live sass compiler**
- **CSS Peek**
- **colorize**
  - UID: kamikillerto.vscode-colorize
  - zeigt die Farbe von rgba- oder hex-Strings in der IDE an, funktioniert in jeder Datei (js, ...) und mit CSS-Vars

#### Java
- **Java Extension Pack**
  - Language Support for Java
  - Java Dependency Viewer
  - Debugger for Java
  - Java Test Runner
  - Maven Project Explorer
- **GraalVM Extension Pack for Java**
  - *collection of extensions that helps users write, debug and test Java, JavaScript, Python, Ruby, R and polyglot applications running on GraalVM, either standalone or using the Micronaut framework. GraalVM Extension Pack for Java bundles GraalVM Tools for Java, GraalVM Tools for Micronaut, and Apache NetBeans Language Server extensions.*
- **GraalVM Tools for Java**
  - *provides full Java development and debugging capabilities and includes the GraalVM runtime with both just-in-time and ahead-of-time compilers*
  - *Besides Java, this extension enables a polyglot environment in VS Code and offers full editing and debugging capabilities for JavaScript and Node.js, Python, R, and Ruby languages. The extension provides a wizard to install GraalVM and help simplify configuring the development environment.*
- **Lombok Annotation Support**
- ~~Tomcat for Java~~
  - <https://marketplace.visualstudio.com/items?itemName=adashen.vscode-tomcat>
- **Community Server Connectors**
  - *provides a Remote Server Protocol based server connector, which can start, stop, publish to, and otherwise control Community runtimes and servers like Apache Felix, Karaf, and Tomcat.*
  - *Supported Servers*
    - *Apache Tomcat [ 5.5 - 9.0 ]*
    - *Apache Karaf [ 4.8 ]*
    - *Apache Felix [ 3.2 - 6.0 ]*
    - *Jetty [ 9.x ]*
    - *Glassfish [ 5.x ]*
    - *Websphere Liberty [ 21.x ]*
  - <https://marketplace.visualstudio.com/items?itemName=redhat.vscode-community-server-connector>
  - <https://code.visualstudio.com/docs/java/java-tomcat-jetty>
- **Checkstyle for Java**
  - <https://github.com/jdneo/vscode-checkstyle>
  - Bei Verwendung einer lokalen Datei (“checkstyle.configurationPath”) muss darauf geachtet werden, dass die Datei kompatibel zur Version von Checkstyle (“checkstyle.version”) ist. Es wird nur Inhalt der gespeicherten Datei validiert.
- **Spring Boot Extension Pack**
  - <https://marketplace.visualstudio.com/items?itemName=Pivotal.vscode-boot-dev-pack>
  - Spring Boot Tools
  - Spring Initializer
  - Spring Boot Dashboard
  - ...


### Remote
- <https://code.visualstudio.com/docs/remote/remote-overview>
- *allows you to use a container, remote machine, or the Windows Subsystem for Linux (WSL) as a full-featured development environment*
- remote extension pack: enthält Docker, SSH und WSL (auch alle einzeln erhältlich)

#### Container
- <https://github.com/Microsoft/vscode-dev-containers> - *A repository of development container definitions for the VS Code Remote* → diese Container können noch angepasst werden
- Java-Beispiele: <https://medium.com/@brunoborges/java-dev-environments-with-containers-66d6797b2753>
- <https://code.visualstudio.com/docs/remote/containers-advanced>
- `npm install` langsam: <https://code.visualstudio.com/remote/advancedcontainers/improve-performance>
- <https://github.com/manekinekko/awesome-devcontainers>

#### WSL
- <https://code.visualstudio.com/docs/remote/wsl>

#### WSL + Container
- WSL auf v2 updaten (<https://docs.microsoft.com/en-us/windows/wsl/install-win10>)
- eine Linux-Distro aus MS-Store installieren
- in Docker-Settings "use the wsl2 based engine" aktivieren
- <https://code.visualstudio.com/blogs/2020/07/01/containers-wsl>
- Ports müssen trotzdem freigegeben werden (`forwardedPorts` in devcontainer.json)
