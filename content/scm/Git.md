---
title: Git
parent: SCM
---

# Inhalt
{: .no_toc }
- TOC
{:toc}

# Git
- <https://www.reddit.com/r/programming/comments/df2uj3/99_of_the_git_commands_youll_need_at_work>
- <https://www.reddit.com/r/programming/comments/wcpz9j/git_cheat_sheet_summary_of_commands_i_used_in_my/>
- <https://github.com/git-tips/tips>
- <https://snyk.io/blog/10-git-aliases-for-faster-and-productive-git-workflow>
- [Fireship - 13 Advanced (but useful) Git Techniques and Shortcuts](https://www.youtube.com/watch?v=ecK3EnyGD8o)
  - bisect, push, log, rebase, revert
  - `git log --graph --decorate --abbrev-commit --pretty=medium --branches --remotes`
- <https://girliemac.com/blog/2017/12/26/git-purr/>
- <https://ohshitgit.com/>
- <https://gitimmersion.com/>
- [HN - Git from the Inside Out, 06/2022](https://news.ycombinator.com/item?id=31964814)
- <https://www.gitkraken.com/learn/git/best-practices>
- <https://www.atlassian.com/de/git>
- <https://softwaredoug.com/blog/2022/11/09/idiot-proof-git-aliases.html>
- <https://www.reddit.com/r/programming/comments/1atowsj/popular_git_config_options/>
  - ```
    push.autoSetupRemote true // to skip the annoying "branch has no remote tracking branch message"
    help.autocorrect
    core.excludesfile // a global .gitignore
    ``` 


## Stages
- **working directory**
  - *the local repository*
  - *changes are not tracked*
  - *track changes by adding them to index* ('staging', `git add`)
  - git add
    - `-p`
      - <https://johnkary.net/blog/git-add-p-the-most-powerful-git-feature-youre-not-using-yet/>
        - *allows you to stage parts of a changed file, instead of the entire file*   
- **index**
  - *confirm changes and add them to head with* `git commit`
- **head**
  - *the most recent committed version of code*
  - `git push` *changes to remote repository*


## Commit
- `git add . && git commit -m "..."` -> `git commit -am "..."`
- fixup
- ammend
  - *convenient way to modify the most recent commit. It lets you combine staged changes with the previous commit instead of creating an entirely new commit* 
  - `git commit --ammend --no-edit`
  - *The --no-edit flag will allow you to make the amendment to your commit without changing its commit message* 

## Push
- force
- force-with-lease
  - *safer option that will not overwrite any work on the remote branch if more commits were added to the remote branch (by another team-member or coworker or what have you). It ensures you do not overwrite someone elses work by force pushing.*
 
## pull
- --rebase
- --ff-only

## Branching
- <https://learngitbranching.js.org/>
- Haupt-Branch heißt 'master' oder 'main' (Konvention)
- `git status` *shows the current branch*
- **create new branch**
  - `git branch <name>` *(only creates, doesn't switch)*
  - *switch to existing branch with* `git checkout <name>`
  - *create new branch and switch to it:* `git checkout -b <name>`
  - *push a new local branch:* `git push -u origin <name>`
- **remote branches**
  - `git branch [-r]` um Remote-Branches anzuzeigen
  - (erstmalig) auschecken: `git checkout --track origin/<name>`
- **delete branch**
  - locally: `git branch -d <localBranchName>`
  - remote: `git push origin --delete <remoteBranchName>`


## Änderungen zusammenführen

### merge
- *merge a branch 'x' into the current checked out branch with* `git merge x`
- *git will ask how to resolve conflicts, if any*
- <u>Merge-Strategien</u>
  - <http://blog.danieljanus.pl/2021/07/01/commit-groups>
  - **A) merge-commit**
    - *all commits from branch will be added to the base branch via a new merge commit*
    - *we don’t rewrite history: once a commit is made, it stays*
    - *you can’t git revert a merge commit—that is, unless you tell Git which of the parent commits you want to keep and which to discard*
    - einen Branch nach master mergen
      ```
      git checkout master
      git pull
      git merge <branch>
      git push
      ```
  - **B) rebase and merge**
    - *all commits from branch will be rebased and added to the base branch*
    - *we don’t squash the branch commits together. Instead, we directly replay them on top of main/master.*
  - **C) squash and merge**
    - `git merge --squash` 
    - *all commits from branch will be combined into one commit in the base branch*
    - *we mash together the changes introduced by the branch commits into a single commit, and then replay that commit on top of main/master*
    - *you can rewrite a branch 10x over, add and remove log and debug at will, and in the end, commit a clear and concise just of changes back to the main branch.*

### cherry pick
- Übernahme eines spezifischen Commits von Branch A nach Branch B
- in Branch A committen und die Hash-Summe des Commits notieren
- zu Branch B wechseln
- `git cherry-pick <hash>` (ist dann mit dem gleichen Kommentar direkt committed)
  - `git cherry-pick <hash> -n` um nicht direkt zu committen
- `git push`

### rebase
- neben merge die andere Möglichkeit, um Änderungen aus einem Branch in einen anderen zu übernehmen
- <https://git-scm.com/book/de/v2/Git-Branching-Rebasing>
- <https://stackoverflow.com/questions/804115/when-do-you-use-git-rebase-instead-of-git-merge>
- Stand von master in den Branch ziehen
  ```
  git checkout <branch>
  git rebase master
  ```
- autostash

### Stand von remote holen
- **fetch**
  - *tells your local git to retrieve the latest meta-data info from the original (yet doesn't do any file transfering. It's more like just checking to see if there are any changes available*
- **pull**
  - *does that AND brings (copy) those changes from the remote repository*
  - macht zuerst `fetch`, dann `merge`
  - *default from "origin"*
  - bzgl. automatischer `Merge branch '<name>' of <url>`-Commits
    - *caused when your local repo is both ahead and behind your remote repo, and you perform a "git pull"*
    - *to avoid these merge commits, you need to explicitly resolve the conflict in a different way."*
    - *One easy way to do this is to always do "git pull --rebase" instead of "git pull", which will rebase your local commits on top of your remote commits, instead of creating a merge commit.*
    - Alternative: pull mit "fast forward"


## Code zurücksetzen
- <https://stackoverflow.com/a/42903805/7437541>
- **reset**
  - local auf remote zurücksetzen
    ```
    git fetch --all
    git reset --hard origin/<branch> (git reset --hard origin/master)
    ```

## Stash
- lokale Änderungen sichern
- zuerst `git stash`<br/>
  `-u` um auch nicht bereits getrackte (neue) Dateien zu stashen
- dann später zurückholen (zum Committen): `git stash pop`
- Stash leeren: `git stash clear`
- <https://www.atlassian.com/git/tutorials/saving-changes/git-stash>


## Aliases
- `git config --global alias.foo "pull --rebase"` -> `git foo`


## Worktree
- <https://git-scm.com/docs/git-worktree>
- mehrere Branches <u>gleichzeitig</u> auf der Festplatte haben, in versch. Verzeichnissen
- *Checkout [other] branches in separate folders using worktree. For each branch, you got an independent IDE project.*
- *(branch) switching is expensive, because in the meantime you completely restructured the repository and maybe build system. If you switch, your IDE will run mad trying to adapt the project settings*
- nützlich z.B. damit man nicht bei jedem Branch-switch node_modules (ggf. in anderer Version) neu installieren muss
- Vorgehen<br/>
  im root des master branch: `git worktree add ../<foldername> <branchname>`<br/>
  erzeugt das Verzeichnis und checkt den Branch darin aus
- Nachteil: HDD-Verbrauch

## switch
- *use to switch branches*
- *performs extra sanity checks that checkout doesn't, for example switch would abort operation if it would lead to loss of local changes*

## restore
- *use to restore a file to last committed version*
- *replaces and simplifies some of the use cases of git reset and git checkout*

## sparse-checkout
- *allows users to restrict their working directory to only the files they care about*
- *useful in CI/CD for improving performance of a pipeline, when you only want to build/deploy part of the monorepo and there's no need to check out everything.*
- <https://github.blog/open-source/git/bring-your-monorepo-down-to-size-with-sparse-checkout/>
- ```
  git clone --no-checkout https://github.com/derrickstolee/sparse-checkout-example
  cd sparse-checkout-example
  git sparse-checkout init --cone
  git checkout main
  git sparse-checkout set service/common
  ```

## bisect

## reflog
- <https://old.reddit.com/r/programming/comments/1djkc4l/literally_never_lose_your_commits_again_git/>

## Workflow
- <https://github.com/pcottle/learnGitBranching>
- **centralized**
  - <https://www.atlassian.com/git/tutorials/comparing-workflows#centralized-workflow>
- **feature branch**
  - <https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow>
- **gitflow**
  - <https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow>
  - <https://www.reddit.com/r/programming/comments/fdv7v0/please_stop_recommending_git_flow>
- **forking**


## Tools
- → SCM/Commits
- **git-cliff**
  - *customizable Changelog Generator that follows Conventional Commit specifications*
  - <https://github.com/orhun/git-cliff> *2.6k
  - <https://news.ycombinator.com/item?id=40798469>

### GUI Clients
- **GitKraken** [1]
  - Paid (recurring licence) 
  - <https://www.gitkraken.com>
- **Fork** [1]
  - Paid (one-time purchase) 
  - <https://fork.dev/>
- **SourceTree** [1]
  - Free
  - <https://www.sourcetreeapp.com/>
- **SmartGit** [1]
  - Paid (recurring licence) 
  - <https://www.syntevo.com/smartgit/>
- [1: Vergleich](https://old.reddit.com/r/programming/comments/yqm0ka/idiot_proof_git/ivracgf/.compact)
- **TortoiseGit**
- **lazygit**
  - *simple terminal UI for git commands* 
  - <https://github.com/jesseduffield/lazygit> <img loading="lazy" src="https://img.shields.io/github/stars/jesseduffield/lazygit?style=flat-square"/>

### CLIs
- **Git bash for windows**
  - Aliase: <https://dev.to/mhjaafar/git-bash-on-windows-adding-a-permanent-alias-198g>
    C:\Program Files\Git\etc\profile.d
    - alias gpl='git pull --rebase'
    - alias gcp='git cherry-pick'
    - alias gcm='git checkout master'
    - alias gpsh='git push'
- **Bit**
  - *autocompletion, new commands*
  - <https://github.com/chriswalz/bit>


## gitignore
- <https://gitignore.io>
  - man gibt seine Programmiersprache, IDE, usw. an und erhält ein darauf abgestimmtes gitignore-File
- <https://github.com/github/gitignore>
  - *A collection of useful .gitignore templates*
