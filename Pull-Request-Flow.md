Introduction
------------
Getting code into src is a process that can lead to confusion, especially if it is your first time working with Git and Branch Driven Development. Here is a quick list of git commands that you may use in the life cycle of your pull request. Assume that you are creating some code that you want to go into the next release - which right now would be `3.x`. You do not ever check in directly to `3.x` or `master`. Instead you issue pull requests against `dev-3.x` or `dev-master`. The code below assumes `dev-3.x` for this example. `foo-123456` is the development branch that you will issue the pull request from. It has all your new and changed code (name it something meaningful).

Bug Branch Creation
-------------------

```
git checkout dev-3.x
git pull upstream dev-3.x
git checkout -b foo-123456
```

Do code stuff. You should always be pushing to origin.
(see [Contribution Standards](https://github.com/yui/yui3/wiki/Contribution-Standards)) 

_If you have travis connected, this will show you build failures_

* Do tests. `yogi test`
* Do builds. `yogi build`
* do commits as you go on all files **except builds** you will commit build files later in the process
* documentation



Everyday
--------

```
git checkout dev-3.x
git pull upstream dev-3.x
git checkout foo-123456
git merge dev-3.x
```

(Fix any merge issues to make sure I'm clean)

When you are ready for a Pull Request
-------------------------------------

```
git merge dev-3.x
git push origin foo-123456
```

issue pr through github's ui against dev-3.x
-------------------------------------------

be sure you have unit tests

when the pr is approved
-----------------------


```
git checkout dev-3.x
git pull upstream dev-3.x
git merge foo-123456
```

build and add commit build files

push up to dev-3.x

`git push upstream dev-3.x`