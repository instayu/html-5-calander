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

* Base and BaseCore now add all ATTRS definitions, across the hierarchy,
  in a single shot. Prior to this change, they used to be added a class
  at a time.

  That is, for Foo extends Bar, the order of operations used to be:

  1) Add Bar ATTRS
  2) Call Bar initializer
  3) Add Foo ATTRS
  4) Call Foo initializer

  Now it is:

  1) Add Foo and Bar's ATTRS together
  2) Call Bar initializer
  3) Call Foo initializer

  This means there's a subtle order of operation change. There may potentially
  be setters/getters/valueFns in Foo, which expected Bar's initializer to have
  been executed already. This is expected to be rare, and the change fixes
  issues encountered in real-world code where setters/getters/valueFns in superclass
  ATTRS overidden in a subclass, wouldn't be able to access the subclass' attributes.

  See the Base and BaseCore API docs and the base-core unit tests for more 
  details.


## Calendar Change History

* Cleaned up lang (see PR #878) [Jeroen Versteeg]:
  * removed unused lang/calendar (only lang/calendar-base is used)
  * removed unused short_weekdays strings from lang/calendar-base
  * replaced weekdays strings from lang/calendar-base with datatype/date-format

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

## DOM Change History

* Fixed: `Y.Selector` could return an incorrect number of elements in browsers
  that don't support support `getElementsByTagName()` or `querySelectorAll()` on
  document fragments. [Ezequiel Rodriguez]

* Fixed: In Opera, `Y.Selector` failed to include selected `<option>` elements
  when the `:checked` pseudo-selector was used. [Jeroen Versteeg]

## Rich Text Editor Change History

* Fix exception when sel.anchorNode doesn't exist. [rgrove]

## Custom Event Infrastructure Change History

* Fixed issue with fireOnce subscribers not receiving the facade,
  if subscription came in after the fire, and the initial fire had
  no listeners (the bug was introduced in 3.10.0, with the no listener
  perf. optimizations).

  The subscribers in the broken code would have received the raw payload
  instead (e.g. {opts:foo}).

## ValueChange Change History

* Added support for `stopPropagation()` and `stopImmediatePropagation()` on the
  `valuechange` event facade. [Wei Wang]

## Handlebars Change History

* Upgraded Handlebars.js to v1.0.12. See [Handlebars' release notes][v1.0.12].

[v1.0.12]: https://github.com/wycats/handlebars.js/blob/master/release-notes.md#v1012--100---may-31-2013

## IO Utility Change History

* Restore form attributes after successful upload in io-upload-iframe. [Ticket #2533186] [ipeychev]
* Upgraded `request` module dependency for `io-nodejs` for compatibility with
  Node.js v0.10. [Pull Request #940]

## JSONP Change History

* Preserve base jsonp _format if {callback} found. Fixes #700 [lsmith]

## Node Change History

* Added: `Node#getHTML()` now works when used against document fragments. [Ezequiel Rodriguez]

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

## Plugin Change History
 
* Added `onceHostEvent` and `onceAfterHostEvent` methods.

## Promise Change History

* Changed the value of `this` inside callbacks to `undefined` to match the
  Promises A+ spec.

## YUI Test Change History

* Modified YUITest.hasNoKeys() to bypass Android 2.3.x prototype
  enumeration bug. (GH #949)

## Tree Change History

* Added `Tree.Node#depth()`, which returns the depth of the node, starting at 0
  for the root node. [Ryan Grove]

* Added `Tree.Sortable#sort()`, which sorts the children of every node in a
  sortable tree. [Ryan Grove]

* `Tree#emptyNode()` now removes nodes without triggering a node map reindex for
  each node, which makes it significantly faster when emptying a node with lots
  of children. [Ryan Grove]

* When inserting a node that already exists in the same parent (which results in
  that node being removed and then re-inserted), `Tree#insertNode()` now
  adjusts the insertion index to ensure that the node is re-inserted at the
  correct position after being removed, even if that position has shifted as a
  result of the removal. [Ryan Grove]

* The `remove` event is now fired when a node is removed and re-inserted as the
  result of a `Tree#appendNode()`, `Tree#insertNode()`, or `Tree#prependNode()`
  call. Previously, the node was removed silently with no event.

  The `src` property of the `remove` event facade in this case will be set to
  "add". Filter on this source if you want to ignore these events. [Ryan Grove]

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

## Widget Change History

* The Widget HTML_PARSER implementation has been updated to use the new 
  _preAddAttrs() hook in Base, since Base now adds all attributes across
  the hierarchy in one shot. Widget HTML_PARSER requires contentBox/srcNode,
  and related attributes to be set up first.

  This is purely an internal implementation change at the base Widget layer,
  and there is no impact to existing implementations. 

## Widget Buttons Change History

* Moved implementation code from the Constructor to the `initializer`
  to account for Base order of operation changes in this release.

  This is one of the older extensions which needed to be upgraded
  after `initializer` support was added for extensions.

  This has no end user impact.

## Widget Position Change History

* Moved implementation code from the Constructor to the `initializer`
  to account for Base order of operation changes in this release.

  This is one of the older extensions which needed to be upgraded
  after `initializer` support was added for extensions.

  This has no end user impact.

## Widget Position Align Change History

* Moved implementation code from the Constructor to the `initializer`
  to account for Base order of operation changes in this release.

  This is one of the older extensions which needed to be upgraded
  after `initializer` support was added for extensions.

  This has no end user impact.

## Widget Position Constrain Change History

* Moved implementation code from the Constructor to the `initializer`
  to account for Base order of operation changes in this release.

  This is one of the older extensions which needed to be upgraded
  after `initializer` support was added for extensions.

  This has no end user impact.

## Widget Stack Change History

* Moved implementation code from the Constructor to the `initializer`
  to account for Base order of operation changes in this release.

  This is one of the older extensions which needed to be upgraded
  after `initializer` support was added for extensions.

  This has no end user impact.

## Widget Std Mod Change History

* Fixed: `fillHeight` didn't work correctly when a section's content was set
  after rendering. [Jeroen Versteeg]

* Moved implementation code from the Constructor to the `initializer`
  to account for Base order of operation changes in this release.

  This is one of the older extensions which needed to be upgraded
  after `initializer` support was added for extensions.

  This has no end user impact.

## YUI Core Change History

* `Y.Array.dedupe()` is now slightly faster in ES5-compliant browsers.
  [Ezequiel Rodriguez]

* Brought `Y.Lang.trim()`, `trimLeft()`, and `trimRight()` into compliance with
  ES5, and added feature tests to ensure that native implementations are only
  used if they work properly. [Ezequiel Rodriguez]

* `Y.Object.keys()` now falls back to the non-native shim for Android 2.3.x
  because the native version incorrectly enumerates the `prototype` property.

* `Y.UA` now correctly identifies IE 11. [Ryan Grove]

* `Y.UA` now identifies Opera 15+ as both Opera and WebKit. Previously it was
  identified as Chrome, since it uses the same Blink rendering engine as
  Chrome. [Ryan Grove]

* Removed all instances of `path.existsSync()` from YUI core, as part of
  node.js target environments being brought up to v0.8. [Clarence Leung]