---
tags: [Notebooks/Docker]
title: Dockerfile
created: '2020-08-15T19:29:53.326Z'
modified: '2021-07-28T12:50:17.444Z'
parent: Docker
grand_parent: DevOps
---

# Dockerfile
- <https://www.reddit.com/r/programming/comments/jb2jwq/dockerfile_security_best_practices>
- <https://docs.docker.com/develop/develop-images/dockerfile_best-practices>
- <https://blog.docker.com/2019/07/intro-guide-to-dockerfile-best-practices>

<br/>

- Nur bei `COPY` und `ADD` wird der Cache invalidiert (wenn Files geändert). Bei z.B. einer `RUN`-Anweisung wird immer der Cache verwendet (build mit `--no-cache=true` um das zu verhindern).
- *Always combine "apt-get update" with installations, e.g. `RUN apt-get update && apt-get install -y package-bar`*
- Aufräumen nach apt-get: `... && rm -rf /var/lib/apt/lists/*`
- Best Practices für Installation von Linux-Paketen in Docker-Images: <https://pythonspeed.com/articles/system-packages-docker/>
- **COPY**
  - *it's suggested that you explicitly copy files that you expect to change frequently. For example, if you're going to copy all of "./" to the container, but "./requirements.txt" is going to change a lot, then you should do `COPY ./requirements.txt /`, then maybe use that file with a RUN command, then make another COPY line like `COPY ./ /`.*
  - Inhalt von Verzeichnis "foo" in Verzeichnis "/bar" kopieren: `COPY foo/ /bar/` 
  - <https://www.reddit.com/r/programming/comments/toptrr/copy_chmod_reduced_the_size_of_my_container_image/.compact>
- **USER**
  - *when you don't need specific privileges, make a new user with this command.*
- <u>CMD vs ENTRYPOINT vs RUN vs EXEC vs CMD</u>
  - **CMD**
    - *default command that executes when the container is starting*
    - *ignored if passing any arguments when starting the container*
    - `CMD ["/myscript.sh", "hello world"]`
    - auch hier gibt es "shell"- und "exec"-Form (siehe entrypoint)
    - *the exec form is required for CMD if you are using it as parameters/arguments to ENTRYPOINT that are intended to be overwritten.*
  - **ENTRYPOINT**
    - <https://docs.docker.com/engine/reference/builder/#entrypoint>
    - *the default command to run when the container starts. Moreover, we're now able to provide extra arguments.*
    - `ENTRYPOINT ["/myscript.sh"]`
    - der entrypoint kann ins "shell"- oder in "exec"-Form angegeben werden
      - shell-Form
        - `ENTRYPOINT command param1 param2`
        - auf Windows ist die default-shell `cmd /S /C` (siehe SHELL)
        - `RUN powershell -command Write-Host hello` wird also zu `cmd /S /C powershell -command Write-Host hello`
        - *In the shell form you can use a \ (backslash) to continue a single RUN instruction onto the next line.*
        - *using the shell form for ENTRYPOINT likely means you're not propagating signals correctly to your app, which can cause problems, in particular in Kubernetes clusters.*
      - exec-Form
        - `ENTRYPOINT ["executable", "param1", "param2"]`
        - *Unlike the shell form, the exec form does not invoke a command shell. This means that normal shell processing does not happen. For example, CMD [ "echo", "$HOME" ] will not do variable substitution on $HOME. If you want shell processing then either use the shell form or execute a shell directly, for example: CMD [ "sh", "-c", "echo $HOME" ].*
        - *The exec form makes it possible to avoid shell string munging, and to RUN commands using a base image that does not contain the specified shell executable.*
  - *can use cmd and entrypoint in combination. One such use-case is to define default arguments for entrypoint*

    ```
    ENTRYPOINT ["/myscript.sh"]
    CMD ["hello world"]
    ``` 

  - **RUN**
  - **SHELL**
    - *allows the default shell used for the shell form of commands to be overridden.*
    - *The default shell on Linux is ["/bin/sh", "-c"], and on Windows is ["cmd", "/S", "/C"]*
    - <https://docs.docker.com/engine/reference/builder/#shell>
    - Bsp.:

      ```
      SHELL ["powershell", "-command"]
      RUN Write-Host hello
      ```
