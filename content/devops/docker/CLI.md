---
title: CLI
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
  - -> Docker/Tools/compose
- **events**
  - *get real-time events from the server* 
  - <https://docs.docker.com/engine/reference/commandline/events/> 
- **exec**
  - `docker exec -it <name/id> /bin/sh`
  - "Inline": `docker exec <name/id> /bin/sh -c "echo $HOME"`
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
    - bind mount: relative Pfade nicht möglich (docker-compose: ja); Abhilfe: `%CD%` (Windows/cmd) bzw. `${pwd}` (powershell) oder `$PWD` (Linux)
    - → Docker/Storage
- **volume**
    - create
        - driver
            - local
        - <https://docs.docker.com/engine/reference/commandline/volume_create/>
    - <https://docs.docker.com/storage/volumes/>
