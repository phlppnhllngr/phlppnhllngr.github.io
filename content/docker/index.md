---
layout: default
title: Docker
has_children: true
---

# Docker

## Container allgemein
- *a way to package applications with with [their] dependencies and configuration*
- *portable artifact easily shared and moved around*
- *Image layers: OS, application, configuration*
- *OS: Applications Layer > Kernel Layer > Hardware*
- **VM**
    - *virtualizes complete OS; both applications layer & kernel; does not use host kernel*
    - *can run any OS on any host OS*
- **Container**
    - *virtualizes only applications layer on top of host kernel*
    - *smaller in size, faster startup*


## GUI Apps
- <https://dev.to/darksmile92/run-gui-app-in-linux-docker-container-on-windows-host-4kde>
- <https://news.ycombinator.com/item?id=30810410>
- Linux host: xvfb, xorg
- Windows host: VcXsrv → Diverses/Diverse Software


## Alternativen
- **minikube**
    - → DevOps/Kubernetes
    - *the only tool that is a drop-in replacement for Docker Desktop. The other tools [kind, microk8s, or k3s] require a Linux distribution, which makes them a non-starter on macOS or Windows* (<https://matt-rickard.com/docker-desktop-alternatives/>)
- **Podman**
    - *Podman is a daemonless container engine for developing, managing, and running OCI Containers on your Linux System. Containers can either be run as root or in rootless mode. Simply put: alias docker=podman.*
    - *podman is an alternative to Docker, but get mentioned as a replacement for the Docker component (not Kubernetes) of Docker Desktop.*
    - https://podman.io/>
    - <https://github.com/containers/podman> *8k
- **containerd**
    - *An open and reliable container runtime*
    - <https://github.com/containerd/containerd>
    - nerdctl
        - *Docker-compatible CLI for containerd*
        - <https://github.com/containerd/nerdctl>