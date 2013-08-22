## Pull Request Minimum Requirements
If you are making a pull request now please take note of the following
requirements that your pull request needs. The goal of these requirements is to ensure quality, API consistency, code reusability, and maintainability of the contribution.

   * Complete API Docs and inline code comments
   * Unit tests with 90% line coverage, tested on [Target Environments](http://yuilibrary.com/yui/environments/) 
   * User Guide (Components only)
   * Functional examples, written up in Selleck format and with [test automation](https://github.com/yui/yui3/wiki/Selleck-Example-Tests)
   * Proper commit logs
   * Proper updates to HISTORY.md

The YUI team has created a number of tools to make meeting the above requirements much easier:

   * [shifter](http://yui.github.com/shifter): to build the modules properly and consistently.
   * [yuidocjs](http://yui.github.com/yuidoc/): for live-previewing the API docs.
   * [selleck](http://yui.github.com/selleck/): for live-previewing the user guide and functional examples.
   * [yogi](http://yui.github.com/yogi): helper tool wrapping up the functionality from the above tools.
   * [Yeti](http://yeti.cx/): test automation suite for a wide range of test environments.
   * [YUI Test](http://yuilibrary.com/projects/yuitest/): a complete testing framework for JavaScript 
     and Web applications.

## Requirements for Developing Code

We recommend the following process for contributing great code to YUI:




### Security First

Any input that you take from the user and inject back into the page needs to be escaped or placed into the DOM as *text* and *not HTML*.

### Diff Before Every Commit

Get into the habit of running `git diff` or `git diff --cached` before every commit.

### Commits Should Be Granular

You should keep each commit as granular as possible. For instance, do not check in 2 bug fixes in one commit -- separate them out into 2 commits.

### Commit `src/` Files Separately from `build/` Files

When you change src/js code, you'll need to build the component to test your changes locally. This results in modified src/ AND build/ files. As a best practice, you should commit your src/ files separately from your build/ file commits.

### 4 Spaces, No Tabs

The team has determined there will be no tabs in our code. Please set your tabs to equal 4 spaces.

### Avoid `Y.Node.setContent()` and `foo.innerHTML` unless absolutely necessary

`innerHTML` and `Y.Node.setContent()` pass data to innerHTML under the hood, which may lead developers to inadvertently write unsafe code on top of our APIs. Do not use these methods unless you actually **need** their functionality. If all you need to do is put some plain text on the page, use Y.Node's `text` attribute which is safe for user-supplied strings:
```
myNode.set('text', 'some text')
```

If you do need to pass an attribute, property, or method parameter to `innerHTML`, `setContent()`, or any method that uses these under the hood, be sure to explicitly specify the data type of that member as "HTML" in the API docs. For example:
```
/**
Title HTML.
   
@attribute title
@type HTML
*/

/**
Sets this widget's title.

@method setTitle
@param {HTML} title Title to set.
*/
```




### Get feedback early and often 

* An **API review** validates your initial approach
* A **design review** validates your high-level architecture
* A **code review** validates your implementation details
* A **Preview Release** gets you community feedback of working code in real-world situations

### Documentation is just as important as code

* API docs
* Examples
* User guides
* In-line code comments

### Automate your tests

* Unit
* Functional
* Performance


## A Note About Lint

Please read: https://github.com/yui/yui-lint/blob/master/README.md

We reserve the right to one day fail builds on lint errors.

## Release Process

At the end of Code Freeze day (11:59 PM in Sunnyvale), development branches `dev-master` and `dev-3.x` will be frozen so we can make the determination on whether to cut a 3.CURRENT.NEXT release or a 3.NEXT release. A release branch will be created off the chosen development branch in preparation for release, and then all development branches will be unfrozen for continued development.

## Important Milestones

### Pull Request Milestones

Per our [Contributor Model](https://github.com/yui/yui3/wiki/Contributor-Model), pull requests require a 72-hour window for feedback. Please submit your pull request with enough time for this window, if you are trying to meet one of the milestones described below.

### Code Freeze

All source code changes for a release should be merged to the `dev-master` and `dev-3.x` development branches by Code Freeze, including new features, new APIs, deprecations, and bug fixes. This is in order to ensure enough time for thorough testing across all our target environments and community feedback before release. 

Upon Code Freeze, `dev-master` and `dev-3.x` branches will be frozen for a short period so we can create a short-lived release branch (`release-3.x.x`) in preparation for release. After the release branch is created, development branches will re-open for continuous development. Between Code Freeze and Commit Freeze, only documentation updates, test updates, and explicitly identified release blockers fixes are acceptable in a release branch.

### Commit Freeze

No repo changes of any kind are permitted after Commit Freeze to the release branch created at Code Freeze (`release-3.x.x`) without explicit discussion and approval. This is to prevent churn in our CI system that delays releases. Please make sure all code changes and test, documentation, and HISTORY.md updates happen in the release branch before Commit Freeze. 

Development branches will remain open for continuous development.


## License Updates

Any submission that uses open source code from another project must be explicitly called out and is subject to review.

## Right to Revert

Once the contribution has been merged into the repo, if any issues arise in the integration environment or upon subsequent feedback, the contribution may be reverted.