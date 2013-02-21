(This information is currently a WIP, but will supercede the information at [http://yuilibrary.com/yui/docs/tutorials/contribute/](http://yuilibrary.com/yui/docs/tutorials/contribute/)).

If you are new to contributing to YUI, [Contribute.md](https://github.com/yui/yui3/wiki/Contributing.md) is a good place to start.

This tutorial explains YUI's branching strategy and developer workflow for making and submitting contributions to the project.

This tutorial assumes you already have Git installed and working. If you don't, see [Tutorial: Set Up Your Git Environment](http://yuilibrary.com/yui/docs/tutorials/git/) for more info. Also be sure to [sign our CLA](http://yuilibrary.com/contribute/cla/), if you haven't already, before you contribute to YUI. 



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
     **has not** been through the CI process. Developers check their changes in to
     these integration branches for the automated testing system to validate. Once they
     are validated, the code is merged into `master` and `3.x` respectively.

## Initial Setup

   1. Fork the project on GitHub (http://www.github.com/yui/yui3).
   1. Clone the fork to your local environment for development.

## Do Good Stuff

   1. Create a feature branch to house atomic code changes.
   1. Satisfy the contribution requirements (see [YUI Contribution Standards](https://github.com/yui/yui3/wiki/Contribution-Standards)).
   1. Push changes to your fork.
   1. Submit a pull request from your fork to the `live-docs`, `dev-master`, or `dev-3.x` branch  for review.
   1. Incorporate community feedback.
   1. Push changes to your fork -- the pull request will automatically update.
   1. Rinse and repeat.

All changes should continue to be made on the feature branch; that way the pull request you submit will automatically update to include them. Make sure to keep the feature branch updated with the latest changes from master, so that they don't diverge during your development process.

## Important Tips

  * Always work from a feature branch. Since all code submissions will be through a Pull Request, feature branches isolate changes from one submission to another.
  * Always start your new branch from the branch you want to submit to: `git checkout -b myfeature dev-master`
  * Remember to submit your Pull Request to the proper `dev-` branch and not `master` or `3.x`.