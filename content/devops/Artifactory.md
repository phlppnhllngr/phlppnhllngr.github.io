---
tags: [Notebooks/DevOps]
title: Artifactory
created: '2020-07-09T09:11:44.636Z'
modified: '2021-07-21T11:42:44.818Z'
parent: DevOps
---

# Artifactory
- **Installation**
    - Docker
        - [https://www.jfrog.com/confluence/display/JFROG/Installing+Artifactory#InstallingArtifactory-DockerInstallation](https://www.jfrog.com/confluence/display/JFROG/Installing+Artifactory#InstallingArtifactory-DockerInstallation)
- **REST-API**
    - [https://www.jfrog.com/confluence/display/JFROG/Artifactory+REST+API](https://www.jfrog.com/confluence/display/JFROG/Artifactory+REST+API)
    - Beispiele
      - Jar hochladen
        ```
        curl -XPUT "http://hostname:8081/artifactory/libs-release-local/foo/bar/baz/1.2.0/baz-1.2.0.jar" -T "target/baz-1.2.0.jar"
        ```
- **CLI**
    - [https://www.jfrog.com/confluence/display/CLI/CLI+for+JFrog+Artifactory](https://www.jfrog.com/confluence/display/CLI/CLI+for+JFrog+Artifactory)
- **mit Maven**
    - [https://www.jfrog.com/confluence/display/JFROG/Maven+Repository](https://www.jfrog.com/confluence/display/JFROG/Maven+Repository)
- **mit Jenkins (Plugin)**
    - [https://www.jfrog.com/confluence/display/JFROG/Jenkins+Artifactory+Plug-in](https://www.jfrog.com/confluence/display/JFROG/Jenkins+Artifactory+Plug-in)
