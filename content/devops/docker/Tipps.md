---
tags: [Notebooks/Docker]
title: Tipps
created: '2020-03-09T14:21:51.109Z'
modified: '2021-04-03T10:55:43.836Z'
parent: Docker
grand_parent: DevOps
---

# Tipps
- <https://github.com/wsargent/docker-cheat-sheet>
- in Shell starten
  `docker run --entrypoint /bin/sh -it`
- IP-Adresse des (Windows-)Host bekommen
  `getent hosts docker.for.win.localhost | cut -d ' ' -f1`
  oder
  `getent hosts host.docker.internal | cut -d ' ' -f1`
- Container (einschl. beendet) auflisten
  `docker ps -a`
- Images mit `<none>` löschen
  `docker rmi $(docker images --filter="dangling=true" -q)`
- alte Images löschen
  `docker rmi $(docker images | grep -E "months ago|years ago")`
- *processes in containers should not be run as root*
- File aus einem Image zum Host kopieren (?)
  `docker cp $(docker create <image>:latest):/path/in/image /path/in/host`
- *Anywhere that you find a command that takes container ID, you only need to specify as much of the ID as makes it unique (so "616abcde" could just "616" usually). You could specify the full container name if you'd like, e.g. wonderful_davinci. If you prefer using the name, then you should probably assign a name by yourself at run time (`docker run --name foo`)*
- *Changes to a service can be applied in-place, so for example, if you have 5 tasks running in a service and need two extra tasks, you can change your docker-compose.yml, then rerun `docker stack deploy` and you will only modify two tasks instead of recreating the original five.*
- *put the commands that will change least frequently at the top of your Dockerfile so that you can cache layers (and then reuse the cached layers) for as long as possible.*
