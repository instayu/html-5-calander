
## ArraySort Change History




* Added `Y.ArraySort.naturalCompare()`, which compares two strings or numbers
  (or a number and a string) in natural order. This ensures that a value like
  'foo2' is sorted before 'foo10', whereas a standard ASCII sort would sort
  'foo10' first. [Ryan Grove]

## AsyncQueue Change History




* Fixed an issue that triggered an extra execution of a callback.
  [Ticket #2528602] [Ticket #2531758] [Ticket #2531844]

* Fixed a bug in which the until condition of a callback was evaluated
  prematurely when the previous callback paused the queue.

* Fixed a bug in which the 'complete' event would not be fired if stop was
  called from inside a callback.

## Attribute Change History




* Fixed regression introduced with the solution for setter opts, added in
  3.10.2, for cases where user subscribed to attribute change events, with
  additional arguments to be passed to the subscriber, for example:

    host.after("myattrChange", fn(e, custArg){}, context, custArgValue);
    ...
    host.set("myattr", 10, {src:"foo"});

* For performance reasons, attribute now bypasses the event subsystem, if
  there are no listeners, and sets the attribute value directly (still going
  through all the attribute infrastructure - setter, validator etc.).

## AutoComplete Change History




* Added Hungarian language support

## Base Change History



* BaseObservable now bypasses the event sub-system if there are no listeners for
  the `init` event, during construction, to optimize performance.

## Calendar Change History




* Setting `minimumDate` or `maximumDate` now correctly disables nodes before or
  after those dates. [Arnaud Didry]

* Added Hungarian language support [Gábor Kovács]

## Color Change History




* `toArray()` always returns alpha values [Pull Request #548] [Ticket #2533111]

## Console Change History




* Added Hungarian language support [Gábor Kovács]

## DataTable Change History



* Release Paginator for DataTable. DataTable's Paginator consists of a few
  files and components each with a single purpose in mind.
    Model- Mixes in Paginator-Core to provide a model for the DataTable
      Paginator
    View- Sets up a view of controls that is associated with a single model
    Controller- Binds and maintains the state between the model and the view
      as well as the interaction with DataTables other components.
    Templates- A collection of templates used by the view and the controller
      to add mark up to the layout in a unified manner. The template is
      created using `Y.Template.Micro` but can be updated to use any
      precompiled templating language.
    Skins- Night and Sam skins for the default paginator view.

* Release a default footer view that will create an empty `<tfoot>` for row
  placement in the footer node. This is optionally added by the Paginator when
  the location is specified for the footer if it is not already in place.

* Update `_afterDataChange()` to only change the row modified.
  [Pull Request #695] [Ticket #2532962]

* Expand the title change to allow for a columns title, key, abbr and label for
  more flexibility with column titles. [Pull Request #703] [Ticket #2533220]

* Added Hungarian language support [Gábor Kovács]

## Date Change History




* Added Hungarian language support [Gábor Kovács]

## Rich Text Editor Change History




* Fix exception when sel.anchorNode doesn't exist. [rgrove]

## Custom Event Infrastructure Change History




* Fixed issue with fireOnce subscribers not receiving the facade,
  if subscription came in after the fire, and the initial fire had
  no listeners (the bug was introduced in 3.10.0, with the no listener
  perf. optimizations).

  The subscribers in the broken code would have received the raw payload
  instead (e.g. {opts:foo}).

## Handlebars Change History




* Upgraded Handlebars.js to v1.0.12. See [Handlebars' release notes][v1.0.12].

[v1.0.12]: https://github.com/wycats/handlebars.js/blob/master/release-notes.md#v1012--100---may-31-2013

## IO Utility Change History




* Restore form attributes after successful upload in io-upload-iframe. [Ticket #2533186] [ipeychev]

## JSONP Change History




* Preserve base jsonp _format if {callback} found. Fixes #700 [lsmith]

## ScrollInfo Node Plugin Change History




* Added an `isNodeOnscreen()` method that returns `true` if the given node is
  within the visible bounds of the viewport, `false` otherwise. [Ryan Grove]

* Improved the performance of `getOffscreenNodes()` and `getOnscreenNodes()`.
  [Ryan Grove]

* Fixed a bug that caused `getOffscreenNodes()` and `getOnscreenNodes()` to
  return incorrect information when used on a scrollable node rather than the
  body. [Ryan Grove]

## Paginator Change History



* Initial release.

## Promise Change History




* Changed the value of `this` inside callbacks to `undefined` to match the
  Promises A+ spec.

## Tree Change History




* Added `Tree.Node#depth()`, which returns the depth of the node, starting at 0
  for the root node. [Ryan Grove]

* Added `Tree.Sortable#sort()`, which sorts the children of every node in a
  sortable tree. [Ryan Grove]

* The `Tree#createNode()`, `Tree#insertNode()`, and `Tree#traverseNode()`
  methods now throw or log informative error messages when given a destroyed
  node instead of failing cryptically (or succeeding when they shouldn't).
  [Ryan Grove]

* The `Tree.Node#isRoot()` method now returns `false` on destroyed nodes instead
  of causing an exception. [Ryan Grove]

* The `Tree.Sortable#sortNode()` and `Tree.Sortable.Node#sort()` methods now
  accept a `deep` option. If set to `true`, the entire hierarchy will be sorted
  (children, children's children, etc.). [Ryan Grove]

* Tree.Sortable: Sort comparator functions are now executed in their original
  context. When the sort comparator lives on the tree, its `this` object will be
  the tree instance. When it lives on a node, its `this` object will be the
  node. When specified as an anonymous function in an options object, its `this`
  object will be the global object. [Ryan Grove]
