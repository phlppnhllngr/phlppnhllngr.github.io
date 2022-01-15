---
tags: [Notebooks/Docker]
title: Images - Varianten
created: '2019-02-14T20:19:30.421Z'
modified: '2021-04-02T14:37:12.937Z'
parent: Docker
---

# Images - Varianten
- **scratch**
  - ```FROM scratch```
  - *This image is most useful in the context of building base images or super minimal images that contain only a single binary and whatever it requires*
  - Image enthält <u>nichts</u>. Funktioniert trotzdem, da jede Container-Instance ein "root filesystem (rootfs)" vom Host bekommt (/etc, /proc, ... aber z.B. keine Shell)
- **slim**
  - headless, ohne Entwicklungstools
- **alpine**
  - 4 MB
  - *Alpine Linux is a security-oriented, lightweight Linux distribution based on musl libc and busybox.*
  - Paketmanager: apk
- **ubuntu**
  - 120 MB
  - Paketmanager: apt
- **stretch**
- **buster**
- **debian**  
  - buster-slim
- **phusion**
  - 8 MB
  - https://github.com/phusion/baseimage-docker 
  - *...much more powerful than Busybox or Alpine. Baseimage-docker is a special Docker image that is configured for correct use within Docker containers. It is Ubuntu, plus: Modifications for Docker-friendliness. Administration tools that are especially useful in the context of Docker. Mechanisms for easily <mark>running multiple processes</mark>, without violating the Docker philosophy.*
- **Google distroless**
  - https://aboullaite.me/docker-distroless-image/
  - https://github.com/GoogleContainerTools/distroless *5.5k
  - *"Distroless" images contain only your application and its runtime dependencies. They <mark>don’t contain any programs like shells and package managers</mark> usually found in a Linux distribution.*
  - Images für Java, Nodejs, ...

**Microsoft**
- <mark>Um Windows-Container zu nutzen, muss man in Docker für Windows 'switch to windows containers' auswählen und dann Docker neu starten</mark>
- nur mit Windows-Host möglich & nicht jede Image-Version passt zu jeder Host-Windows-Version
- https://docs.microsoft.com/en-us/virtualization/windowscontainers/quick-start/run-your-first-container
- https://hub.docker.com/u/microsoft/
- alle auch mit 'insider'-Variante
- Windows
  - https://hub.docker.com/_/microsoft-windows
  - ~20 GB
- server core
  - https://hub.docker.com/_/microsoft-windows-servercore
- nano server
  - https://hub.docker.com/_/microsoft-windows-nanoserver
  - ~260MB
  - *Windows Server Core and Nanoserver are the most common base images to target. The key difference between these images is that Nanoserver has a significantly smaller API surface. **PowerShell, WMI, and the Windows servicing stack are absent from the Nanoserver image.** Nanoserver was built to provide just enough API surface to run apps that have a dependency on .NET core or other modern open source frameworks. As a tradeoff to the smaller APi surface, the Nanoserver image has a significantly smaller on-disk footprint than the rest of the Windows base images.*
  - → powershell:nanoserver-Varianten?
- powershell
  - latest (23.03.2021) ~6GB
  - Varianten
    - nanoserver
      - ~500MB
    - servercore
      - 1809 → 2018/09, 2004 → 2020/04
      - ~6GB
    - linux
  - https://hub.docker.com/_/microsoft-powershell
  - https://github.com/PowerShell/PowerShell-Docker
- dotnet-framework
  - https://hub.docker.com/_/microsoft-dotnet-framework
  - https://github.com/microsoft/dotnet-framework-docker
  - Varianten
    - mcr.microsoft.com/dotnet/framework/sdk
      ~ 9GB
- dotnet
  - https://hub.docker.com/_/microsoft-dotnet
- Community
  - diverse
    - https://github.com/StefanScherer/dockerfiles-windows
      - Dockerfiles für alle möglichen Sprachen, Frameworks, ...
  - Java
    - https://hub.docker.com/r/winamd64/openjdk/
    - https://hub.docker.com/_/openjdk/?tab=tags&page=1&name=windows
    - https://github.com/carlossg/docker-maven

**MacOS**
- Docker-OSX
  - https://github.com/sickcodes/Docker-OSX
  - *Run Mac in a Docker! Run near native OSX-KVM in Docker! X11 Forwarding! CI/CD for OS X!*
  - Stand 03/21 nicht mit Windows (WSL2) möglich (https://github.com/sickcodes/Docker-OSX/issues/37)

**Android**
- Waydroid
  - *A container-based approach to boot a full Android system on a regular GNU/Linux system like Ubuntu.*
  - <https://waydro.id/>
- Anbox
  - <https://github.com/anbox/anbox>
- ReDroid
  - <https://github.com/remote-android/redroid-doc#overview>