---
tags: [Notebooks/Diverses]
title: Linux
created: '2020-03-23T21:03:45.669Z'
modified: '2021-09-13T12:06:08.150Z'
parent: Diverses
---

# Linux

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
- **chown**
  - change file ownership
  - Every file is owned by a specific user (or UID) and a specific group (or GID)
  - `sudo chown $USER foo`
  - `chown user:group file`
- **chgrp**
  - change file group ownership
- **sudo**
  - temporarily become the superuser
- **su**
  - temporarily become another user
  - `su` zu root werden, mit Umgebung des vorherigen Users
  - `su -` zu root werden, mit Umgebung von root


## Shell
- <https://github.com/alebcay/awesome-shell>
- [Bash Notes For Professionals](https://books.goalkicker.com/BashBook/)
- <https://google.github.io/styleguide/shellguide.html>
- <https://www.reddit.com/r/programming/comments/qjnzmn/underwhelmed_by_bash_functions_maybe_youre_using>
- <https://github.com/jlevy/the-art-of-command-line>
<br/><br/>
- `sudo !!` um den letzen Befehl als Sudoer zu wiederholen
- `$?` = exit code des letzten Commands
- sh ist nur ein Symlink auf die Standardshell des Systems (meist bash)
- **nicht-interaktive Paketinstallation**
  ```sh
  DEBIAN_FRONTEND=noninteractive apt-get ...
  ```
  - *It never interacts with you at all, and makes the default answers be  used  for  all  questions.  It might  mail  error messages to root, but that's it; otherwise it is completely silent and unobtrusive,  a  perfect  frontend  for automatic installs.*
- **leichtgewichtigere Installationen**
  ```
  apt-get -y install --no-install-recommends <the-package>
  apt-get clean && rm -rf /var/lib/apt/lists/*
  ```
- **bash strict mode**
  ```bash
  #!/bin/bash
  set -euo pipefail
  IFS=$'\n\t'
  ```
  - <http://redsymbol.net/articles/unofficial-bash-strict-mode>
  - <https://cuddly-octo-palm-tree.com/posts/2021-01-17-bash-set-dash-e> (exit on error)
- **set -x**
  *which is like DOS’ ECHO ON: it prints every command before it runs. Free progress log*

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
    - https://github.com/nvbn/thefuck
    - *corrects your previous console command*
  - **nushell**
    - https://github.com/nushell/nushell
    - Rust
  - **modern-unix**
    - *A collection of modern/faster/saner alternatives to common unix commands.*
    - <https://github.com/ibraheemdev/modern-unix> *5.3k


## Commands & Packages
- **rm**
  - *In Unix, programs generally do not interpret wildcards themselves. The shell interprets unquoted wildcards, and replaces each wildcard argument with a list of matching file names. if `$foo` might contain spaces, then `rm "$foo/*.txt"` might not do what you [want]* => `rm "$foo"/*.txt`
- **Xvfb**
  - In-memory Display
  - geeignet für headless Testen
- **cron**
  - *daemon which runs at the times of system boot*
  - *crontab = cron table. file which contains the schedule of cron entries to be run and at specified times. File location varies by operating systems.*
  - *cron is the name of the tool, crontab is generally the file that lists the jobs that cron will be executing, and those jobs are cron jobs*
- **miller**
  - *like awk, sed, cut, join, and sort for name-indexed data such as CSV, TSV, and tabular JSON*
  - https://github.com/johnkerl/miller
- **jq**
  - *command-line JSON processor*
  - <https://earthly.dev/blog/jq-select>


## Distributionen
- Oracle Linux
  - Paketmanager: yum
- Debian
  - Paketmanager: dpkg
- Linux Mint
  - *designed to work 'out of the box' and comes fully equipped with the apps most people need.*
  - <https://linuxmint.com/>
