---
tags: [Notebooks, Notebooks/Docker]
title: Tools
created: '2019-02-14T20:19:00.854Z'
modified: '2021-09-13T13:38:11.554Z'
parent: Docker
grand_parent: DevOps
---

# Tools
<https://github.com/veggiemonk/awesome-docker>

- **compose**
  - <https://github.com/docker/awesome-compose>
  - compose-file v2: <https://docs.docker.com/compose/compose-file/compose-file-v2>
  - compose-file v3: <https://docs.docker.com/compose/compose-file>
  - extending: <https://docs.docker.com/compose/extends>
  - [HN - Docker Compose best practices for dev and prod, 08/22](https://news.ycombinator.com/item?id=32484008)
  - [HN - Best practices around creating production ready web apps with Docker Compose, 06/21](https://news.ycombinator.com/item?id=27359081)
- **Composerize**
  - *Turns docker run commands into docker-compose files*
  - <https://github.com/magicmark/composerize>
- **dive**
  - siehe auch `docker image history`
  - *tool for exploring a docker image, layer contents, and discovering ways to shrink your Docker image size*
  - zeigt die Dockerfile-Zeilen und die daraus resultierenden Dateisystem-Zustände (als Tree), inkl. Dateigrößen
  - <https://github.com/wagoodman/dive> <img loading="lazy" src="https://img.shields.io/github/stars/wagoodman/dive?style=flat-square"/>
  - erhältlich als Binary oder Docker image
- **jib**
  - *builds optimized Docker images for your Java applications without a Docker daemon - and without deep mastery of Docker best-practices. Available as plugins for Maven and Gradle and as a Java library.*
  - *Jib gives you the opportunity to build docker images: without a docker daemon running (CI and so on), with reproducible builds (which is also a big plus for cache friendliness), that are layered in a way so that you usually just need to push and pull your own code but not libraries or other resources because everything else is cached, with very little configuration needed, with lots of possibilities to configure stuff*
  - *The advantage of jib is that your dependencies are a separate layer to your application code, so the amount of data required to move around when deploying new releases is much smaller.*
  - <https://github.com/GoogleContainerTools/jib/>
  - <https://www.reddit.com/r/java/comments/huivgu/customize_the_container_build_plan_prepared_by/>
  - Extensions
    - <https://github.com/GoogleContainerTools/jib-extensions>
    - jib-native-image-extension-maven
    - ...
- **docker-slim**
  - <https://github.com/docker-slim/docker-slim> <img loading="lazy" src="https://img.shields.io/github/stars/docker-slim/docker-slim?style=flat-square"/>
  - *Don't change anything in your Docker container image and minify it by up to 30x (and for compiled languages even more) making it secure too!*
  Node.js application images: from node:alpine - 66.7MB => 34.7MB (minified by 1.92X)
  JAVA application images: from ubuntu:14.04 - 743.6 MB => 100.3 MB
- **Watchtower**
  - <https://github.com/containrrr/watchtower>
  - *application that will monitor your running Docker containers and watch for changes to the images that those containers were originally started from. If watchtower detects that an image has changed, it will automatically restart the container using the new image.*
- **tini**
  - <https://github.com/krallin/tini> <img loading="lazy" src="https://img.shields.io/github/stars/krallin/tini?style=flat-square"/>
  - *init for containers*
  - Vorteile: <https://github.com/krallin/tini/issues/8>
- **slim**
  - <https://github.com/ottomatica/slim>
  - *Build and run tiny vms from Dockerfiles*
- **hadolint**
  - <https://github.com/hadolint/hadolint> <img loading="lazy" src="https://img.shields.io/github/stars/hadolint/hadolint?style=flat-square"/>
  - Dockerfile Linter
  - als CLI, Docker-Image oder VSCode-Extension verfügbar
- **buildkit**
  - *BuildKit has been integrated to docker build since Docker 18.06*
  - <https://github.com/moby/buildkit>
  - <https://docs.docker.com/develop/develop-images/build_enhancements/>
- **buildpacks**
  - <https://buildpacks.io>
  - *transform your application source code into images that can run on any cloud*
- **syft**
  - *CLI tool and library for generating a Software Bill of Materials from container images and filesystems*
  - *Exceptional for vulnerability detection when used with a scanner tool like Grype.*
  - <https://github.com/anchore/syft>
- **harbormaster**
  - *small utility that lets you easily deploy multiple Docker-Compose applications. It does this by taking a list of git repository URLs that contain Docker Compose files and running the Compose apps they contain. It will also handle updating/restarting the apps when the repositories change*
  - <https://gitlab.com/stavros/harbormaster>
- **skopeo**
  - *Work with remote images registries - retrieving information, images, signing content*
  - *can perform operations which consist of: Inspecting a remote image showing its properties including its layers, without requiring you to pull the image to the host. (...)*
  - <https://github.com/containers/skopeo>
- **dozzle**
  - *Realtime log viewer for docker containers.*
  - <https://github.com/amir20/dozzle> <img loading="lazy" src="https://img.shields.io/github/stars/amir20/dozzle?style=flat-square"/>


## GUIs
- **docker-desktop**
  - <https://www.docker.com/products/docker-desktop>
  - mit Kubernetes-Support (single node cluster)
  - *free for small businesses (fewer than 250 employees AND less than $10 million in annual revenue), personal use, education, and non-commercial open source projects*
- **portainer**
  - <https://www.portainer.io/>
- **dockstation.io**
  - <https://dockstation.io/>
- **kitematic**
  - <https://github.com/docker/kitematic/> <img loading="lazy" src="https://img.shields.io/github/stars/docker/kitematic?style=flat-square"/>
- **lazydocker**
  - *A simple terminal UI for both docker and docker-compose*
  - <https://github.com/jesseduffield/lazydocker> <img loading="lazy" src="https://img.shields.io/github/stars/jesseduffield/lazydocker?style=flat-square"/>
- **Yacht**
  - *with a focus on templates and 1-click deployments*
  - <https://github.com/SelfhostedPro/Yacht>


## Security
- <https://blog.gitguardian.com/how-to-improve-your-docker-containers-security-cheat-sheet>
- <https://github.com/myugan/awesome-docker-security>
- **trivy**
  - CLI um Docker Images zu überprüfen
  - <https://github.com/knqyf263/trivy>
  - <https://foreops.com/blog/trivy-intro/> - *Container Scanning with Trivy in Jenkins*
- **docker-bench-security**
  - <https://github.com/docker/docker-bench-security> <img loading="lazy" src="https://img.shields.io/github/stars/docker/docker-bench-security?style=flat-square"/>
  - *script that checks for dozens of common best-practices around deploying Docker containers in production*
  - prüft keine Images, sondern Host
- **grype**
  - *A vulnerability scanner for container images and filesystems*
  - <https://github.com/anchore/grype>
