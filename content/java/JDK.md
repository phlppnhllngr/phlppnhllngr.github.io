---
tags: [Notebooks/Java]
title: JDK
created: '2019-02-21T16:00:15.322Z'
modified: '2021-07-29T06:10:52.572Z'
parent: Java
---

# JDK
<img src="https://opensource.com/sites/default/files/2022-03/jdk.jpg" loading="lazy"/><br/><br/>
- The Java Version Almanac - <https://javaalmanac.io/>
- <https://endoflife.date/java>

## Distributionen
- **OpenJDK**
    - Der Begriff meint zum einen das Open-Source-Repository mit dem Java-Quellcode, zum anderen die Distribution (Builds/Binaries) von Oracle (“Oracle OpenJDK”). Hier gibt es keinen Support und nach 6 Monaten (Release neue Version) keine weiteren Updates, auch nicht für "LTS"-Versionen (hierzu siehe unten).
- **OracleJDK**
    - OpenJDK mit ein paar Erweiterungen. Kostenpflichtig ab Java 12. Längerer Support für LTS-Versionen. Es gibt Lizenzen für Entwickler oder persönlichen Gebrauch, kommerzielle Verwendung ist hier aber ausgeschlossen.
    - LTS
        - *Oracle's stated opinion is that there's nothing special about LTS releases, and they merely correspond to an Oracle support product and should not be significant to anyone who is not a paying customer that buys support from Oracle.*
- **Andere OpenJDK Distributionen**
    - mit LTS-Support, zum Teil kostenpflichtig
    - Amazon Corretto (kostenlos, Updates für 8 bis 2023, 11 ab April 19 und bis 2024)
    - IBM
    - Red Hat
    - ~~AdoptOpenJDK~~ Adoptium
        - *The Adoptium Working Group promotes and supports (...) runtimes and associated technology for use across the Java ecosystem. <mark>Eclipse Temurin</mark> is the name of the OpenJDK distribution from Adoptium.* 
        - [https://adoptium.net/](https://adoptium.net/)
    - ...


## Upgrade guides
- [Oracle JDK Migration Guide](https://docs.oracle.com/en/java/javase/17/migrate/getting-started.html)
- <https://blogs.oracle.com/javamagazine/post/its-time-to-move-your-applications-to-java-17-heres-why-and-heres-how>
