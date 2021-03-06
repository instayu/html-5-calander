This tutorial walks you through how to set up Git on various platforms so you can be reading and writing YUI code in no time. Once your environment is set up, be sure to read [Tutorial: Contribute Code to YUI](http://yuilibrary.com/yui/docs/tutorials/contribute/) to learn how to clone YUI source code to your local development environment, and [submit a CLA](http://yuilibrary.com/contribute/cla/) to contribute to YUI.

## Install Git on Mac

### Lion

* [Download and Install Xcode from the Mac App Store](http://itunes.apple.com/us/app/xcode/id448457090?mt=12) (it's free)
* After installation open a terminal and type: `git --version`
* You should see something like this _Version may vary_: `git version 1.7.4.4`
* Git is now installed and working

### [Snow] Leopard

* [Download and Install Git Client for OS X](http://code.google.com/p/git-osx-installer/downloads/list)
* After installation open a terminal and type: `git --version`
* You should see something like this _Version may vary_: `git version 1.7.6.1`
* Git is now installed and working

### Tiger

* [Download and Install Git package for OS X](http://metastatic.org/text/Concern/2007/09/15/new-git-package-for-os-x/)
* You will need to add `/usr/local/bin` to your `$PATH`
    * `vim ~/.bashrc`
    * At the bottom of the file add this line:
    * export `PATH=$PATH:/usr/local/bin`
* After installation open a terminal and type: `git --version`
* You should see something like this: `git version 1.7.6.1`
* Git is now installed and working

### Mac Ports

If you have Mac Ports installed, do the following:

* Install the `git-core` package
* `sudo port install git-core`
* After installation open a terminal and type: `git --version`
* You should see something like this: `git version 1.6.0`
* Git is now installed and working

### Fink

_Git is in the unstable tree in Fink, and I couldn't get it to install. You should pick another method_

## Install Git on Linux

### Redhat

For Fedora 7 and later.

* Install the `git-core` package
* `sudo yum install git-core`
* After installation open a terminal and type: `git --version`
* You should see something like this: `git version 1.7.6.1`
* Git is now installed and working

For Fedora 6 and older, git-core is part of Fedora Extras (http://fedoraproject.org/wiki/Extras).

For users of Red Hat Enterprise Linux and its clones (such as CentOS and Scientific Linux), users will have to build git by hand. Source available here: http://git.or.cz/

### Ubuntu

* Install the `git-core` package
* `sudo apt-get install git-core`
* After installation open a terminal and type: `git --version`
* You should see something like this: `git version 1.7.0.4`
* Git is now installed and working

## Install Git on Windows

* [Download and Install Git Client for Windows](http://code.google.com/p/msysgit/downloads/list)
* During installation, you'll be asked which SSH Executable you'd like to use. Unless you already use plink/putty/pageant and are familiar with managing keys on it, choose "Use OpenSSH". It simplifies ssh key generation and use.
* After installation open Git Bash and type: `git --version`
* You should see something like this: `git version 1.7.6.1`
* Git is now installed and working
* **Important Config Option** You need to add this config option to help Windows deal with line endings: `git config --global core.autocrlf true`

## Configure Git

Setting `user.name` and `user.email` are the minimum configuration options that need to be set so your name and email will show up in your commit messages.

```
git config --global user.name "Dav Glass"
git config --global user.email dav.glass@yahoo.com
```
Use _your_ name and email of course; there are [many other configuration options](http://www.kernel.org/pub/software/scm/git/docs/git-config.html) you can set. These configs should be written to this file (same for Windows, when working in Git Bash): `~/.gitconfig`. My current `~/.gitconfig` looks like this:

```
[merge]
   tool = opendiff
[core]
   excludesfile = /Users/davglass/.gitignore

[alias]
   st = status
   ci = commit
   co = checkout
   br = branch
[color]
   ui = auto
   status = auto
   branch = auto
    diff = never

[user]
   name = Dav Glass
   email = dav.glass@yahoo.com
```

And my `~/.gitignore` file

```
.DS_Store
._*
.svn
.hg
.*.swp
```

## Set Up SSH

GitHub has several helpful tutorials on setting up SSH for use with git. Click the links below for more information:

* [Generating SSH keys (OS X)](http://help.github.com/mac-key-setup/)
* [Generating SSH keys (Win/msysgit)](http://help.github.com/msysgit-key-setup/)
* [Troubleshooting SSH issues](http://help.github.com/troubleshooting-ssh/)

## Commit Code: Git Tips

Git is a little different than CVS, every person has a copy of the repository on their local machine. So you can commit to it as much as you like. No build will be triggered.

Most of the built in aliases for git will help because they are similar to CVS.

* `git pull` This will pull a fresh copy of the repository.
* `git commit` This will commit changes to your local repository (not the server).
* `git add` This is a little different, you use git add to add a file to the commit index. It's not just for new files.
* `git push` This is what moves your local repository to the server you checked out from.
* `git status` Shows you the status of your repository.
* `git diff` Gives you a diff of the file.
* `git rm` This lets you remove files and directories.

### git add

This example shows using git add to add each file to the commit index before committing.

```
$ cd /my/working/directory
$ vim README

# Edit the file

$ git add README
$ git commit -m "Updated the README file"

# Then you will see something like this:

Created commit 794a86f: Updated the README file
 1 files changed, 1 insertions(+), 0 deletions(-)
```

### git commit all

This example shows using `git -a` to commit all changed files

```
$ cd util/dd/src/js
$ vim drag.js

# Edit the file

$ git commit -a

# At this point git will open your default editor and ask for a commit message
# Then you will see something like this:

Created commit ed16907: fixed #2345: patched file to fix something
 1 files changed, 2 insertions(+), 0 deletions(-)
```

### Resolve a Failed Push

If you encounter a (non-fast forward) error on push:

```
To git@github.com:username/yui3.git
! [rejected]    master -> master (non-fast foward)
error: failed to push some refs to 'git@github.com:username/yui3.git'
```

Generally that means that your tree is now out of sync with the main repository. You need to cd projectroot and do a git pull. This should bring your tree into sync with the repository and then it will allow you to git push.

### Revert Changes In Your Working Tree

To revert modified files in your working tree (the equivalent of `cvs co -C` ):

```
$ git checkout -- path/to/file
```

A `git status` will give you a list of files in your working tree which are modified.

### Create Remote Branches

NOTE: This method does not require you to switch to the local branch in order to push it to the remove server.

Create the local branch (from the branch you're currently in (generally "master")):

```
$ git branch [branch name]
```
Push it to the origin server:

```
$ git push origin [branch name]
```
Users will then be able to checkout the remote branch by using:

```
$ git checkout -b [local branch name] origin/[branch name]
```
Which will create a new local branch, which tracks against the remote branch, and also change the working tree to the local branch (so any changes you make, you're making to the branch).

Users can then switch between branches as required using:

```
$ git checkout [branch name]
```

# Switching back to "master", which is a tracking branch itself, works the same way...
```
git checkout "master"
```

### Reset to a Tag

Based on the [yui3 project](http://github.com/yui/yui3) and pulling the tag [v3.4.0](http://github.com/yui/yui3/tree/v3.4.0)

From your cloned repo:

```
# Get up to date
$ git pull origin master

# Reset head to the tag
$ git checkout v3.4.0

# Should print something like this:
Note: checking out 'v3.4.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b new_branch_name

HEAD is now at d617041... Bump package.json version to 3.4.0.

# Now create a local branch for easy task switching:
$ git checkout -b branch-3.4.0

# You can check this by calling:
$ git log -n1

# That commit should be the one listed above:
commit d6170413cd7404cb54e207cd9341dbc0ff16e358
Date:   Thu Jul 28 11:25:42 2011 -0700

Bump package.json version to 3.4.0.

# Now you can switch between master and this tag like this:
$ git checkout master # Back to the master branch

$ git checkout branch-3.4.0 # Back to this tag
```

### Use `rebase` and `merge` to Keep Your Development Branch in Sync

Use rebase to apply commits downstream onto your development branch. Use merge to apply commits from your dev branch back upstream: http://sites.google.com/a/insoshi.com/insoshi-guides/Git-Guides/merge-vs-rebase

```
$ git checkout mybranch // checkout my dev branch
$ vi workingfiles.js // make some changes
$ git commit -a -m "edits" // commit my changes
$ git checkout master // checkout my upstream branch
$ git pull // pull from origin
$ git rebase master mybranch // apply commits from origin to dev branch

# at this point I'm in mybranch so I can keep working...
#... or I can push my commits to origin/master

$ git checkout master // back to the upstream branch
$ git merge mybranch // integrate my changes
$ git push // push my changes
```

## Resources

* [YUI Git Helper](http://github.com/davglass/yui-git/)
* [GitX - OS X Git GUI](http://gitx.frim.nl/)
* [Everyday GIT With 20 Commands Or So](http://www.kernel.org/pub/software/scm/git/docs/everyday.html)
* [Git Users Manual](http://www.kernel.org/pub/software/scm/git/docs/user-manual.html)
* [Git Tutorial](http://www.kernel.org/pub/software/scm/git/docs/gittutorial.html)
* [More Git resources](http://github.com/blog/120-new-to-git)
* [Daily Git Tips](http://gitready.com/)
* [Git Community Book](http://book.git-scm.com/)
* [GitHub Guides](http://github.com/guides)
* [GitWiki](http://git.or.cz/gitwiki)
* [GitCasts](http://gitcasts.com/)
* [Git-SVN Crash Course](http://git.or.cz/course/svn.html)
* [Git Cheat Sheet](http://cheat.errtheblog.com/s/git)
* [Why Git is Better Than X](http://whygitisbetterthanx.com/)