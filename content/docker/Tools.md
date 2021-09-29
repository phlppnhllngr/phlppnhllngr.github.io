---
tags: [Notebooks, Notebooks/Docker]
title: Tools
created: '2019-02-14T20:19:00.854Z'
modified: '2021-09-13T13:38:11.554Z'
parent: Docker
---

# Tools
[https://github.com/veggiemonk/awesome-docker]()

- **compose**
  - https://github.com/docker/awesome-compose
  - compose-file v2: [https://docs.docker.com/compose/compose-file/compose-file-v2/]()
  - compose-file v3: [https://docs.docker.com/compose/compose-file/]()
  - extending: https://docs.docker.com/compose/extends/
- **Composerize**
  - *Turns docker run commands into docker-compose files*
  - https://github.com/magicmark/composerize
- **dive**
  - siehe auch `docker image history`
  - *tool for exploring a docker image, layer contents, and discovering ways to shrink your Docker image size*
  - zeigt die Dockerfile-Zeilen und die daraus resultierenden Dateisystem-Zustände (als Tree), inkl. Dateigrößen
  - https://github.com/wagoodman/dive ⭐17k
  - erhältlich als Binary oder Docker image
- **jib**
  - *builds optimized Docker images for your Java applications without a Docker daemon - and without deep mastery of Docker best-practices. Available as plugins for Maven and Gradle and as a Java library.*
  - *Jib gives you the opportunity to build docker images: without a docker daemon running (CI and so on), with reproducible builds (which is also a big plus for cache friendliness), that are layered in a way so that you usually just need to push and pull your own code but not libraries or other resources because everything else is cached, with very little configuration needed, with lots of possibilities to configure stuff*
  - *The advantage of jib is that your dependencies are a separate layer to your application code, so the amount of data required to move around when deploying new releases is much smaller.*
  - https://github.com/GoogleContainerTools/jib/
  - https://www.reddit.com/r/java/comments/huivgu/customize_the_container_build_plan_prepared_by/
  - Extensions
    - https://github.com/GoogleContainerTools/jib-extensions
    - jib-native-image-extension-maven
    - ...
- **docker-slim**
  - https://github.com/docker-slim/docker-slim ⭐8.7k
  - *Don't change anything in your Docker container image and minify it by up to 30x (and for compiled languages even more) making it secure too!*
  Node.js application images: from node:alpine - 66.7MB => 34.7MB (minified by 1.92X)
  JAVA application images: from ubuntu:14.04 - 743.6 MB => 100.3 MB
- **Watchtower**
  - https://github.com/containrrr/watchtower
  - *application that will monitor your running Docker containers and watch for changes to the images that those containers were originally started from. If watchtower detects that an image has changed, it will automatically restart the container using the new image.*
- **tini**
  - https://github.com/krallin/tini ⭐3.7k
  - *init for containers*
  - Vorteile: https://github.com/krallin/tini/issues/8
- **slim**
  - https://github.com/ottomatica/slim 
  - *Build and run tiny vms from Dockerfiles*
- **hadolint**
  - [https://github.com/hadolint/hadolint]()
  - Dockerfile Linter
  - als CLI oder Docker image verfügbar
- **buildkit**
  - *BuildKit has been integrated to docker build since Docker 18.06*
  - https://github.com/moby/buildkit
  - https://docs.docker.com/develop/develop-images/build_enhancements/
- **buildpacks**
  - buildpacks.io
  - *transform your application source code into images that can run on any cloud*


## GUIs
- docker-desktop
  - [https://www.docker.com/products/docker-desktop]()
  - mit Kubernetes-Support (single node cluster)
  - *free for small businesses (fewer than 250 employees AND less than $10 million in annual revenue), personal use, education, and non-commercial open source projects*
- portainer
  - https://www.portainer.io/
- dockstation.io
  - https://dockstation.io/
- kitematic
  - https://github.com/docker/kitematic/ ⭐11k


## Orchestrierung
- Kubernetes (k8s)
  - https://dev.to/sandrogiacom/kubernetes-for-java-developers-setup-41nk (minikube, kubectl, virtualbox)
- Rancher  
  - https://github.com/rancher/rancher
- harbormaster
  - *small utility that lets you easily deploy multiple Docker-Compose applications. It does this by taking a list of git repository URLs that contain Docker Compose files and running the Compose apps they contain. It will also handle updating/restarting the apps when the repositories change*
  - https://gitlab.com/stavros/harbormaster
