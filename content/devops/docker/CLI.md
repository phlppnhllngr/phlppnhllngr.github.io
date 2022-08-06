---
tags: [Notebooks/Docker]
title: CLI
created: '2020-08-29T16:59:31.019Z'
modified: '2021-07-19T08:13:11.037Z'
parent: Docker
grand_parent: DevOps
---

# CLI
- <https://docs.docker.com/engine/reference/commandline/docker/>
- **attach**
  - *attach your terminal’s standard input, output, and error (or any combination of the three) to a running container*
- **compose**
  - *The new Compose V2, which supports the compose command as part of the Docker CLI, is now available.*
  - *Run docker compose up and the Docker compose command starts and runs your entire app. You can alternatively run docker-compose up using Compose standalone (docker-compose binary).*
  - <https://docs.docker.com/compose/reference/>
- **events**
  - *get real-time events from the server* 
  - <https://docs.docker.com/engine/reference/commandline/events/> 
- **exec**
  - `docker exec -it <name/id> /bin/bash`
- **history**
  - *Show the history of an image* 
  - <https://docs.docker.com/engine/reference/commandline/history/> 
- **inspect**
  - *provides detailed information on constructs controlled by Docker* 
  - <https://docs.docker.com/engine/reference/commandline/inspect/>
- **logs**
  - `docker logs <name/id>`
- **run**
  - <https://docs.docker.com/engine/reference/run/>
  - *Four of the Dockerfile commands cannot be overridden at runtime: FROM, MAINTAINER, RUN, and ADD. Everything else has a corresponding override in docker run.* 
  - `docker run --rm --name=<container-name> <image>`
  - `-v`
    - relative Pfade nicht möglich (docker-compose: ja); Abhilfe: `%CD%` (Windows/cmd) bzw. `${pwd}` (powershell) oder `$PWD` (Linux)
    - volume-Varianten
      - → Docker/Storage
      - bind mount ("host voulume")
        - `-v /host/path/:/container/path`
      - managed
        - unnamed (anonymous) managed
          - `-v /container/path/`
          - *create a volume on the host system at a location owned by the docker daemon and mount it in the container at /container/path*
          - im Host (automatisch erzeugt) unter `/var/lib/docker/volumes/<random-hash>/_data`
          - *To find out where docker created the volume on host:* {% raw %} `docker inspect -f "{{.Mounts}}" <ContainerName>` {% endraw %}
        - named managed
          - `-v <name>:/container/path`
          - *Same as previous, only instead of volume being assigned a hash, you can provide it with a meaningful name*
