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
- in Shell starten <br/>
  `docker run --entrypoint /bin/sh -it`
- Container debuggen, der keine Shell etc hat:
  ```
  docker run --name xyz ...
  docker run --pid container:xyz --network container:xyz busybox sh
  ```
  - *start a debugger container that will share the pid and net namespaces of the target. The debugger container can (and probably should) bring its own tools, and using ps or ip in it will show the exact same process tree and the network stack as the target container sees itself ...  there are three namespaces that can be shared this way: pid, net, and ipc. The last one, though, can be shared only if the target itself was (re)started with --ipc 'shareable'*
  - *The docker run (or docker create) command doesn't allow sharing the mnt namespace. It means that the filesystem you see while in the debugger's shell is not the filesystem of the target container! With the pid namespace shared, you can still access the target's container filesystem using the following trick: `ls -l /proc/1/root/` or any other PID that belongs to the target container. But it might be quite confusing and limiting...*  (<https://iximiuz.com/en/posts/docker-debug-slim-containers/>)
- IP-Adresse des (Windows-)Host bekommen <br/>
  `getent hosts docker.for.win.localhost | cut -d ' ' -f1` <br/>
  oder <br/>
  `getent hosts host.docker.internal | cut -d ' ' -f1` <br/>
  siehe auch <https://stackoverflow.com/questions/48546124/what-is-linux-equivalent-of-host-docker-internal/48547074#48547074>
- Container (einschl. beendet) auflisten <br/>
  `docker ps -a`
- Images mit `<none>` löschen <br/>
  `docker rmi $(docker images --filter="dangling=true" -q)`
- alte Images löschen <br/>
  `docker rmi $(docker images | grep -E "months ago|years ago")`
- *processes in containers should not be run as root*
- File aus einem Image zum Host kopieren (?) <br/>
  `docker cp $(docker create <image>:latest):/path/in/image /path/in/host`
- *Anywhere that you find a command that takes container ID, you only need to specify as much of the ID as makes it unique (so "616abcde" could just "616" usually). You could specify the full container name if you'd like, e.g. wonderful_davinci. If you prefer using the name, then you should probably assign a name by yourself at run time (`docker run --name foo`)*
- *Changes to a service can be applied in-place, so for example, if you have 5 tasks running in a service and need two extra tasks, you can change your docker-compose.yml, then rerun `docker stack deploy` and you will only modify two tasks instead of recreating the original five.*
- *put the commands that will change least frequently at the top of your Dockerfile so that you can cache layers (and then reuse the cached layers) for as long as possible.*
