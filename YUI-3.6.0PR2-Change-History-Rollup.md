YUI 3.6.0 Change History Rollup
===============================

The changes included in the YUI 3.6.0 up to PR2 are listed below, per component.  Components not listed were not changed in 3.6.0PR2.

App Framework Change History
============================

### App

* Added static property: `Y.App.serverRouting`, which serves as the default
  value for the `serverRouting` attribute of all apps. [Ticket #2532319]

* Organized all CSS classes `Y.App` uses under a static `CLASS_NAMES` property.

### App Transitions

* Fixed issue with non-collapsing white space between views while transitioning.
  White space is now fully collapsed and prevents views from jumping after a
  cross-fade transition. [Ticket #2532298]

* Moved `transitioning` CSS classname under `Y.App.CLASS_NAMES`.

### ModelList

* The `add()` method now accepts an `index` option, which can be used to insert
  the specified model(s) at a specific index in the list. [Greg Hinch]

* The `each()` and `some()` methods now iterate over a copy of the list, so it's
  safe to remove a model during iteration. [Ticket #2531910]

* The `remove()` method now optionally accepts the index of a model to remove
  (or an array of indices). You no longer need to specify the actual model
  instance(s), although that's still supported as well.

* Fixed an issue where a list that received bubbled events from a model would
  assume the model was in the list if its `id` changed, even if the model
  actually wasn't in the list and was merely bubbling events to the list.
  [Ticket #2532240]

### Router

* [!] Changed how hash-based paths interact with the URL's real path. The
  path-like hash fragments are now treated as a continuation of the URL's path
  when the router has been configured with a `root`. [Ticket #2532318]

* Fixed issue when multiple routers on were on the page and one router was
  destroyed the remaining routers would stop dispatching. [Ticket #2532317]

* The `req` object passed to routes now has a `pendingRoutes` property that
  indicates the number of matching routes after the current route in the
  dispatch chain. [Steven Olmsted]



Attribute Change History
========================

  * Optimized valueFn handling, so that valueFn is not called for Attribute,
    if user provides a value.

  * Support opts argument for setAttrs() also. Passed through to set, and ends up
    mixed into the event payload for all the attributes set through setAttrs()


Base Change History
===================

  * "value" defined in a subclass ATTRS definition, will now override 
    "valueFn" for the same attribute from the superclass chain. 
    
    Previously, "value" would only override "value" and "valueFn" 
    would only overide "valueFn", and in the aggregated set of 
    attributes, "valueFn" would take precedence over "value". 
    
    This meant that subclasses had to define a "valueFn" to overide 
    superclasses, if the superclass used "valueFn".

Calendar Change History
=======================

  * Bug fixes for 2532262, 2532277, 2531828.
  * Near 100% unit test coverage

Charts Change History
=====================

  * #2531796 Addressed issue in which a combo series with discontinuous data and discontinuousType set to dashed broke the chart.
  * #2532102 Addressed issue in which Area Charts with null values at the start or beginning do not close accurately.
  * #2532186 Addressed issue in which categoryDisplayName and valueDisplayName in seriesCollection were not accepted on init.
  * #2532234 Addressed issue in which axis appendTitleFunction and appendLabelFunction attributes were not being set properly.
  * #2532284 Addressed issue in which legend item text with spaces wrapped.
  * #2532285 Cleaned up legend destructor method.
  * #2532327 Addressed issue in which negative values in a column series displayed incorrectly.
  * #2532348 Addressed issue in which AreaSpline style object returned null.
  * #2532353 Addressed issue in which vertical attribute was not being set properly on non-histogram cartesian series.
  * #2532292 Filled out testing coverage
  * #2531688 Fixed rounding bug in pie chart. 


Collection Change History
=========================

* [!] The `sort` parameter of `Array.unique()` has been removed. This parameter
  was deprecated in YUI 3.3.0.

* `Array.unique()` now accepts an optional test function as its second
  parameter. This function can perform custom comparison logic to determine
  whether two values should be considered equal. [Ticket #2527901]

* The `every()`, `filter()`, `map()`, and `reduce()` functions now work
  correctly on array-like objects in ES5 browsers. [Ticket #2531652]

DataTable Change History
========================

 * Extracted all rendering logic into new class Y.DataTable.TableView.  Added
   `view` and `viewConfig` attributes to configure which view to use to render
   the table.  `headerView`, `bodyView`, and `footerView` are all passed along
   to this View class to delegate rendering (if appropriate).  You can now have
   a single `view` config on DT to render the entire table and contents.
   NOTE: if you were subscribing to `renderHeader`, `renderBody`, or
   `renderFooter` events, they now have to be prefixed with 'table' (E.g.
   `table.after('table:renderBody', fn);`
 * Column configuration array is now copied when assigned.  This allows the same
   array and column config objects to be used for multiple tables.

Custom Event Infrastructure Change History
==========================================

 * Fixed memory consumption issue where Y.Do's internal touched object cache, 
   Y.Do.objs, would never release object references.

   The Y.Do.objs property has been deprecated as of 3.6.0, and will be null.

   The cached state previously stored in Y.Do.objs has been moved onto the
   AOP'd object itself, in the *private* `_yuiaop` property.

   The only reason `_yuiaop` is mentioned here, is to provide a temporary 
   migration path for users who may have been using Y.Do.objs. If you are using 
   this property, please file a ticket with the use case, and we'll look at 
   addressing the use case formally, while not impacting GC.

File Module Change History
==========================

  * Added the ability to set custom headers and 
    `withCredentials` property on the XHR instance.


Graphics Change History
=======================

  * #2532293 Filled out testing coverage. 
  * #2532307 Added xRadius and yRadius attributes for ellipses. 
  * #2532362 Removed hard-coded "yui3-" from class names.
  * #2532306 Addressed issue in which too large a bounding box was being created for quadratic and cubic bezier curves. 
  * #2532305 Addressed issue in which linejoin bevel was not being set.
  * #2532243 Addressed issues caused by setting visible to false on a graphic instance. 
  * #2532222 Addressed issue in which a rotated shape did not drag correctly.  
  * #2531989 Address issues with invalid gradient values for x1,x2,y1,y2.
  * #2532242 Fixed issue with VMLGraphic.removeShape in which shapes were not removed when an id is passed instead of an instance.
  * #2532255 Fixed bug with shape attribute translateX and translateY.
  * #2532252 Fix issue in which passing null to stroke/fill attributes in CanvasShape threw errors.
  * #2532253 Implement clear method in canvas graphic. 
  * #2532272 Fixed issues with VMLGraphic.getXY() in which the wrong values were returned after x and y attributes are updated.
  * #2532243 Fixed issue in which setting the visible attribute of a graphic to false upon instantiation caused errors.
  * #2532114 Add ability to draw subpixel paths in ie. 

Handlebars Change History
=========================

  * Merged in commit wycats/handlebars.js@0afc8b58d


IO Utility Change History
=========================

  * Fixed issue when running in Node.js where `config.data` wasn't automatically
    stringified. [Ticket #2532390]


Matrix Change History
=====================

  * #2532255 Added translateX and translateY methods.

Pjax Change History
===================

* Fixed issue where pjax would try to navigate from clicks on elements which
  were not anchors or the anchor's `href` was a URL from a different origin than
  the current page. [Ticket #2531943]

Plugin Host Change History
==========================

  * Allow for non-base/non-attribute based plugins, by not assuming setAttrs or destroy exist
    on the plugin.


Slider Change History
=====================

  * `new Y.Slider({ disabled: true })` now locks thumb [#2532100]

SWF Utility Change History
==========================

  * Changed how the `<object>` tag is written to the DOM
    to fix an issue in IE (bug 2529891).


Uploader Utility (New) Change History
=====================================

  * Bug fix for 2532150 (empty fileList after fileselect event)
  * Bug fix for 2532140 (can't select the same set of files twice)
  * Bug fix for 2532111 (drop event is not being fired)
  * New feature: a `fileFilterFunction` attribute and improved
    `fileList` handling for filtering selected files.
  * New feature: Added support for file type filters to the HTML5 
    uploader's "Select Files" dialog.
  * New feature: allow setting custom headers and `withCredentials`
    property for the HTML5 uploader (passed through to the underlying
    XMLHttpRequest Level 2 instance).

Widget Modality Change History
==============================

  * Removed hard-coded "yui3-" CSS classname where the mask node was being
    retrieved via the ".yui3-widget-mask" CSS selector. [Ticket #2532363]

Widget Change History
=====================

 * Widget no longer runs html parser against the default `contentBox` created
   from `CONTENT_TEMPLATE`, so that html parser implementations don't need to
   check for `null` results for missing nodes.


YUI Core Change History
=======================

* Changed the default `throwFail` behavior to act like it sounds, see ticket #2531679
    If `throwFail` is `true` (default) we will not wrap modules or the use callback in
    a try catch. If it's `false`, they will be wrapped (the old behavior).