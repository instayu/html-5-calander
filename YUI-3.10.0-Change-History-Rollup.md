### App Framework Change History

#### Model

* Fixed: The `options` object passed to Model's `setAttrs()` method was being
  modified. Now a shallow copy of this object is now created so that the
  `_transaction` property is added to the copy and not the passed-in object.
  [#598]

### Attribute Change History

* Significant performance improvements in common Attribute operations.

  For example, on Chrome:

      `get()` is 4 times faster
      `set()` is 3 times faster

  Major performance related changes are listed below.

  Commit messages have detailed descriptions of incremental changes, and the
  benefits introduced.

* We retrieve and pass the internally stored attribute configuration in State
  by reference in a lot more places, across methods, results in less function
  hops, and removing the need for each method to go and ask for the configuration.

* Avoid the delete operator for transient configuration properties, and just set
  to null or other falsey values as appropriate.

* Store final attribute config in State by reference, as opposed to merging
  since it's isolated already higher up in the call stack.

### AutoComplete Change History
* (Add italian language files to the components. [albertosantini])

### Base Change History

* Significant performance improvements in common Base/BaseCore operations.

  For example, on Chrome:

    `new BaseCore()` is 3 times faster
    `BaseCore set()` is 3 times faster
    `BaseCore get()` is 5 times faster

  In addition to the above basic `BaseCore` numbers, improvements in CustomEvent
  performance, result in the following improvements for `Base`

    `new Base()` is 4 times faster
    `Base set()` is 4 times faster
    `Base get()` is 5 times faster

  Major performance related changes are listed in the list of updates below.

  Commit messages have detailed descriptions of incremental changes, and the
  benefits introduced.

* [!] The result of static `ATTRS` aggregation is now cached during the creation of
  the first instance of a given "class", and the cached results are reused for
  subsequent instances.

  This provides significant performance benefits, but has the potential to introduce
  a backwards compatibility issue in the hopefully rare circumstance that you're
  modifying the static ATTRS collection directly, after the first instance is created.

  [!] If you are modifying static `ATTRS` collection directly after an instance is
  created (e.g. if an optional module comes in and updates the collection dynamically),
  you will need to change the implementation to use the static `Y.Base.modifyAttrs()`
  or `Y.BaseCore.modifyAttrs()` method, so we can mark the cached aggregation 
  dirty, and recompute it.

      `Y.Base.modifyAttrs(MyClass, {..changes to merge..})`

  `Base.create` and `Base.mix` will take care of this internally, so you only need 
  to use the above methods if your own code is touching the ATTRS object on a class.
  Additionaly, `Base.create` and `Base.mix` will add the `modifyAttrs` to your created
  class, so you can also call it directly on the class. e.g. 

      `MyCreatedClass.modifyAttrs({..changes to merge..})`


### Charts Change History

  * #2533184 Addressed issue in which Axis.getEdgeOffset was returning an incorrect value.
  * #2533130 Added hideFirstMajorUnit and hideLastMajorUnit attributes to axis classes allowing for suppression of rendering the first/last label and tick on an axis.
  * #2533128 Add ability for axis to generate labels and their position from an array of values. 


### Color Change History 
 * (Allow upper and lowercase to values for convert(). Also return original value if an invalid to value is provided. Fixes #583)

### Console Change History
* (Add italian language files to the components. [albertosantini])

### CSS Grids Change History
* (remove previous text and images, use lorem ipsum and placeholder text instead.)

### DataTable Change History
* (Fix renderBody in the docs and in table-message. [albertosantini])

### Event-custom Change History
* Significant performance improvements in common CustomEvent operations.

  There are improvements across the board, but the work was largely aimed at events
  with no listeners (to facilate speeding up `new Base()` which publishes/fires 2
  events [init, initializedChange], which usually don't have listeners).

  For example, on Chrome:

      `fire() with 0 listeners` is 6 times faster
      `fire() with 2 listeners` is 2-3 times faster (w, w/o payload)
      `publish()` is 2 times faster
      `publish() compared to _publish()` is 5 times faster (see below)
      `EventTarget construction + publish + fire with 0 listeners` is 3 times faster

  Major performance related changes are listed below.

  Commit messages have detailed descriptions of incremental changes, and the
  benefits introduced.

* Moved more properties to the `CustomEvent` prototype, to improve publish costs

* Instantiate `_subscribers`, `_afters` arrays lazily to reduce publish costs for the
  no listener case. Same thing was also done for less commonly used features, like the
  `targets` map.

* Reduce `new EventTarget` costs, by removing default properties which just match the
  `CustomEvent` defaults. It reduces the number of properties we need to iterate each time
  we mix values while publishing.

* Removed unrequired `Y.stamp` on _yuievt. It wasn't being used in the library code base

* Changed `Y.stamp` calls to `Y.guid` where it was being used to set up `id` properties.
  There didn't seem to be a need to add the `_yuid` property and it added overhead.

* Provide a fast-track for `fire` with no potential subscribers (no local subscribers, no
  bubble targets, and no broadcast), by jumping to the default function directly (if
  configured) or just doing nothing, if no default function.

* Made `*` support close to zero cost for folks who aren't using it, by only trying to look
  for siblings if someone had subscribed using `*`.

* Reduced `isObject` checks, by combining facade creation and argument manipulation
  into `_getFacade()`.

* Improved `fireComplex` times, by creating lesser used queues lazily (`es.queue`, `es.afterQueue`).

* Avoid `slice` and related arguments iteration costs for common `fire` signatures,
  (`fire("foo")`, `fire("foo", {})`) by working with arguments directly for these cases.

  Since `fire` is open-ended in terms of it's number of args, anything besides the above
  signatures still use `slice`.

* `fire(...)` now delegates to `_fire(array)` to avoid repeated conversion of `arguments` to
   arrays, across the calling stack from `eventTarget.fire()` to `customEvent.fire()`.

* Avoid `_monitor()` hops, but checking for whether or not monitoring is enabled outside
  of the function.

* Removed `Y.cached` wrapper around `_getType()`. This was an interesting one. The work
  we do to generate the key for the cache, turned out to be more than what `_getType()` costs
  if we just re-run it.

* Added a fast-path *currently private* `_publish()` for low-level, critical path
  implementations, such as Attribute and Base.

  `_publish()` doesn't provide any API sugar (e.g. type to fulltype conversation), and
  leaves the `CustomEvent` configuration to the caller to avoid iteration and mixing costs.

  The assumption is that low-level callers know about the event system architecture, and
  know what they're doing. That's why its private for now, but its 5x faster than `publish()`
  for a comparable event configuration. `publish()` leverages `_publish()`, also ends up being
  faster after this change, but not by such a big factor.

 * (Revert EventTarget back to lazily creating `targets` [ericf])

### Node Change History
* Fix node.all() to return an empty NodeList if the node was destroyed - Fixes #580 (hat tip Dallas Wheeler)

### OOP Utilities Change History
* Updated `Y.clone()` to always quit early and not try to clone DOM nodes.
  Common host objects like DOM nodes cannot be "subclassed" in Firefox and old
  versions of IE. Trying to use `Object.create()` or `Y.extend()` on a DOM node
  will throw an error in these browsers.

Tree Change History

* Added `Tree#findNode()` and `Tree.Node#find()` methods, which pass the
  specified node and each of its descendants to a callback function and returns
  the first node for which the callback returns a truthy value. [Ryan Grove]

* Added `Tree#traverseNode()` and `Tree.Node#traverse()` methods, which pass the
  specified node and each of its descendants to a callback function in
  depth-first order. [Ryan Grove]

* Added a `Tree.Sortable` extension, which can be mixed into any Tree class to
  provide customizable sorting logic for nodes. [Ryan Grove]

* Fixed: The number returned by `Tree#size()` didn't include the root node.
  [Ryan Grove]

### YUI Loader Change History

* Removed the default `build` directories from Loader generated combo URL's

### Profiler Change History

* [!] DEPRECATED: This module will be removed from the library in a future version.

### Widget Change History
* Added custom prefix support to widget.getSkinName,
    derived https://github.com/yui/yui3/pull/327


### Tree Change History
* Added `Tree#findNode()` and `Tree.Node#find()` methods, which pass the
  specified node and each of its descendants to a callback function and returns
  the first node for which the callback returns a truthy value. [Ryan Grove]

* Added `Tree#traverseNode()` and `Tree.Node#traverse()` methods, which pass the
  specified node and each of its descendants to a callback function in
  depth-first order. [Ryan Grove]

* Added a `Tree.Sortable` extension, which can be mixed into any Tree class to
  provide customizable sorting logic for nodes. [Ryan Grove]

* Fixed: The number returned by `Tree#size()` didn't include the root node.
  [Ryan Grove]

### YUI Core Change History
* (Add ability to filter log messages by threshold [andrewnicols])