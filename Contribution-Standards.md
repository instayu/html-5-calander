## Propose a Submission

Thank you for your interest in contributing to the YUI project! Before we get started, please be sure to [sign a CLA](http://yuilibrary.com/contribute/cla/).

Proposals can be submitted via a pull request or as an idea to the Contributor Mailing List. Submissions that follow our contribution standards and are aligned with the direction of the project will be accepted. Submissions that are not accepted can always be published to YUI Gallery.

Please review YUI’s [Contributor Model](https://github.com/yui/yui3/wiki/Contributor-Model/) for more information about how proposals get processed once submitted.

## Development Workflow

Please review YUI’s [Developer Workflow](https://github.com/yui/yui3/wiki/Developer-Workflow/) for details on how to set up your Git branches and contribute changes to the YUI project.

## Minimum Requirements

The goal of these requirements is to ensure quality, API consistency, code reusability, and maintainability of the contribution. All contributions must satisfy:

   * Complete API Docs and inline code comments
   * Unit tests with 80% line coverage
   * User Guide (Components only)
   * Functional examples, written up in Selleck format and with test automation (https://github.com/yui/yui3/wiki/Selleck-Example-Tests)
   * Proper commit logs
   * Proper updates to HISTORY.md

The YUI team has created a number of Node.js-based NPM modules to make meeting the above requirements much easier:

   * [shifter](http://yui.github.com/shifter): to build the modules properly and consistently.
   * [yuidocjs](http://yui.github.com/yuidoc/): for live-previewing the API docs.
   * [selleck](http://yui.github.com/selleck/): for live-previewing the user guide and functional examples.
   * [yogi](http://yui.github.com/yogi): helper tool wrapping up the functionality from the above tools.

## Further Recommendations

We recommend the following process for contributing great code to YUI:

### Get feedback early and often 

* An **API review** validates your initial approach
* A **design review** validates your high-level architecture
* A **code review** validates your implementation details
* A **Preview Release** gets you community feedback of working code in real-world situations

### Documentation is just as important as code

* API docs
* Examples
* User guides

### Automate your tests

* Unit
* Functional
* Performance

## A Note About Lint

Please read: https://github.com/yui/yui-lint/blob/master/README.md

We reserve the right to one day fail builds on lint errors.

## Important Milestones

### Feature Complete

All big ticket items should be merged in by Feature Complete. This is in order to ensure enough time for testing and community feedback before release. Big ticket items include new features, new APIs, large code changes, deprecations, and upstream changes that may impact other code.

### Code Freeze

No code changes of any kind are permitted after code freeze without explicit discussion and approval. This is to prevent churn that delays releases. Please make sure all bug fixes, test updates, documentation, and HISTORY.md updates happen before code freeze.

The time between the `Feature Complete` milestone and the `Code Freeze` milestone is meant for late-breaking bug fixes of a smaller nature that come out of community feedback and testing.


### Preview Releases

Coming soon.

## License Updates

Any submission that uses open source code from another project must be explicitly called out and is subject to review.

## Right to Revert

Once the contribution has been merged into the repo, if any issues arise in the integration environment or upon subsequent feedback, the contribution may be reverted.