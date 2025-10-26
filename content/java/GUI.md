---
tags: [Notebooks/Java]
title: 'GUI'
parent: Java
---

# GUI

## JavaFX
- <https://www.jfx-central.com/>

### Docs
- <https://github.com/openjfx/samples>
- native
  - <https://github.com/mipastgt/JFXToolsAndDemos/blob/master/docs/articles/JFX-Native/JFX-Native.adoc>
    - *This article summarizes the experiences which I collected while converting one of my existing Java applications to a native application using the Gluon Client Maven plugin*
  - <https://gluonhq.com/javafx-in-the-new-era-of-graalvm/>
- <https://edencoding.com/>
- <https://github.com/wiverson/maven-jpackage-template>
  - *Sample project illustrating building nice, small cross-platform JavaFX-based desktop apps with native installers while still using the standard Maven dependency system.*
- **CSS**
    - <http://docs.oracle.com/javase/8/javafx/api/javafx/scene/doc-files/cssref.html>


### Entwicklungstools
- <https://github.com/mhrimaz/AwesomeJavaFX>
- **maven archetypes**
  - <https://github.com/openjfx/javafx-maven-archetypes>
- <https://github.com/mipastgt/JFXToolsAndDemos>
  - *A collection of tools and demos for JavaFX.*
- **Scenic View**
  - <http://fxexperience.com/scenic-view/>
- **Scene builder**
  - <https://gluonhq.com/products/scene-builder/>
- **cssfx**
  - *Allow runtime modification of JavaFX CSS*
  - <https://github.com/McFoggy/cssfx>
