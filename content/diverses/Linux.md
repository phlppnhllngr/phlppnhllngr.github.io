---
title: Linux
parent: Diverses
---

# Linux
{: .no_toc }

## Inhalt
{: .no_toc }
- TOC
{:toc}


## User
- root hat immer User-ID 0, andere üblicherweise 1000+


## Berechtigungen
- neue Datei erzeugen mit `touch foo`, `ls -l foo` zeigt dann die "permission bits", z.B.: `-rwxr-xr-x`
  - file type: `-` (`-` = regular file)
  - owner permissions: `rwx`
  - group permissions: `r-x`
  - other permissions: `r-x`
- **chmod**
  - change mode
  - modify file access rights
  - r = read, w = write, x = execute
  - 4 = read, 2 = write, 1 = execute
  - `chmod 761 foo` -> owner of file foo: rwx (7=4+2+1), group that owns file foo: rw (6=4+2), other: x
  - *The file's owner or root can change permissions*
  - <https://wiki.ubuntuusers.de/chmod/>
  - <https://www.guru99.com/file-permissions.html#linux_file_permissions>
- **chown**
  - change file ownership
  - Every file is owned by a specific user (or UID) and a specific group (or GID)
  - `sudo chown $USER foo`
  - `chown user:group file`
  - *the owner can permit the other types of users to access that file and folder*
  - *only root can run chown to change a file's owner to another user*
  - <https://www.guru99.com/file-permissions.html#linux_file_ownership>
- **chgrp**
  - change file group ownership
  - *The owner of a file may change the group of the file to any group of which that owner is a member.*
- **sudo**
  - *gives non-root users temporary access to the elevated privileges* 
  - *does not switch the user account to become root*
- **su**
  - *temporarily become root*
  - `su` zu root werden, mit Umgebung des vorherigen Users
  - `su -` zu root werden, mit Umgebung von root


