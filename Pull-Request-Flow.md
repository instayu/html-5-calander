Introduction
------------
Getting code into src is a process that can lead to confusion, especially if it is your first time working with Git and Branch Driven Development. Here is a quick list of git commands that you may use in the life cycle of your pull request. Assume that you are creating some code that you want to go into the next release - which right now would be `3.x`. You do not ever check in directly to `3.x` or `master`. Instead you issue pull requests against `dev-3.x` or `dev-master`. The code below assumes `dev-3.x` for this example.

Bug Branch Creation
-------------------

```
git checkout dev-3.x
git pull upstream dev-3.x
git checkout -b foo-123456
```

Do code stuff (should always be pushing to origin) 

_If you have travis connected, this will show you build failures_

* do tests 
* do builds
* do commits as you go on all files but builds
* documentation
 (see [Contribution Standards](https://github.com/yui/yui3/wiki/Contribution-Standards))

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