YUI accepts code and documentation contributions via pull requests to the [YUI 3 GitHub repository](https://github.com/yui/yui3/). There are several steps involved in creating a pull request, but once you do it a few times you'll find it's not hard at all.

## Preparing your environment

If this is your first time making a change to YUI, you'll need to set up your coding environment to be able to build YUI and work with git.

### 1. Install git

Many Mac OS X and Linux systems already have git installed. If your system doesn't, see [How to Set Up Your Git Environment](http://yuilibrary.com/yui/docs/tutorials/git/) for instructions.

### 2. Install Node.js

[Download and install Node.js](http://nodejs.org/) if you don't already have it installed. All of YUI's build tools rely on Node.js.

### 3. Install yogi

[Yogi](http://yui.github.io/yogi/) is YUI's command line helper tool, which you'll use to build and test YUI changes.

To install Yogi using npm (which comes with Node.js), run:

```bash
$ npm -g install yogi
```

### 4. Get a GitHub account

If you don't yet have a [GitHub](https://github.com/) account, get one! You'll need it to send a pull request to YUI.

### 5. Fork YUI on GitHub

Go to [YUI's GitHub page](https://github.com/yui/yui3) and click the "Fork" button to create your own personal GitHub fork of YUI. Follow GitHub's instructions to clone the fork to your local machine, then add an `upstream` remote to your local repo that points to YUI's official repo:

```bash
$ git remote add upstream git://github.com/yui/yui3.git
```

### 6. Sign the YUI Contributor License Agreement (CLA)

If this is your first time contributing to YUI, you'll need to [digitally sign the YUI CLA](http://yuilibrary.com/contribute/cla/) so that we can accept your contributions.

## YUI's branching strategy

YUI uses three different development branches on GitHub:

* **[live-docs](https://github.com/yui/yui3/tree/live-docs)** is used for documentation changes that should go live on the YUI website as soon as possible. Code changes should never go into this branch (but API doc comment changes in code are okay).

* **[dev-master](https://github.com/yui/yui3/tree/dev-master)** is used for minor bug fixes intended for the next patch release. A patch release is a fully backwards-compatible minor release that increments YUI's minor version number (the x in 3.11.x).

* **[dev-3.x](https://github.com/yui/yui3/tree/dev-3.x)** is used for new features and significant changes that are intended for the next major release of YUI. A major release increments YUI's major version number (the x in 3.x.0). The `dev-master` branch is regularly merged into `dev-3.x`, but `dev-3.x` is only merged into `dev-master` when a major release occurs.

Before working on a change, decide which branch is appropriate for the change you want to make.

Base your change on the `live-docs` branch if it's just a documentation change. Use `dev-master` if your change is a minor bug fix. Or use `dev-3.x` if your change is a new feature or a significant bug fix.

## Making a change to YUI

### 1. Pull the latest YUI source

Before starting work on a change, make sure you have the latest YUI source.

First, decide what YUI branch you want to base your change on (see the branching strategy section above). Then `cd` to your local YUI clone and run the following commands.

**Note:** these examples assume you'll base your change on the `dev-3.x` branch, but you can replace `dev-3.x` in every example that follows with whichever development branch makes the most sense for your change.

```bash
$ git checkout dev-3.x
$ git pull upstream dev-3.x
```

### 2. Create a new topic branch for your change

It's best to develop changes in a "topic branch", which is a branch that only contains commits related to a single change. This will make merging easy later and keep your pull request nice and clean.

Think of a short but descriptive name for your topic branch, then create it like this (replace `my-topic-branch` with the name you prefer):

```bash
$ git checkout -b my-topic-branch dev-3.x
```

### 3. Make your change

Make any code, test, or documentation changes you want to make.

Keep your code changes relevant (that is, don't go around reformatting files or refactoring code that's unrelated to your change), and try to adhere to the existing coding style of any files you change.

Be sure to write unit tests for any bugs you fix or new functionality you add! We won't accept pull requests that don't include tests.

See [[Contribution Standards]] for details on YUI's code quality standards and testing guidelines.

### 4. Build and test your change.

Run `yogi build` from a module directory to build that module. Run `yogi test` from a module directory to run that module's unit tests.

### 5. Edit the `HISTORY.md` files for any modules you changed (optional)

In the source directory of every YUI module there's a file named `HISTORY.md`. This file contains a Markdown-formatted history of all the changes that have been made to that module.

If you made changes to one or more modules, please update those modules' `HISTORY.md` files and describe the changes you made. This step is optional, but it'll make the reviewer's job easier and we'll love you for it.

### 6. Commit your change

After you've tested your change and ensured that it works in all major browsers, commit it to git.

**Note:** Please commit source files and documentation only. Don't commit anything in the `build/` directory.

```bash
$ git add <one or more changed source files>
$ git commit -m "Description of the change"
```

### 7. Merge in the latest upstream changes

Be sure to merge in the latest upstream changes frequently, and especially before you submit a pull request.

```bash
$ git pull upstream dev-3.x
```

This may generate a merge commit. That's fine. If there are conflicts, you may need to resolve them in order to finish the merge. If you're not sure how to resolve conflicts, feel free to ask on the #yui IRC channel on Freenode or the [yui-contrib mailing list](https://groups.google.com/forum/#!forum/yui-contrib).

### 8. Push your branch to GitHub

When you're ready to share your changes with the world, push your topic branch to your GitHub fork of YUI. This will only modify your fork; it won't modify the official YUI repo.

```bash
$ git push origin my-topic-branch
```

### 9. Submit a pull request

After you've finished your change and pushed your topic branch to GitHub, browse to your topic branch on GitHub and click the **Pull Request** button.

Be sure to set the **base branch** dropdown to the correct YUI development branch (`live-docs`, `dev-master`, or `dev-3.x`).

![Screenshot of the "base branch" dropdown](http://f.cl.ly/items/3z2V1I23260S083p1C3P/Image%202013.05.21%204%3A18%3A36%20PM.png)

Give your pull request a descriptive title and a detailed description of the changes you made. If you added new features, describe what those features are, how they work, and why you think they're useful.

The more descriptive your pull request is, the more likely it will be reviewed quickly and accepted.

### 10. Respond to feedback on your pull request

YUI core commiters, reviewers, and other YUI users will review your pull request and may leave suggestions or other feedback, or they may ask questions about your changes. GitHub will email you a notification whenever someone comments on your pull request.

Please take feedback and criticism in a constructive spirit and answer any questions.

If a reviewer requests changes, you can make these changes in your local topic branch, commit them, and push them to your GitHub repo as described above. GitHub will automatically update the pull request with your new commits as long as you keep them in the same topic branch.

Not all pull requests will be approved. A YUI reviewer may decide that the change isn't necessary, or that a different approach would be better, or that it's just not something that should become part of YUI.

If your pull request isn't approved, don't feel bad! Your contributions are still very welcome, and we encourage you to send us more pull requests.

## Reviewers & committers: How to review and merge a PR

The information in this section is for YUI core reviewers and commiters only. If you're not a reviewer or committer, this doesn't apply to you.

**Note:** While all PRs require the approval of a reviewer, committers should merge their own PRs once a reviewer has signed off. Committers, please don't expect reviewers to merge your changes for you.

### 1. Review the code on GitHub

Read the diffs associated with the pull request. Do the proposed changes make sense? Do they fix a problem or improve YUI in a valuable way? Are they maintainable? Does the code adhere to the style and standards of the changed files and the library in general? Do they include unit tests?

Comment on code that you have questions about or that you think should be changed. Ask questions about the changes if anything needs clarification.

### 2. Build and test the changes locally

If the code changes look good and you're inclined to accept the pull request, the next step is to run unit tests and make sure they all pass.

Follow GitHub's instructions for merging the pull request into your local repo via the command line, but don't push the changes upstream yet.

After merging the changes into your local repo, build any modules whose source files changed, then run the unit tests for those modules in all major browsers. If there are failures, paste the failure info into a comment on the pull request.

### 3. Update `HISTORY.md` files and documentation if necessary

If the contributor didn't update the `HISTORY.md` files for changed modules, update them now.

If the contributor didn't include documentation and for some reason you didn't reject the pull request, then it's your job to write those docs before merging the changes.

### 4. Commit build files, etc., then merge and push!

Commit all the build files and other local changes (`HISTORY.md`, docs, etc.) you've made.

Merge the topic branch into the appropriate development branch (`live-docs`, `dev-master`, or `dev-3.x`).

```bash
$ git checkout dev-3.x
$ git merge my-topic-branch
```

If there are any conflicts, resolve them. Then push the changes upstream to automatically close the PR.

```bash
$ git push upstream dev-3.x
```