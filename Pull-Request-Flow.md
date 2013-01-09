Introduction
------------
Getting code into [source](https://github.com/yui/yui3) is a process that can lead to confusion, especially if it is your first time working with Git and Branch Driven Development. Here is a quick list of git commands that you may use in the life cycle of your pull request. Assume that you are creating some code that you want to go into the next release - which right now would be `3.x`. You do not ever check in directly to `3.x` or `master`. Instead you issue pull requests against `dev-3.x` or `dev-master`. The code below assumes `dev-3.x` for this example. `foo-123456` is the development branch that you will issue the pull request from. It has all your new and changed code (name it something meaningful).

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
* Do commits as you go on all files **except builds**.  You will commit build files later in the process.
* Documentation (depending on how big your changes are)
   * API Docs
   * Examples
   * User Guides



Everyday
--------

```
git checkout dev-3.x
git pull upstream dev-3.x
git checkout foo-123456
git merge dev-3.x
```

(Fix any merge issues to make sure your build is clean.)

When you are ready for a Pull Request
-------------------------------------

```
git merge dev-3.x
git push origin foo-123456
```

Issue pull request through github's ui against dev-3.x
-------------------------------------------

Be sure you have unit tests (see minimum requirements under [Contribution Standards](https://github.com/yui/yui3/wiki/Contribution-Standards))

Be sure to switch to the 'dev-3.x' branch on the GitHub site when setting up the pull request.
 
When the pr is approved
-----------------------

( **You must be a commiter or reviewer in order to actually pull in code.** See the [Contributor Model](https://github.com/yui/yui3/wiki/Contributor-Model))

```
git checkout dev-3.x
git pull upstream dev-3.x
git merge foo-123456
```

Build and add commit build files.

Edit HISTORY.md (usually with something like @VERSION@ + your change information).

Push up to dev-3.x

`git push upstream dev-3.x`

Or, if you use a local dev-3.x branch:
```
git checkout dev-3.x
git pull upstream dev-3.x
git checkout foo-123456
git merge dev-3.x
git commit -m 'Merge in dev-3.x'
git checkout dev-3.x
git merge foo-123456
git commit -m 'Merge in fix for #123456 by [anonymous]'
git push upstream dev-3.x
```
