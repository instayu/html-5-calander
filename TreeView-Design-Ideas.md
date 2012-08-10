# TreeView Design Ideas

* Make content template extendable (see [ticket #2532516](http://yuilibrary.com/projects/yui3/ticket/2532516) and [pull request #192](https://github.com/yui/yui3/pull/192))

## Different template types

* Avoid the YUI 2 concept of having different TreeNode "classes".
* Instead, you might want to have a nice sugary way to register different TreeNode templates and use them by name. This could be useful if you want to generate a TreeView with mixed types of nodes.
* The default TreeNode template should just expect a label and optionally take a url.
* The default TreeNode template should make it easy to choose whether you want the label treated as text or as innerHTML. 
* TreeView should ship with at least one (preferably a few) templates that show how to have a TreeNode with a label and a checkbox, or an editable label, or [insert your favorite feature here]

## Data sources

* JS/JSON TreeViews: if the user includes extra properties, pass those down the templates.
* Progressive enhancement: Similar to JS TreeViews, often users will be enhancing markup that contains useful extra metadata -- defined in classes, or in data-* attributes, or elsewhere. Related: the author of the TreeView doesn't necessarily have much control over the original markup, so any additional knobs you give them would be helpful.
* ModelList: It should be easy to construct a TreeView on top of a ML or LazyML. 
  * By default, TreeView looks for a "label" field to populate the label and a "children" field for child MLs. However, you can configure TreeView to look for different field names.

## Useful built-in features

* Solid PE. A *major* use case for TreeView is enhancing some existing navigation.
* ARIA and keyboard navigation
* Touch support
* A basic set of ModelList / ArrayList features like each(), some() ... 

## Mixins / Extensions

* I/O Tree -- sugar for loading children by hitting some remote data source (YUI 2 TreeView had this)
* Persistent Tree -- use localStorage or cookies to preserve the open/shut state of each node across page views. Very useful for any kind of "book" or "documentation" interface. (YUI 2 TreeView did not have this)
* Router Tree -- A tree that responds to HTML History and reflects the current path -- as the user navigates around from {root}/foo/bar to {root}/baz/zot, the tree automatically closes /foo/bar and opens /baz/zot. 
* Greppable Tree -- add advanced List-like features, like grep(), filter(), ... In response to some event, I need to find a node (according to some criteria) and expand to that node.
