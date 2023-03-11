---
title: Storage
parent: Docker
grand_parent: DevOps
---

# Storage
- writable layer
  - *The writable layer of the container is where all the data will be written in the container if no volume is mounted. It will persist on container restart, but will be deleted if the container is deleted.*
  - *Writing into a container’s writable layer requires a storage driver to manage the filesystem. The storage driver provides a union filesystem, using the Linux kernel. This extra abstraction reduces performance as compared to using data volumes, which write directly to the host filesystem.*
- <https://docs.docker.com/storage>


## Bind mount
  - aka "host volume"
  - *a file or directory on the host machine is mounted into a container*
  - *The file or directory is referenced by its full or relative path on the host machine*
  - *Bind mounts exist on the host file system and being managed by the host maintainer. Applications / processes outside of Docker can also modify it*
  - *have limited functionality compared to volumes*
    - *You can’t use Docker CLI commands to directly manage bind mounts*
  - *Bind mounts are very performant*
  - *Bind mounts are much easier to backup. Docker sadly does not provide any command to backup volumes*
  - *If you use the -v switch from the docker run command and try to mount a non-existent directory from the host — a new directory will be created on the host with root as the owner and 755 permissions making it not writable for any other user than root inside of the container.*
  - CLI: `docker run -v /host/path/:/container/path`
  - *in a docker-compose.yml:*

    ```yaml
    volumes:
     - type: bind
       source: ./my-file
       target: ./etc/my-file
    ```

## Volume
  - aka "managed volume"
  - *Created and managed by Docker*
  - *With Volume, a new directory is created within Docker's storage directory on the host machine, and Docker manages that directory's content*
  - *they can not be accessed outside of Docker.*
  - *Docker manages [it] by placing it into the $DOCKER-DATA-DIR/volumes directory and attaching a reference to it (names or randomly generated ids)*
  - *many advantages over bind mounts*
    - *A given volume can be mounted into multiple containers simultaneously*
    - *you can manage volumes using Docker CLI commands or the Docker API.*
  - named
    - ```
      docker volume create <name>
      docker run -v <name>:/container/path
      ```
    - docker-compose.yml
      ```yaml
      volumes:
      - type: volume
        source: dbdata #named volume; (For anonymous/unnamed volumes, this field is omitted)
        target: /var/lib/dbdata
      ```
  - unnamed
    - im Host (automatisch erzeugt) unter `/var/lib/docker/volumes/<random-hash>/_data`
    - ```
      docker run -v /container/path/
      ```
  - <https://docs.docker.com/storage/volumes>


## Mount & volume
- *You can't reference either of them in a Dockerfile; the `VOLUME` directive creates a new nameless (with randomly generated id) volume every time you launch a new container and cannot reference an existing volume.*


## tmpfs mounts
- *If you’re running Docker on Linux, you have a third option: tmpfs mounts*
- *will persist data as long as the container is running (i.e. the data in the volume will be deleted when the container stops)*
- *the tmpfs volume size is unlimited by default with the risk of the container using up all the machine memory. Using tmpfs-size flag is recommended to mitigate that risk*
- *When you create a container with a tmpfs mount, the container can create files outside the container’s writable layer. As opposed to volumes and bind mounts, a tmpfs mount is temporary, and only persisted in the host memory. When the container stops, the tmpfs mount is removed, and files written there won’t be persisted.*
- *Unlike volumes and bind mounts, you can’t share tmpfs mounts between containers*
- <https://docs.docker.com/storage/tmpfs/>


## Temporäre Dateien in Containern
- **Linux**
  - *By default, all the files and data that gets stored in /var/tmp live for up to 30 days. Whereas in /tmp, the data gets automatically deleted after ten days. Furthermore, any temporary files that are stored in the /tmp directory get removed immediately on system reboot.*
- **cron**
  - Standardmäßig sind in Container keine cron-Jobs aktiv, daher wird /tmp ohne zusätzliche Konfig nie geleert.
- **tmpfs**
  - *if you need to be able to clean up temporary data while the container is running, this is not a good solution as you will need to stop the container to have your temporary data cleaned.*
- **Mounting host machine /tmp in the container with a bind mount**
  - *result will depend on how the host machine manage /tmp (in most cases, data are cleared upon machine restart)*
- **Volume, mit dedizierten "Cleanup"-Container geteilt**
