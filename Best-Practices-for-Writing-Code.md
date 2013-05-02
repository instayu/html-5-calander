## Diff Before Every Commit

Get into the habit of running `git diff` or `git diff --cached` before every commit.

## Commits Should Be Granular

You should keep each commit as granular as possible. For instance, do not check in 2 bug fixes in one commit -- separate them out into 2 commits.

## 4 Spaces, No Tabs

The team has decreed there will be no tabs in our code. Please set your tabs to equal 4 spaces.

## Avoid `Y.Node.setContent()` and `foo.innerHTML` unless absolutely necessary

`innerHTML` and `Y.Node.setContent()` pass data to innerHTML under the hood, which may lead developers to inadvertently write unsafe code on top of our APIs. Do not use these methods unless you actually **need** their functionality. If all you need to do is put some plain text on the page, use Y.Node's `text` attribute which is safe for user-supplied strings: