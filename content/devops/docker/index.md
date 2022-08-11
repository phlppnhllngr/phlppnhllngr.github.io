---
layout: default
title: Docker
has_children: true
parent: DevOps
---

# Docker
- <https://tomgregory.com/running-docker-in-docker-on-windows/>

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


## für GUI Apps
- <https://dev.to/darksmile92/run-gui-app-in-linux-docker-container-on-windows-host-4kde>
- <https://news.ycombinator.com/item?id=30810410>
- Linux host: xvfb, xorg
- Windows host: VcXsrv → Diverses/Diverse Software
