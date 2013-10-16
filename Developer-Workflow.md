(This information supplements the information at [http://yuilibrary.com/yui/docs/tutorials/contribute/](http://yuilibrary.com/yui/docs/tutorials/contribute/)).

If you are new to contributing to YUI, [Contribute.md](https://github.com/yui/yui3/blob/master/CONTRIBUTING.md) is a good place to start.

This document explains YUI's branching strategy and developer workflow for making and submitting contributions to the project.

This document assumes you already have Git installed and working. If you don't, see [Tutorial: Set Up Your Git Environment](http://yuilibrary.com/yui/docs/tutorials/git/) for more info. Also be sure to [sign our CLA](http://yuilibrary.com/contribute/cla/), if you haven't already, before you contribute to YUI. 



## Branch Information

YUI's development happens on five main branches. The following describes what
each of these code branches represents:

  * `live-docs`: Represents the latest GA release of YUI, plus any
    documentation-only updates. Any tweaks or additions to the docs for the
    latest release happen on this branch, and they are reflected on the website.

  * `master`: (Read-only) Contains everything in `live-docs`, plus code changes that will go
    into the next YUI release. The code changes in `master` are either bug fixes
    or small changes which should not break API compatibility. Patch releases
    will be cut from this branch; e.g. 3.6.x. *All code in this branch has fully
    passed all unit tests and should be stable.*

  * `3.x`: (Read-only) Represents the next major YUI release; e.g. 3.7.0. This is an
    integration branch which contains everything in `master`, plus larger code
    changes which will go into a future YUI release. The changes in `3.x`
    require a minor version increment before they are part of release, e.g.,
    3.7.0. Preview Releases will be cut from this branch for developers to test
    and evaluate. *All code in this branch has fully passed all unit tests and should be stable.*

  * `dev-master` and `dev-3.x`: Current working branches containing code that
     **has not** been through the CI process. **Developers check their changes in to**
     **these integration branches for the automated testing system to validate.** Once they
     are validated, the code is merged into `master` and `3.x` respectively. **Never** check in to
     `master` or `3.x` directly.

  * `release-3.x.x`: Short-lived release branches where code checkins are carefully managed for extensive testing and release deployment.

## Preparing your environment

If this is your first time making a change to YUI, you'll need to set up your coding environment to be able to build YUI and work with git.

### 1. Install git

Many Mac OS X and Linux systems already have git installed. If your system doesn't, see [How to Set Up Your Git Environment](http://yuilibrary.com/yui/docs/tutorials/git/) for instructions.

### 2. Install Node.js

[Download and install Node.js](http://nodejs.org/) if you don't already have it installed. All of YUI's build tools rely on Node.js.

### 3. Install yogi

[Yogi](http://yui.github.io/yogi/) is YUI's command line helper tool, which you'll use to build and test YUI changes. (You may also need to install [phantomjs](http://phantomjs.org/).)

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


## Making a change to YUI

### 1. Pull the latest YUI source

Before starting work on a change, make sure you have the latest YUI source.
Your YUI fork should:
* Always be up-to-date with dev-master
* Always be pushed to daily (get upstream changes and push to your fork).
* Always be in sync with your current work.

First, decide what YUI branch you want to base your change on (see the branching strategy section above). Then `cd` to your local YUI clone and run the following commands.

**Note:** these examples assume you'll base your change on the `dev-3.x` branch, but you can replace `dev-3.x` in every example that follows with whichever development branch makes the most sense for your change.

```bash
$ git checkout dev-3.x
$ git pull upstream dev-3.x
```

### 2. Create a new topic branch for your change

It's best to develop changes in a "topic branch", which is a branch that only contains commits related to a single change. This will make merging easy later and keep your pull request nice and clean. Use `dev-master` or `dev-3.x` as your base branch, depending on the scope of your change.

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

Run `yogi build` from a module directory to build that module. Run `yogi test` from a module directory to run that module's unit tests. Please note `yogi test` uses `PhantomJS` to test your code. If you wish to test your code within a browser, run `yeti <name>.html`, where `name` is the name of the HTML file which contains your tests. Please make sure your code tests successfully in all of the environments located [here](http://yuilibrary.com/yui/environments/) before submitting your pull request.

Please note when adding, or removing modules from the `src` directory, you must regenerate the `meta` data for the YUI seed file. You can do this by running the `yogi loader` command from the `src` directory, which will regenerate the `meta` data and rebuild the seed file.

### 5. Edit the `HISTORY.md` files for any modules you changed (optional)

In the source directory of every YUI module there's a file named `HISTORY.md`. This file contains a Markdown-formatted history of all the changes that have been made to that module.

If you made changes to one or more modules, please update those modules' `HISTORY.md` files and describe the changes you made. This step is optional, but it'll make the reviewer's job easier and we'll love you for it.

If this is the first entry for this new version, and it's not already there, include an entry like this:

```
@VERSION@
------

* [your info here]
```

This token will be replaced by the correct version at release time.


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

If this is **ongoing work** you should prefix the title of the pull request with **"[WIP] some new feature"** and push to that branch often. This keeps a record of your progress. If you want feedback from another member of the YUI community, simply use the **@username** syntax in a comment and ask them to take a look.

### 10. Respond to feedback on your pull request

YUI core commiters, reviewers, and other YUI users will review your pull request and may leave suggestions or other feedback, or they may ask questions about your changes. GitHub will email you a notification whenever someone comments on your pull request.

Please take feedback and criticism in a constructive spirit and answer any questions.

If a reviewer requests changes, you can make these changes in your local topic branch, commit them, and push them to your GitHub repo as described above. GitHub will automatically update the pull request with your new commits as long as you keep them in the same topic branch.

Not all pull requests will be approved. A YUI reviewer may decide that the change isn't necessary, or that a different approach would be better, or that it's just not something that should become part of YUI.

If your pull request isn't approved, don't feel bad! Your contributions are still very welcome, and we encourage you to send us more pull requests.

## Building YUI

### Steps

For alternate instructions, see https://github.com/yui/yui3/issues/916#issuecomment-25738494

* Set up your environment as described above. You should have `yogi` installed and have a local clone of YUI on your development machine.

* Go to the directory you want to build within YUI and just run `$ yogi build`. (`yogi` uses `shifter` under the hood.)
   * For example `$ cd yui3/src/anim & yogi build`
   * Output goes to `../../build`

### Tips

* For help with `yogi` just run `yogi --help`
* Make sure you are always running the latest version of `yogi`
 
## Reviewers & committers: How to review and merge a PR

The information in this section is for YUI core reviewers and commiters only. If you're not a reviewer or committer, this doesn't apply to you.

**Note:** While all PRs require the approval of a reviewer, committers should merge their own PRs once a reviewer has signed off. Committers, please don't expect reviewers to merge your changes for you.

### 1. Review the code on GitHub

Read the diffs associated with the pull request. Do the proposed changes make sense? Do they fix a problem or improve YUI in a valuable way? Are they maintainable? Does the code adhere to the style and standards of the changed files and the library in general? Do they include unit tests? If they do not include unit tests, it will be **your** responsibility to write them.

Comment on code that you have questions about or that you think should be changed. Ask questions about the changes if anything needs clarification.

### 2. Build and test the changes locally

If the code changes look good and you're inclined to accept the pull request, the next step is to run unit tests and make sure they all pass. If there are any downstream dependencies, verify that their unit tests continue to pass as well.

Follow GitHub's instructions for merging the pull request into your local repo via the command line, but don't push the changes upstream yet.

After merging the changes into your local repo, build any modules whose source files changed, then run the unit tests for those modules in all major browsers. If there are failures, paste the failure info into a comment on the pull request.

Consider asking another YUI community member to review the code as a sanity check.

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


### 5. After you push: 

Immediately verify that the automated build passes all unit tests and no breakage has occurred as a result of checking the code in.

### 6. If you pushed to `dev-master` you must merge `dev-master` into `dev-3.x`.

## Merging fixes into a release branch

1. Find the most recent common commit between your dev branch (i.e. `dev-3.x`) and a release branch (i.e. `release-3.12.0`). 

  To discover this common commit, use something like:

  ```
  $ git merge-base dev-3.x release-3.12.0
  ```

2. Create a new branch from that commit.

3. Cherry-pick your changes into that new branch (from your own development branch say `bugfix-1234`).

4. Issue a pull request against the release branch and state which other `dev-*` branch it should be merged into.

5. **Reviewers only**: Merge that branch into both the dev branch (i.e. `dev-3.x`) and release branch (i.e. `release-3.12.0`). 

## References
* [shifter](http://yui.github.com/shifter) - Build YUI and Gallery - `sudo npm -g i shifter`
* [yogi](http://yui.github.com/yogi) - ( **Y**UI **o**r **G**allery **I**nterface )  Command Line Helper for YUI - `sudo npm -g i yogi`
* [Grover](http://github.com/davglass/grover) - YUITest wrapper for PhantomJS - `sudo npm -g i grover` (Make sure you have [phantomjs](http://phantomjs.org/) installed)
* [Yeti](http://yeti.cx/) - Automates tests written with QUnit, Jasmine, Mocha with Expect.js assertions, Dojo Objective Harness, or YUI Test.
* [UglifyJS](https://github.com/mishoo/UglifyJS) - Used to compress js
* [Istanbul](https://github.com/yahoo/istanbul) - Code coverage tool
* [GearJS](https://github.com/yahoo/gear) - Build System for Node.js and the Browser