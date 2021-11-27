---
layout: default
title: Docker
has_children: true
---

# Docker

## GUI Apps
- <https://dev.to/darksmile92/run-gui-app-in-linux-docker-container-on-windows-host-4kde>
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