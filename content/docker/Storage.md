---
tags: [Notebooks/Docker]
title: Storage
created: '2020-08-09T10:30:01.094Z'
modified: '2020-08-09T10:48:18.388Z'
parent: Docker
---

# Storage
- [https://docs.docker.com/storage/]()

## bind mount
  - *a file or directory on the host machine is mounted into a container*
  - *The file or directory is referenced by its full or relative path on the host machine*
  - *Bind mounts exist on the host file system and being managed by the host maintainer. Applications / processes outside of Docker can also modify it*
  - *have limited functionality compared to volumes*
    - *You can’t use Docker CLI commands to directly manage bind mounts*
  - *Bind mounts are very performant*
  - *Bind mounts are much easier to backup. Docker sadly does not provide any command to backup volumes*
  - *in a docker-compose.yml:*

    ```yaml
    volumes:
     - type: bind
       source: ./my-file
       target: ./etc/my-file
    ```


## volume
  - [https://docs.docker.com/storage/volumes/]()
  - *Created and managed by Docker*
  - *With Volume, a new directory is created within Docker's storage directory on the host machine, and Docker manages that directory's content*
  - *they can not be accessed outside of Docker.*
  - *Docker manages [it] by placing it into the $DOCKER-DATA-DIR/volumes directory and attaching a reference to it (names or randomly generated ids)*
  - *many advantages over bind mounts*
    - *A given volume can be mounted into multiple containers simultaneously*
    - *you can manage volumes using Docker CLI commands or the Docker API.*
  - *in a docker-compose.yml:*

    ```yaml
    volumes:
    - type: volume
      source: dbdata #named volume; (For anonymous volumes, this field is omitted).
      target: /var/lib/dbdata
    ```


## mount & volume
*You can't reference either of them in a Dockerfile; the `VOLUME` directive creates a new nameless (with randomly generated id) volume every time you launch a new container and cannot reference an existing volume.*
