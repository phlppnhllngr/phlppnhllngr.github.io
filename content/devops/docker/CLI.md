---
title: CLI
parent: Docker
grand_parent: DevOps
---

# CLI
- <https://docs.docker.com/engine/reference/commandline/docker/>
- **attach**
  - *attach your terminal’s standard input, output, and error (or any combination of the three) to a running container*
- **builder**
  - prune
    - Löscht den Build-Cache 
    - `docker builder prune --all --force`  
- **compose**
  - *The new Compose V2, which supports the compose command as part of the Docker CLI, is now available.*
  - *Run docker compose up and the Docker compose command starts and runs your entire app. You can alternatively run docker-compose up using Compose standalone (docker-compose binary).*
  - <https://docs.docker.com/compose/reference/>
  - -> Docker/Tools/compose
- **events**
  - *get real-time events from the server*
  - Event Types
    - Container
      - destroy
        - Bsp.: `Event(status=destroy, id=979b980d62202d9287d7a8479a233d36665fb55da456ac0bb442c03475ca1130, from=busybox, node=null, type=CONTAINER, action=destroy, actor=EventActor(id=979b980d62202d9287d7a8479a233d36665fb55da456ac0bb442c03475ca1130, attributes={image=busybox, name=busybox}), time=1691273991, timeNano=1691273991571197700)` 
      - die
        - Ein Container, der von "innen" gestoppt wird (`exit`), feuert das Event "die"
        - Bsp.: `Event(status=die, id=979b980d62202d9287d7a8479a233d36665fb55da456ac0bb442c03475ca1130, from=busybox, node=null, type=CONTAINER, action=die, actor=EventActor(id=979b980d62202d9287d7a8479a233d36665fb55da456ac0bb442c03475ca1130, attributes={execDuration=6, exitCode=137, image=busybox, name=busybox}), time=1691273991, timeNano=1691273991469248300)`
      - exec_die
        - Durch Ausführung des Health-Check-Commands wird ein exec_die-Event gefeuert, inkl. Angabe über den Exit-Code 
      - health_status
      - kill
        - Ein Container, der via `docker stop` gestoppt wird, feuert die Events `kill (signal=15)`, `kill (signal=9)`, `stop`, `die (attributes={exitCode=<number>})`
        - Ein Container, der via `docker kill` gestoppt wird, feuert die Events `kill (signal=9)`, `die`
        - Bsp.: `Event(status=kill, id=979b980d62202d9287d7a8479a233d36665fb55da456ac0bb442c03475ca1130, from=busybox, node=null, type=CONTAINER, action=kill, actor=EventActor(id=979b980d62202d9287d7a8479a233d36665fb55da456ac0bb442c03475ca1130, attributes={image=busybox, name=busybox, signal=9}), time=1691273990, timeNano=1691273990522381600)`
      - oom
      - pause
      - stop
      - ...  
  - <https://docs.docker.com/engine/reference/commandline/events/>
  - <https://dev.to/themreza/monitoring-and-logging-docker-events-59oi>
- **exec**
  - `docker exec -it <name/id> /bin/sh`
  - "Inline": `docker exec <name/id> /bin/sh -c "echo $HOME"`
- **history**
  - *Show the history of an image* 
  - <https://docs.docker.com/engine/reference/commandline/history/>
- **image**
  - ls
- **inspect**
  - *provides detailed information on constructs controlled by Docker* 
  - <https://docs.docker.com/engine/reference/commandline/inspect/>
- **logs**
  - `docker logs <name/id>`
- **ps**
  - alias `container ls` 
  - `--all`
  - `--filter`
  - `--format`
    - nur best. Spalten ausgeben, Zeilen als Liste: `docker ps --size --format '{{.Names}} {{.Size}}'`
    - nur best. Spalten ausgeben, Zeilen tabellarisch: `docker ps --size --format 'table {{.Names}}\t{{.Size}}'` 
  - `--size | -s`
    - Wie "all", mit zusätzl. Spalte "SIZE": `178MB (virtual 1.07GB)`
    - *describe the amount of disk space used by a container*
    - *When starting a container, the image that the container is started from is mounted read-only. On top of that, a writable layer is mounted, in which any changes made to the container are written. The read-only layers of an image can be shared between any container that is started from the same image, whereas the "writable" layer is unique per container*
    - size = disk size of writable layer
    - virtual = the combined size of the readonly layer (the image), and the writable layer of the container
    - *Things that are not included currently are: volumes, disk space used for the container's configuration files, memory written to disk (if swap is enabled)* (<https://docs.docker.com/engine/storage/drivers/#container-size-on-disk>)
    - <https://docs.docker.com/reference/cli/docker/container/ls/#size>
  - <https://docs.docker.com/reference/cli/docker/container/ls/>
