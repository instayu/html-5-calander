This tutorial assumes you already have `Git` installed and working. If you don't, see [Tutorial: Set Up Your Git Environment](http://yuilibrary.com/yui/docs/tutorials/git/) for more info, also be sure to [sign our CLA](http://yuilibrary.com/contribute/cla/) if you haven't already before you contribute to YUI.

This tutorial explains how to set up your environment to make contributions and how to make individual pull requests.

For more advanced information visit our Developer Workflow wiki on Github.

## Initial Setup

### Fork YUI

Log into GitHub and visit the YUI 3 project page on GitHub: http://github.com/yui/yui3/.

[[img/fork.png]]

Now you need to create **your fork** by clicking the [[img/fork_button.png]] button. When the forking process completes, you will be presented with information about your new repository.

**Note:** These examples were created while logged in as the `yui-contrib` user, you should substitute `yui-contrib` with your GitHub username.

[[img/after-fork.png]]

### Clone Your YUI Fork Locally

Clone your newly created fork by running `git clone [url]`, where url is **"Your Clone URL"** (and not the "Public Clone URL"). Cloning copies your fork onto your local machine. For example:

```
$ git clone git@github.com:yui-contrib/yui3.git
```

The output of the above command will look something like this:

```
Initialized empty Git repository in /src/dev/contrib/yui3/.git/
remote: Counting objects: 31520, done.
remote: Compressing objects: 100% (8945/8945), done.
remote: Total 31520 (delta 21295), reused 30725 (delta 20682)
Receiving objects: 100% (31520/31520), 12.57 MiB | 1814 KiB/s, done.
Resolving deltas: 100% (21295/21295), done.
```

### Add the Upstream Repository

Add a remote repository pointing back to the main YUI fork. This establishes a relationship between your local git repository and the upstream project that you forked from, which in turn makes it easy to stay up to date with the official YUI repository. This step needs to be done from inside the project you just cloned.

```
$ cd yui3
$ git remote add upstream git://github.com/yui/yui3.git
```

After adding the upstream remote repository, you can update your fork at any time by running:

```
$ git pull upstream master
```

You should see output similar to the following:

```
From git://github.com/yui/yui3
* [new branch]      master     -> upstream/master
Already up-to-date.
```

_This just created the `upstream/master` branch in your local repository. It's used to track upstream changes that happen on the official YUI fork._

**Run `git pull upstream master` often to make sure that you're up to date with the latest YUI source;** when there are upstream changes the output will look something like this:

```
From git://github.com/yui/yui3
3dccf5b..99efb0c  master     -> upstream/master
* [new tag]         yui3-644   -> yui3-644
From git://github.com/yui/yui3
* [new tag]         yui3-643   -> yui3-643
Merge made by recursive.
api/event-target.js.html                 |   12 ++++++------
build/event-custom/event-custom-debug.js |   10 +++++-----
build/event-custom/event-custom-min.js   |    4 ++--
build/event-custom/event-custom.js       |   10 +++++-----
build/yui-base/yui-base-debug.js         |   19 ++++++++++++++-----
build/yui-base/yui-base-min.js           |    4 ++--
build/yui-base/yui-base.js               |   19 ++++++++++++++-----
build/yui/yui-debug.js                   |   19 ++++++++++++++-----
build/yui/yui-min.js                     |    4 ++--
build/yui/yui.js                         |   19 ++++++++++++++-----
src/event-custom/js/event-target.js      |   10 +++++-----
src/yui/js/yui-array.js                  |   19 ++++++++++++++-----
12 files changed, 97 insertions(+), 52 deletions(-)
```

## Contributing Changes

### Branch-Based Workflow

Each time you start working on a set of related changes to YUI, create a topic branch. Isolating your changes to a branch makes it easy to resolve conflicts with the upstream repository. First, make sure your repository is up to date with upstream and create a new topic branch (replace myfeature with a meaningful branch name):

```
$ git fetch upstream
$ git checkout -b myfeature upstream/master --no-track
```

_Edit some files, add some features, fix some bugs, and frequently commit changes to your topic branch._

```
$ git commit -am "Give a good description here, better than this one."
```

Pull any `upstream` changes into your branch and **test your changes** against this latest code from the main YUI project repository.

```
$ git pull upstream master
```

Push your topic branch up to GitHub and **submit a Pull Request** from your `myfeature` topic branch.

```
$ git push origin myfeature
```

### Submit a Pull Request

Pull requests notify the YUI Team that you want us to pull your code and start the process of getting it merged into the official release. We accept pull requests via [GitHub's Fork + Pull Model](http://help.github.com/send-pull-requests/).

### Reference Bug #s in Commit Messages

Commit messages are parsed and the referenced GitHub issue will be linked.

The following syntax is supported:

```
$ git commit -m "fix #1234"
$ git commit -m "fixes #1234"
$ git commit -m "fixed #1234"
$ git commit -m "close #1234"
$ git commit -m "closes #1234"
$ git commit -m "closed #1234"
```

If you are actively developing, this will save you time and let the reporter of the issue know that it has been fixed.