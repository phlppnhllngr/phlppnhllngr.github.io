---
tags: [Notebooks/Docker]
title: CLI
created: '2020-08-29T16:59:31.019Z'
modified: '2021-07-19T08:13:11.037Z'
parent: Docker
grand_parent: DevOps
---

# CLI
- **run**
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
- **attach**
  - *attach your terminal’s standard input, output, and error (or any combination of the three) to a running container*
- **exec**
  - `docker exec -it <name/id> /bin/bash`
- **logs**
  - `docker logs <name/id>`
