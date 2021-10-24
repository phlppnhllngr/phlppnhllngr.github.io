---
tags: [Notebooks/DevOps]
title: Rancher
created: '2020-03-07T13:28:40.216Z'
modified: '2021-04-02T23:50:12.200Z'
parent: DevOps
---

# Rancher

## 1.6
- unterstützt docker-compose v1 & v2 (d.h. '2', '2.1' und neuer nicht)

### Installation (docker image)
- Tutorial: https://www.youtube.com/watch?v=7L6kgKHqPsI
- wichtig: GUI nicht mit `localhost:<port>` aufrufen, sondern über die IP-Adresse (ipconfig), wie im Tutorial, sonst funktioniert der 'network-services'-Stack nicht

### CLI
- *tool to manage the Rancher server from your command-line-interface. You can manage environments, hosts, stacks, services and containers.*
- https://rancher.com/docs/rancher/v1.6/en/cli/

### compose
- ["rancher-compose-cli" ist archived/deprecated](https://forums.rancher.com/t/rancher-cli-vs-rancher-compose/5811/3)
- *multi-host version of Docker Compose and will upload your docker-compose.yml and rancher-compose.yml to the Rancher server to deploy a new stack with the given configuration. This tool is ideal for CD pipelines*
- Download: https://www.pimwiddershoven.nl/entry/rancher-and-rancher-compose-command-line-tools
- https://rancher.com/docs/rancher/v1.6/en/cattle/adding-services/#adding-services-with-rancher-compose
- https://rancher.com/docs/rancher/v1.6/en/cattle/rancher-compose/commands/
- yml
  - *rancher-compose.yml which extends and overwrites the docker-compose.yml. For example, scale of services and health checks would be in the rancher-compose.yml file.*