- <u>Maven-Plugins</u>
  - **openjfx/javafx-maven-plugin**
    - <https://github.com/openjfx/javafx-maven-plugin>
  - **javafx-maven-plugin**
    - <https://github.com/javafx-maven-plugin/javafx-maven-plugin>
    - *wrapper for the packaging tool that comes with JavaFX, javapackager*
    - *native executables, installers & jar*
    - [archived docs](http://web.archive.org/web/20170926160512/http://javafx-maven-plugin.github.io/) (→ <https://github.com/javafx-maven-plugin/javafx-maven-plugin/issues/363>)
  - **gluonfx plugin for maven**
    - <[https://docs.gluonhq.com/client/](https://docs.gluonhq.com/#_gluonfx_plugin_for_maven)>
    - *leverages GraalVM, OpenJDK and JavaFX 11+, by compiling into native code the Java Client application and all its required dependencies, so it can directly be executed as a native application on the target platform*
- **e(fx)clipse**
- **JPackageScriptFX**
  - <https://github.com/dlemmermann/JPackageScriptFX>
  - *A tutorial project featuring a build script (Mac, Windows) for JavaFX applications based on the new jpackage tool.*
- <u>updates</u>
  - **updatefx**
    - *web style online updates of Java applications*
    - <https://github.com/vinumeris/updatefx>
  - **fxlauncher**
    - *Auto updating launcher for JavaFX Applications*
    - <https://github.com/edvin/fxlauncher>
- **KickstartFX**
  - *template for JavaFX applications*
  - <https://github.com/xpipe-io/kickstartfx> 
  - <https://old.reddit.com/r/java/comments/1o8s973/introducing_kickstartfx_the_most_advanced_javafx/> 


### Libs

#### Meta-Frameworks
- **WorkbenchFX**
  - *build large applications from multiple views*
  - <https://github.com/dlsc-software-consulting-gmbh/WorkbenchFX>
- **jpro**
  - <https://www.jpro.one/>
  - *JavaFX-Anwendungen ohne nötiges Java-Plug-in im Browser ausführen*
  - *führt die JavaFX-Anwendung auf einem Server oder in Docker aus und mappt den JavaFX-Scenegraph, der das User Interface beschreibt, direkt auf einen HTML-DOM-Graphen im Browser des Clients.*
  - self hosted/free oder cloud/paid

#### UI Components
- **JFoenix**
  - <http://jfoenix.com/>
  - <https://github.com/jfoenixadmin/JFoenix>
  - Material Design
- **JMetro**
  - <https://pixelduke.com/java-javafx-theme-jmetro/>
  - Fluent Design (=Office Look), mit Dark Theme
- **bootstrapfx**
  - <https://github.com/kordamp/bootstrapfx>
- **MaterialFX**
  - *successor to the already available JFoenix library, which is a bit old and has a lot of issues*
  - <https://github.com/palexdev/MaterialFX>
- **controlsfx**
  - <http://fxexperience.com/controlsfx/>
- **ValidatorFX**
  - *inspired by ControlsFX but tries to overcome its shortcomings*
  - <https://github.com/effad/ValidatorFX>
- <http://aalmiray.github.io/ikonli/>
- <https://github.com/schlegel11/JFXAnimation>
- <https://github.com/Typhon0/AnimateFX>
- <https://github.com/iamgio/animated>
- <https://github.com/HanSolo/tilesfx> - *A JavaFX library containing tiles for Dashboards*
- <https://github.com/miho/ScaledFX>
- **GemsFX**
  - <https://github.com/dlsc-software-consulting-gmbh/GemsFX>
  - *A collection of JavaFX controls and utilities.*
- <https://github.com/dustinkredmond/FXTrayIcon>
- **medusa**
  - *A JavaFX library for Gauges*
  - <https://github.com/HanSolo/Medusa>
- **formsfx**
  - fluent builder für Forms
  - <https://github.com/dlsc-software-consulting-gmbh/FormsFX>
- **charts**
  - <https://github.com/HanSolo/charts>
- **Flowless**
  - *layout container that lays out cells in a vertical or horizontal flow*
  - *only the currently visible cells are rendered in the scene. You may have a list of thousands of items, but only, say, 30 cells are rendered at any given time.*
  - *You will benefit from Flowless (compared to ListView) the most if you have many add/delete items occuring in the viewport and an expensive updateItem method.*
  - <https://github.com/FXMisc/Flowless>
- **AtlantaFX**
  - <https://github.com/mkpaz/atlantafx> 
  - *Modern JavaFX CSS theme collection with additional controls*


#### diverse
- <https://github.com/ReactiveX/RxJavaFX>
- **ReactFX**
  - <https://github.com/TomasMikula/ReactFX> 
  - *Reactive event streams, observable values and more for JavaFX*
- <https://github.com/TomasMikula/EasyBind>
- **lib-i18n**
  - <https://github.com/Naoghuman/lib-i18n/>
  - *allows a developer to bind a key-value pair of a .properties file to a StringBinding. This makes it very easy to change the language during runtime in a JavaFX application.*
- **jfxtras**
  - *A supporting library for JavaFX, containing helper classes, extended layouts, controls and other interesting widgets.*
  - <https://github.com/JFXtras/jfxtras>
  - <http://jfxtras.org/>
  - <https://github.com/JFXtras/jfxtras-labs>
  - pojo -> observable adapater
- **EasyFXML**
  - *opinionated set of tools aiming to simplify development of robust and modular JavaFX applications*
  - *project is divided in multiple modules* (docker, native, junit, mvc)
  - <https://github.com/Tristan971/EasyFXML> (ARCHIVED)
- **PreferencesFX**
  - *A framework for easily creating a UI for application settings / preferences.*
  - <https://github.com/dlsc-software-consulting-gmbh/PreferencesFX>


### Test
- **TestFX**
  - <https://github.com/TestFX/TestFX> *600
  - headless oder headed
  - *Simple robots to simulate user interactions*
  - Integrationen für junit, spock


### mit Spring
- <https://spring.io/blog/2019/01/16/spring-tips-javafx>
- <https://github.com/roskenet/springboot-javafx-support>
- <http://www.greggbolinger.com/let-spring-be-your-javafx-controller-factory/>
- <https://www.youtube.com/watch?v=Lse51SpfKHo>


### Tipps
- Listener wieder entfernen, sonst memory leaks


## SnapKit
- *tools for creating rich Java Client applications that achieve the original promise of Java by running pixel-perfect and native on the desktop and in the browser*
- *comparatively small and simple, light-weight and performant. When compiled to the browser (via TeaVM), many apps are only 1 MB in size.*
- <https://github.com/reportmill/SnapKit>