## Shell
- <https://github.com/alebcay/awesome-shell>
- [Bash Notes For Professionals](https://books.goalkicker.com/BashBook/)
- <https://google.github.io/styleguide/shellguide.html>
- <https://www.reddit.com/r/programming/comments/qjnzmn/underwhelmed_by_bash_functions_maybe_youre_using>
- <https://github.com/jlevy/the-art-of-command-line>
- <https://github.com/onceupon/Bash-Oneliner> - *A collection of handy Bash One-Liners and terminal tricks for data processing and Linux system maintenance.*
- [HN: Shell script best practices, from a decade of scripting things ](https://news.ycombinator.com/item?id=33354286)
- [HN: Linux command line for you and me](https://news.ycombinator.com/item?id=32886315)
- <https://github.com/trinib/Linux-Bash-Commands> - *Ultimate list of Linux bash commands, cheatsheet and resources*
- [Buch "The Linux Command Line"](https://www.linuxcommand.org/tlcl.php)
- <https://testing.googleblog.com/2023/10/shell-scripts-stay-small-simple.html>
<br/><br/>
- `sudo !!` um den letzen Befehl als Sudoer zu wiederholen
- `$?` = exit code des letzten Commands
- sh ist nur ein Symlink auf die Standardshell des Systems (meist bash)
- **bash flags**
  ```bash
  #!/bin/bash
  # -u (`-o nounset`) -- exit if a variable is not set
  # -e (`-o errexit`) -- exit for any command failure
  # -o pipefail -- Causes a pipeline to return the exit status of the last command in the pipe that returned a non-zero return value
  # -v (`-o verbose`) -- Print each command to stdout before executing it
  # -x -- Similar to -v, but expands commands
  set -euo pipefail
  IFS=$'\n\t'
  ```
  - <http://redsymbol.net/articles/unofficial-bash-strict-mode>
  - <https://cuddly-octo-palm-tree.com/posts/2021-01-17-bash-set-dash-e> (exit on error)
  - <https://tldp.org/LDP/abs/html/options.html>
  - <https://gist.github.com/mohanpedala/1e2ff5661761d3abd0385e8223e16425>
- **Strings prüfen**
  - Ob leer (zero-length, null): `if [ -z "$str" ];`
  - Ob nicht leer: `if [ -n "$str" ];`
- **Dateien prüfen**
  - Ob Datei existiert: `if [ -d $dir ];`
  - Ob Datei nicht existiert: `if [ ! -d $dir ];`
- **Signals**
  - *The signals are a method of communication between processes. When a process receives a signal, the process interrupts its execution and a signal handler is executed*
  - *After handling the signal, the process may or may not continue its normal execution*
  - Signals 
    - int
      - *is the signal sent when we press Ctrl+C*
      - *The default action is to terminate the process. However, some programs override this action and handle it differently.*
      - *We can think of `SIGINT` as an interruption request sent by the user.*
    - term & quit
      - *meant to terminate the process. In this case, we are specifically requesting to finish it. `SIGTERM` is the default signal when we use the `kill` command.* 
    - kill
      - *When a process receives `SIGKILL` it is terminated. This is a special signal as it can’t be ignored and we can’t change its behavior. We use this signal to forcefully terminate the process. We should be careful as the process won’t be able to execute any clean-up routine.*
    - abrt
    - ...
  - <https://www.baeldung.com/linux/sigint-and-other-termination-signals> 
  - trap
    - ```bash
      set -eu

      cleanup() {
        code=$?
        echo "inside cleanup, code was $code"
        trap - EXIT INT TERM QUIT # avoid reexecuting handlers
        exit "$code"
      }
      
      trap cleanup EXIT INT TERM QUIT
      
      echo '1'
      cat doesntexist.txt
      echo '2' # will not be printed
      ```

    - *bash: EXIT will also run on SIGINT (^C), which most other shells won't*
- **Farbige Outputs**
  - <https://stackoverflow.com/questions/5947742/how-to-change-the-output-color-of-echo-in-linux> 

### Tools
  - **shellspec**
    - <https://shellspec.info>
    - *BDD unit testing framework for shells*
  - **zx**
    - *A tool for writing better scripts*
    - *provides useful wrappers around child_process*
    - ```
      let branch = await $`git branch --show-current`
      await $`dep deploy --branch=${branch}`
      ```
    - <https://github.com/google/zx>
  - **wait-for-it**
    - <https://github.com/vishnubob/wait-for-it>
    - *test and wait on the availability of a TCP host and port*
  - **shellcheck**
    - <https://github.com/koalaman/shellcheck>
    - *static analysis tool for shell scripts. gives warnings and suggestions for bash/sh shell scripts*
    - Plugins für diverse IDEs, u.a. VSCode
  - **thefuck**
    - <https://github.com/nvbn/thefuck>
    - *corrects your previous console command*
  - **nushell**
    - https://github.com/nushell/nushell
    - Rust
  - **modern-unix**
    - *A collection of modern/faster/saner alternatives to common unix commands.*
    - <https://github.com/ibraheemdev/modern-unix> *5.3k
  - **direnv**
    - *when you cd to a directory, do things like set variables*
  - **asdf**
    - *manage and use specific versions of software. Can work with direnv too!*


## Commands & Packages
- **cron**
  - *daemon which runs at the times of system boot*
  - *crontab = cron table. file which contains the schedule of cron entries to be run and at specified times. File location varies by operating systems.*
  - *cron is the name of the tool, crontab is generally the file that lists the jobs that cron will be executing, and those jobs are cron jobs*
  - <https://tool.crontap.com/cronjob-debugger>
- **curl**
  - [HN - Mastering curl: interactive text guide](https://news.ycombinator.com/item?id=37390941)
- **envsubst**
    - *substitutes the values of environment variables*
- **exit**
  - *command often used to exit or logout of a session. For example, during an FTP session the bye command will exit FTP.*
  - *aliases for exit include "bye", "logout", and "lo".*
- **jq**
  - *command-line JSON processor*
  - <https://earthly.dev/blog/jq-select>
- **miller**
  - *like awk, sed, cut, join, and sort for name-indexed data such as CSV, TSV, and tabular JSON*
  - https://github.com/johnkerl/miller
- **nc**
  - Netcat
  - *networking utility for reading from and writing to network connections using TCP or UDP*
  - `nc -zv <host> <port>` z. B. `nc -zv foo.bar 1234`
  - `-z` *sets nc to simply scan for listening daemons, without actually sending any data to them*
  - `-v` verbose
- **rm**
  - *In Unix, programs generally do not interpret wildcards themselves. The shell interprets unquoted wildcards, and replaces each wildcard argument with a list of matching file names. if `$foo` might contain spaces, then `rm "$foo/*.txt"` might not do what you [want]* => `rm "$foo"/*.txt`
- **rsync**
  - *ist sowohl ein Netzwerkprotokoll als auch ein unter der GPL stehendes Programm zur Synchronisation von Daten* 
  - *Programm, um Dateien zwischen lokalen oder über das Netzwerk erreichbaren Pfaden abzugleichen [und zu kopieren]*
  - *Sind Quelle und Ziel lokale Pfade, werden die betroffenen Dateien normal kopiert. Wenn auf Quelle oder Ziel aber per SSH oder über einen speziellen rsync-daemon zugegriffen wird, nutzt rsync zusätzlich noch einen speziellen Delta-Transfer-Algorithmus, so dass nur die geänderten Teile der Dateien über das Netzwerk transportiert werden müssen.* 
  - <https://wiki.ubuntuusers.de/rsync/>
- **sed**
  - foo in text.txt durch bar ersetzen (`-i` = replace inline): `sed -i "s/foo/bar/" "./text.txt"`
- **traceroute**
  - *ermittelt, über welche Router und Internet-Knoten IP-Datenpakete bis zum abgefragten Rechner gelangen*
  - `traceroute wikipedia.de`
  - in Windows als tracert.exe verfügbar
- **try**
  - *lets you run a command and inspect its effects before changing your live system*
  - use cases
    - *quickly find out which files are touched / installed by apt installing a certain package*
    - *find out which log file, if any, a program writes to*
    - *run one of those curl / bash installation commands and inspect exactly what it'll do without reading through a huge script*
  - <https://github.com/binpash/try>
- **watch**
  - `watch -n 1 date +%s`
- **Xvfb**
  - In-memory Display
  - geeignet für headless Testen
    
### FTP
- <https://www.computerhope.com/unix/ftp.htm>
- <https://linuxize.com/post/how-to-use-linux-ftp-command-to-transfer-files/>
- **ftp**
- **ftps**
  - FTP over TLS 
- **sftp**
  - *Im Unterschied zum FTP über TLS (FTPS) begnügt sich SFTP mit einer einzigen Verbindung zwischen Client und Server.* 
- **lftp**
  - *Neben FTP unterstützt das Programm die Protokolle FXP, HTTP, FISH, SFTP, HTTPS, FTPS und BitTorrent.* 
- **scp**
  - secure copy protocol


## Package-Installation
- **nicht-interaktiv**
  ```sh
  DEBIAN_FRONTEND=noninteractive apt-get ...
  ```
  - *It never interacts with you at all, and makes the default answers be  used  for  all  questions.  It might  mail  error messages to root, but that's it; otherwise it is completely silent and unobtrusive,  a  perfect  frontend  for automatic installs.*
- **leichtgewichtiger**
  ```
  apt-get -y install --no-install-recommends <the-package>
  apt-get clean && rm -rf /var/lib/apt/lists/*
  ```
- **bestimmte Version**
  ```
  # alpine
  apk add packagename=1.2.3-suffix
  ```
  

## Distributionen
- Ubuntu
  - 22.04 LTS: jammy jellyfish
- Red Hat Enterprise Linux (RHEL)
  - Paketmanager: yum (RHEL 6, 7), dnf (RHEL 8: *yum is an alias to dnf*), rpm
    - *rpm is a package format, although the rpm command can be used to install rpm files. RHEL and Fedora discourage this practice if you can avoid it. The rpm command has a number of other useful functions, however, such as querying the contents of an rpm file.*
    - *DNF or "Dandified YUM" is the next-generation version of the "Yellowdog Updater, Modified" (yum)*
- Oracle Linux (OL, OLE)
  - *clone version of RHEL with some enhancements in Kernel to makes it more compatible with Oracle hardware and software*
  - *Oracle Linux with little effort (adjustments) can enhance the Oracle DB Performance. And most of the Oracle Products are tested under it.*
  - Paketmanager: yum
- Debian
  - Paketmanager: dpkg
  - 9: stretch
  - 10: buster
  - 11: bullseye
- Fedora
  - Paketmanager: dnf (Fedora 18+) 
- Linux Mint
  - *designed to work 'out of the box' and comes fully equipped with the apps most people need.*
  - <https://linuxmint.com/>
- Alpine
  - Paketmanager: apk
    - `apk add --no-cache` vs `apk add && rm /var/cache/apk/*`
      - *The `--no-cache` option allows to not cache the index locally, which is useful for keeping containers small.*
      - *But with multiple `apk add --no-cache` commands, the index files get downloaded every time. In this case it's less network chatter to do `apk update` at the top, then `rm -rf /var/cache/apk/*` near the bottom.*
      - *`rm -rf ...` DOES NOT reduce your image size when executed as a separate Dockerfile `RUN` statements. You MUST executed it in the same run statement*
      - <https://stackoverflow.com/questions/49118579/alpine-dockerfile-advantages-of-no-cache-vs-rm-var-cache-apk>   


## libc (C-Standard-Bibliothek)
- *There are two popular implementations for the libc interface* 
- glibc (GNU libc)
  - enthalten in: Ubuntu, Debian, CentOS, RHEL, SUSE, ...
  - *downside is that it is a fairly large and heavy codebase*
- musl
  - *newer implementation of the library. Used by Alpine Linux, it is much smaller in size compared to GNU libc and is meant to be lightweight, fast and simple. However, there are caveats. Musl libc actually has functional differences compared to GNU libc - things like regular expressions, EOF and multithreading could behave differently based on the implementation.*
  - für [statisches Linken](https://de.wikipedia.org/wiki/Linker_(Computerprogramm)#Statisches_Linken) optimiert


## Druck

### CUPS
- **Dockerfiles**
  - <https://github.com/olbat/dockerfiles/tree/master/cupsd> 
  - <https://github.com/quadportnick/docker-cups-airprint>
  - <https://github.com/anujdatar/cups-docker>
  - <https://gitlab.com/ydkn/docker-cups>
  - <https://github.com/thbe/docker-cups>
  - <https://github.com/jacobalberty/cups-docker>
