### Branch Information

YUI's development happens on five main branches. The following describes what
each of these code branches represents:

  * `live-docs`: Represents the latest release of YUI, plus any
    documentation-only updates. Any tweaks or additions to the docs for the
    latest release happen on this branch, and they are reflected on the website.

  * `master`: Contains everything in `live-docs`, plus code changes that will go
    into the next YUI release. The code changes in `master` are either bug fixes
    or small changes which should not break API compatibility. Patch releases
    will be cut from this branch; e.g. 3.6.x. *All code in this branch has fully
    passed all unit tests and should be stable.*

  * `3.x`: Represents the next major YUI release; e.g. 3.7.0. This is an
    integration branch which contains everything in `master`, plus larger code
    changes which will go into a future YUI release. The changes in `3.x`
    require a minor version increment before they are part of release; e.g.
    3.7.0. Preview Releases will be cut from this branch for developers to test
    and evaluate. *All code in this branch has fully passed all unit tests and should be stable.*

  * `dev-master` and `dev-3.x`: Current working branches containing code that
     **has not** been through the CI process. Developers check their changes in to
     these integration branches for the automated testing system to validate. Once they
     are validated, the code is merged into `master` and `3.x` respectively.

### Code Process

  * Always work from a feature branch, since all code submissions will be through a Pull Request.
  * Always start your new branch from the branch you want to submit to: `git checkout -b myfeature dev-master`
  * Remember to submit your Pull Request to the proper `dev-` branch and not `master` or `3.x`.