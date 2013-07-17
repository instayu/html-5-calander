### Security First

Any input that you take from the user and inject back into the page needs to be escaped or placed into the DOM as *text* and *not HTML*.

### Diff Before Every Commit

Get into the habit of running `git diff` or `git diff --cached` before every commit.

### Commits Should Be Granular

You should keep each commit as granular as possible. For instance, do not check in 2 bug fixes in one commit -- separate them out into 2 commits.

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


### Pushes to `dev-master` and `dev-3.x` should be holistic:

Do not push code to dev-master/dev-3.x without the following:
   * Test your code
      * unit tests
      * functional tests
   * APIDocs
   * Accessibility
   * Documentation
      * commented code
      * api docs
      * full suite of examples
      * complete user guide content

Do *not* defer testing or documentation to do "later".

### Commit `src/` Files Separately from `build/` Files

When you change src/js code, you'll need to build the component to test your changes locally. This results in modified src/ AND build/ files. As a best practice, you should commit your src/ files separately from your build/ file commits.