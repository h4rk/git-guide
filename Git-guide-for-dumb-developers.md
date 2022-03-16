# Git guide for dumb developers (like me)

- [Git guide for dumb developers (like me)](#git-guide-for-dumb-developers-like-me)
  - [1. Introduction to git](#1-introduction-to-git)
    - [1.1 Quick introduction to git](#11-quick-introduction-to-git)
      - [1.1.1 Repositories, branches, conflicts](#111-repositories-branches-conflicts)
      - [1.1.2 Local structure](#112-local-structure)
    - [1.2 .gitignore](#12-gitignore)
    - [1.3 Git config](#13-git-config)
  - [2. Commands on local repos](#2-commands-on-local-repos)
    - [2.1 Git add](#21-git-add)
    - [2.2 Git commit](#22-git-commit)
    - [2.3 Git restore](#23-git-restore)
    - [2.4 Git reset](#24-git-reset)
    - [2.5 Git status](#25-git-status)
    - [2.6 Git switch](#26-git-switch)
    - [2.7 Git merge](#27-git-merge)
  - [3. Commands on remote repos](#3-commands-on-remote-repos)
    - [3.1 Git clone](#31-git-clone)
    - [3.2 Git fetch](#32-git-fetch)
    - [3.3 Git pull](#33-git-pull)
    - [3.4 Git push](#34-git-push)

<br>

<div style="page-break-after:always" />

---

<br>

## 1. Introduction to git
### 1.1 Quick introduction to git
Git is a distributed **version control system**.
<br>
It consist of a remote repository which is both storage place for all kind of files and an archive holding all prevoius changes logged and accessible.

#### 1.1.1 Repositories, branches, conflicts
Repositories have branches, which are parallel istances of the repository that allows different developers to work on different features at the same time without having to constantly share with each other the changes they make, git will handle merging changing mostly on his own, unless there are **conflicts**.<br>
**Conflicts** are situations where you are trying to implement a change you made, but in the meantime the thing you changed was also modified by someone else, so git cannot autonomosly decide which version to keep, and you need to explicitly tell him.

Repositories are usually structured with a main (also called *master* in older repos) branch and a subset of branches, created as copies of the main branch, used to introduce changes without risking of losing what's alredy there and working.
<br>
After you changes are tested and proven to be working, you can first merge the main branch into your secondary branch once again, to implement parallel changes prople may have made, and to assure there are no conflicting changes and after that you can merge your branch into the main branch, effectively applying your changes to the real code.

#### 1.1.2 Local structure
In order to work on your changes you will need to copy (or *clone*, more on commands on later chapters) the remote repository on your local machine.
Doing so will create an exact copy of everything (you can also choose to copy only a subset of the remote repo e.g: only one of a few branches) present on the remote repo on your machine.
<br>
Here things are a bit different, in fact the repository in structured in 3 levels:
1. Working directory
2. Staging area
3. Local repository

Working directory is the place where you are actually working and modifing files; staging area is a middle ground, where you can save changes in order to commit them on the repository; lastly, the local repository is the actual repository there you will need to write your definitive changes.
![no-img-found](img/local-repo-staging-wd.png)

### 1.2 .gitignore
When working with code, programs and complex frameworks it's often the case where you will have a lot of files you actually don't want to save on your repository because they are heavy and useless (local library files which are remotly shared in advanced environments, config files which are personal to your code editor, etc...)
Git offers you the chance to declare all of this in a file, placed anywhere in the repository and automatically ingore these files/folders when making commits.
<br>
You can use the exact name of every file you want to ignore, but that is going to get weird if you need to ignore a lot of stuff, so git allows you the opportunity to use regex-like syntax, like in this example:

```
#Exclude specific file
test.txt


#Exclude specific extension
*.log
*.jar


#Exclude specific file
tmp/
lib/


#Weird combinations:
#
#exclude every jar file inside any folder that ends with the suffix 'Library'
*Library/*.jar

#exclude any occurrence of /logs/debug.log from anywhere in the repo
**/logs/debug.log
```


### 1.3 Git config
Every change you make on the repository needs to be signed, therefore you will need to declare a username and an email for that purpose.<br>
You can do that with the following commands:

```
git config [--global] user.name <choosen username>
```

```
git config [--global] user.email <choosen email>
```

The 'global' flag is better avoided in work environment, because every commit you will make from that machine will use those information, and chances are that you will eventually forget it and commit on a new client repository with wrong username or even worse, with your personal github account which will be a bit embarassing (trust me on this one).
<br>
It's a bit tedious to configure both values each time you clone a new repository, but it's good discipline and plus you will memorize it for good.

## 2. Commands on local repos
### 2.1 Git add
This command moves files from the working directory to the staging area. Syntax is as follow:
```
git add <filename or glob expression>
```
There is much more details to this command but for the basics this is gonna do it.
You can add file 1 by 1 and perform different, very small and specific commits or add everything in one go and perform a single commit with the following syntax:
```
git add .
```

### 2.2 Git commit
Commit allow you to apply every change present in your staging area to your local repository.
The syntax is as follow:
```
git commit [-m <commit message>]
```
Just like the add command (and every other command explanation in this guide) this is an extremely practical and simplyfied explanation of the basics, you can find in detail documentation in the git official website.

Executing a git commit without specifing the message will prompt open a text editor fot you to write the message, since it's mandatory (and you should care to write something short but meaningful, you will thank yourself a lot), but chances are you didn't care or pay enougth attention to select a text editor you are actually able to use when installing git, so my advice is to just use the '-m \<message>' flag from the command line.


### 2.3 Git restore
Restore allows you to restore working tree files. You did some stupid change and need to restore it to how it was before? This is the command for you.
Here is the syntax:
```
git restore <filepath or glob expr>
```

Again, if you want to restore everything in the working directory you can just go:
```
git restore .
```
This command can also be used to restore the stuff in the staging area (sourcing from HEAD, which is git lingo to indicate the last commit on your local repository) with the optional flag '--staged', but this can also be done with another command we are about to see, and since git restore it's actually experimental at the moment of writing, we'll use the other method for now.

### 2.4 Git reset
### 2.5 Git status
### 2.6 Git switch
### 2.7 Git merge

## 3. Commands on remote repos
### 3.1 Git clone
### 3.2 Git fetch
### 3.3 Git pull
### 3.4 Git push