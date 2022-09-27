---
title: Remote Debugging
parent: Webdev
---

# Remote Debugging

## weinre
- <http://www.codeblocq.com/2016/03/Remote-Web-Debugging-with-weinre/>
- Vorgehen
  - ipconfig → IPv4-Adresse rausfinden (boundHost)
  - in der zu debuggenden Website das Skript einfügen
  - den Webserver für die Webseite starten
  - auf dem Mobilgerät die Webseite aufrufen
  - die weinre-Adresse im Desktop-Browser aufrufen
  - oben unter "Access Points" auf "debug user interfaces"
  - unter "Targets" sollte jetzt ein Eintrag mit Adresse des Geräts und Webservers verfügbar sein
  - oben in der Leiste Markup / console / Network / localstorage (etc) inspizieren
  - bei hover über HTML-Element wird es auf dem Mobilgerät markiert 
  - unten in der Leiste kann die Konsole aufgeklappt werden, wo man mit $0 mit einem ausgewählten Element interagieren kann
  - rechts kann Style geändert werden: Doppelklick element.style → property → Enter → value → Enter

## JSConsole
- <http://www.codeblocq.com/2016/03/Remote-JavaScript-debugging-with-jsconsole/>

## VorlonJs
- <http://www.vorlonjs.io/>
- <https://github.com/MicrosoftDX/Vorlonjs/>
- ähnlich weinre

## RemoteDebug iOS WebKit Adapter
- <https://github.com/RemoteDebug/remotedebug-ios-webkit-adapter>
- *allows Safari and WebViews on iOS to be debugged from tools like VS Code, Chrome DevTools, Mozilla Debugger.html and other tools compatible with the Chrome Debugging Protocol.*
- 1.2.20: *Important message for Windows users! Currently the adapter doesn't work for IOS 12+. For IOS 11 there are a few additional steps*
- ~~https://github.com/Microsoft/vscode-ios-web-debug~~ deprecated
- <https://github.com/google/ios-webkit-debug-proxy>

## eruda
- <https://github.com/liriliri/eruda>
- Script zum Einbinden, erzeugt Button zum Öffnen einer Pseudo-Console (für mobile Browser)

## vConsole
  - Script zum Einbinden
  - *Features: View console logs, View network requests, View document elements, View Cookies, LocalStorage and SessionStorage, Execute JS command manually, Custom plugin*
  - <https://github.com/Tencent/vConsole> *12.9k