- **pause**
  - *suspends all the processes for an indefinite time*
  - *consumes the same memory used while running the container, but the CPU is released completely*
- **run**
  - <https://docs.docker.com/engine/reference/run/>
  - *Four of the Dockerfile commands cannot be overridden at runtime: FROM, MAINTAINER, RUN, and ADD. Everything else has a corresponding override in docker run.* 
  - `docker run --rm --name=<container-name> <image>`
  - `-v`
    - bind mount: relative Pfade nicht möglich (docker-compose: ja); Abhilfe: `%CD%` (Windows/cmd) bzw. `${pwd}` (powershell) oder `$PWD` (Linux)
    - → Docker/Storage
  - `--memory`
    - <https://docs.docker.com/config/containers/resource_constraints/#limit-a-containers-access-to-memory> 
  - `--memory-swap`
    - *Operating systems use swap space to create the so called virtual memory (which is obviously bigger then the RAM you might have).* 
    - *If `--memory-swap` is set to the same value as `--memory`, and `--memory` is set to a positive integer, the container does not have access to swap*
    - *By specifying `--memory=20m` and `--memory-swap=30m` we allow 10 MB of swap.*
    - *The best you'll get out of an HDD right now is 150 MB/s. The maximum speed of transfer of an SSD is 600 MB/s, as that is the max speed of a SATA3 connection. They are usually slower than this though. The maximum speed of transfer of DDR3-800 RAM is 6400 MB/s (so the slowest DDR3 RAM around). These are all approximate and handwavy. However, while an SSD is quicker, HDD is 2% of RAM transfer rate, and SSD at its very best is 9% of RAM transfer rate.*
    - <https://docs.docker.com/config/containers/resource_constraints/#--memory-swap-details>
  - `--memory-reservation`
    - *is softlimit for the memory when docker detects there isn't enough memory*
    - *it will decrease the memory till the reservation limit is hit. (That's why it has to be smaller than the memory flag)*
    - *upper bound is `--memory` and lower bound is `--memory-reservation`.*
- **system**
  - <u>prune</u>
    - *Remove all unused [stopped] containers, networks, images (both dangling and unreferenced), and optionally, volumes.*
    - `docker system prune --all --volumes --force`
    - Optionen
      - `--all`
        - *Remove all unused images not just dangling ones*
        - *An unused image means that it has not been assigned or used in a container. For example, when running docker ps -a - it will list all of your exited and currently running containers. Any images shown being used inside any of containers are a "used image".*
        - *a dangling image just means that you've created the new build of the image, but it wasn't given a new name. So the old images you have becomes the "dangling image". Those old image are the ones that are untagged and displays "<none>" on its name when you run docker images.*
      - `--force`
        - *Do not prompt for confirmation* 
      - `--volumes`
        - *Prune volumes*
        - löscht aber nicht alle ungenutzten Volumes --> `docker volume prune --all`
      - `--filter`  
    - <https://docs.docker.com/engine/reference/commandline/system_prune/>
  - <u>df</u>
    - *displays information regarding the amount of disk space used by the Docker daemon*
    - ```
      TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
      Images          14        14        6.911GB   85.23MB (1%)
      Containers      19        19        6.876GB   0B (0%)
      Local Volumes   12        9         4.514GB   2.774GB (61%)
      Build Cache     0         0         0B        0B
      ```
    - `--verbose | -v`
      - Zeigt einzelne Größen aller Images, Container und Volumes an
    - <https://docs.docker.com/reference/cli/docker/system/df/> 
- **volume**
    - create
        - driver
            - local
              - Bsp. CIFS:
                ```
                  docker volume create --driver local --opt type=cifs --opt device="//192.169.0.0/foo/bar" --opt o=username=user,password=password,vers=3.0,noperm,iocharset=utf8 cifs_volume
                  docker run -i --rm -v cifs_volume:/mnt busybox ls -l /mnt
                ```
        - <https://docs.docker.com/engine/reference/commandline/volume_create/>
    - prune
      - Optionen
        - --all
        - --force  
    - <https://docs.docker.com/storage/volumes/>
