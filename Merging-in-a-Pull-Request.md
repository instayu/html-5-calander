This tutorial is for developers who want to check out a Pull Request issued by another user. This is the workflow the YUI team follows to merge in Pull Requests to the YUI projects.

## Create a New Branch

Checkout a new branch so you can review and test another user's Pull Request. In these examples you'll be working with a Pull Request issued by GitHub user `davglass` from his somefeature branch.

```
$ git fetch upstream
$ git checkout -b davglass-somefeature upstream/master --no-track
```

Pull in the code from `davglass`'s somefeature branch:

```
$ git pull https://github.com/davglass/yui3.git somefeature
```

## Review and Test Changes

You should review the code changes made in the Pull Request, and **make sure to thoroughly test them**. GitHub is great for code reviews, so use it to discuss the changes in the Pull Request with the issuer. You should suggest any adjustments you think they should make, ask them to include tests, etc. until you feel the changes are ready to be merged into `dev-master` or `dev-3.x`.

## Perform the Merge

At this point you should feel confident that the Pull Request has been fully vetted and tested, and ready to merge into your master branch.

```
$ git checkout dev-master
$ git merge davglass-somefeature
```