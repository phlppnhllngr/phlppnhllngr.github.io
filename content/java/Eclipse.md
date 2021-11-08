---
tags: [Notebooks/Java]
title: Eclipse
created: '2019-10-18T22:17:52.957Z'
modified: '2021-06-08T13:23:53.232Z'
parent: Java
---

# Eclipse

## Plugins

- ~~Indent Guide~~ siehe Konfig/whitespace
- **Ansi escape in console**
  - *interprets the ANSI escape sequences to color the console output*
  - https://marketplace.eclipse.org/content/ansi-escape-console
- **Grep Console**
    - optische Hervorhebung von Logs mit konfigurierbaren Regex
    - Defaults funktionieren nicht; z.B. stattdessen `Expression = ^WARN.*$`
    - für neue Eclipse-Versionen nicht verfügbar (kann es aber noch über die Update-site bekommen: http://eclipse.schedenig.name)
    - Alternative: LogViewer? → nur für Files
    - Alternative: ~~Easy Consoler Grepper?~~
- **Checkstyle** <small>→ siehe auch m2e-code-quality</small>
- **SpotBugs** <small>→ siehe auch m2e-code-quality</small>
- **SonarLint**
- **Enhanced Class Decompiler**
- **Lombok**
- **Buildship Gradle**
- **Spring Tools**
- **YEdit** (yaml-Editor)
- **Eclipse Docker Tooling**
- ~~jdt codemining~~
  - ~~https://github.com/angelozerr/jdt-codemining~~
- **pmd** <small>→ siehe auch m2e-code-quality</small>
- **infinitest**
  - https://infinitest.github.io/
  - https://github.com/infinitest/infinitest/
  - continuous testing, watch mode
- **exporter for eclipse**
  - aka Yatta Profiles aka Yatta Eclipse Launcher aka Yatta Eclipse Exporter
  - *easy way to save your Eclipse setups and Workspace configurations – for yourself or your team*
  - *Export your Eclipse configuration, installed plug-ins, workspace settings and project configuration quickly and easily to a single local file*
  - https://marketplace.eclipse.org/content/exporter-eclipse
  - https://www.yatta.de/profiles/
- **memory analyzer (MAT)**
  - erstellt und analysiert Heap-dumps ('hprof') und stellt grafisch dar, versucht Memory-Leaks zu erkennen
- **jar2uml**
- **unnecessary code detector (UCD)**
- **wildwebdeveloper**
  - https://github.com/eclipse/wildwebdeveloper
- **spring sts**
  - https://spring.io/tools
- **IBM WebSphere Application Server V9.x Developer Tools**
  - unterstützte Versionen von Eclipse: nicht neuer als 2020-06
  - die deployten Files sind unter `<Eclipse-Workspace>/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/`:
  ```
  |-module_URI_mapping
  |-NameWebmodul1
      |-WEB-INF
          |-classes/
          |-lib/
          |-web.xml
          |-ibm-web-ext.xml
          |-ibm-web-bnd.xml
      |-META-INF/
  |-NameWebmodul2
  ```
  - `Server > Clean` leert tmp0
  - Deployment Assembly (Rechtsklick > Properties > Deployment Assembly) bestimmt die Verzeichnisstruktur innerhalb tmp0. Konfigurierbar für Gesamtprojekt und je Modul. Die Struktur wird sichtbar, sobald das Publishing des Servers abgeschlossen ist.
  - Beispiel-Deployment-Assembly in einem Maven-Projekt mit Web-Modul und Jar-Modul, wobei das Jar-Modul eine (Workspace-)Abhängigkeit des Web-Moduls ist:
    <table>
      <tr>
        <th>Quelle</th>
        <th>Ziel</th>
      </tr>
      <tr>
        <th>Gesamtprojekt/Parent:</th>
        <th></th>
      </tr>
      <tr>
        <td>/</td>
        <td>/</td>
      </tr>
      <tr>
        <td>webModule (Project)</td>
        <td>webModule.war</td>
      </tr>
      <tr>
        <td>jarModule</td>
        <td>lib/jarModule.jar (notwendig?)</td>
      </tr>
      <tr>
        <th>Webmodul:</th>
        <th></th>
      </tr>
      <tr>
        <td>src/main (java,resources)</td>
        <td>WEB-INF/classes</td>
      </tr>
      <tr>
        <td>src/main/webapp (WEB-INF,META-INF)</td>
        <td>/</td>
      </tr>
      <tr>
        <td>Maven dependencies</td>
        <td>WEB-INF/lib</td>
      </tr>
      <tr>
        <td>jarModule</td>
        <td>WEB-INF/lib/jarModule.jar</td>
      </tr>
    </table>
  - [https://marketplace.eclipse.org/content/ibm-websphere-application-server-v9x-developer-tools](https://marketplace.eclipse.org/content/ibm-websphere-application-server-v9x-developer-tools)


### m2e
- https://www.eclipse.org/m2e/index.html
- [default lifecycle mapping: lifecycle-mapping-metadata.xml](https://github.com/eclipse/m2e-core/blob/master/org.eclipse.m2e.lifecyclemapping.defaults/lifecycle-mapping-metadata.xml)
- "plugin execution not covered by lifecycle configuration":
  [https://www.eclipse.org/m2e/documentation/m2e-execution-not-covered.html](https://www.eclipse.org/m2e/documentation/m2e-execution-not-covered.html)
- in Eclipse den Lifecycle eines Projekts sehen: Properties → Maven → Lifecycle
- **m2e-apt** 
  - *aims at providing automatic Annotation Processing configuration in Eclipse, based on your project's pom.xml and its classpath dependencies*
- **m2e-code-quality**
  - [https://github.com/m2e-code-quality/m2e-code-quality](https://github.com/m2e-code-quality/m2e-code-quality)
  - nicht (mehr) im Marktplatz; Update site: [http://m2e-code-quality.github.io/m2e-code-quality/](http://m2e-code-quality.github.io/m2e-code-quality/)
  - *collection of Eclipse plugins for M2Eclipse that carry configuration from the Checkstyle, FindBugs and PMD Maven plugins to their corresponding Eclipse plugins* (und SpotBugs)
  - installiert alle diese Plugins
  - an den Eclipse-Plugins sollte dann nichts weiter konfiguriert werden müssen (zumindest nicht der Dateipfad zu den Checkstyle-Regeln)
    ```xml
    <project>
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-checkstyle-plugin</artifactId>
            <version>3.1.0</version>
            <!-- This version of the plugin uses Checkstyle 8.19 by default and requires 
            Java 8. But you can upgrade the version used at runtime. -->
            <!-- die Version muss wohl zwangsläufig mit der des Eclipse-Plugins übereinstimmen 
            (m2e-code-quality) -->
            <!--<dependencies> <dependency> <groupId>com.puppycrawl.tools</groupId> 
            <artifactId>checkstyle</artifactId> <version>8.25</version> </dependency> 
            </dependencies> -->
            <configuration>
            <encoding>UTF-8</encoding>
            <configLocation>checkstyle.xml</configLocation>
            <consoleOutput>true</consoleOutput>
            <failsOnError>false</failsOnError>
            </configuration>
            <executions>
              <execution>
                <id>checkstyle</id>
                <phase>validate</phase>
                <goals>
                  <goal>checkstyle</goal>
                </goals>
              </execution>
            </executions>
          </plugin>
        </plugins>
      </build>
    </project>
    ```


## Konfig
- eclipse.ini
  - -Xms512m
- General.Workspace → Text file encoding = UTF-8
- General.Editors.Text Editors → Show whitespace characters
- Java.Editor.Save Actions → Organize Imports + Additional actions
- Java.Debug.Step Filtering → Use step filters (Code beim Debuggen ausschließen)
- Run/Debug.Console.Limit Console Output → unchecked
- Font
  - [https://github.com/tonsky/FiraCode](https://github.com/tonsky/FiraCode)
  - [https://github.com/be5invis/Iosevka](https://github.com/be5invis/Iosevka)


## Rechtschreibprüfung
- in 'preferences' konfigurierbar (text editor → spelling)
- für deutsch: user dict = /pfad/zur/datei (Vorsicht: keine .dic-Datei mit /* am Ende der Wörter),
in diese Datei werden auch die in Eclipse manuell hinzugefügten gespeichert
- nicht konfigurierbar
