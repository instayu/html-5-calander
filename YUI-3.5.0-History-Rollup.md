YUI 3.5.0 History Rollup
===========================

The changes included in the PR1, PR2 and PR3 releases of YUI 3.5.0 are listed below, per component.

App Framework Change History
============================

### App

* Initial release.

### Model

* [!] The `validate()` method is now asynchronous, and is expected to call a
  callback function on success or failure. Old-style synchronous `validate()`
  methods will still work, but are deprecated. [Ticket #2531218]

* Model now supports ad-hoc attributes, which means it's no longer necessary to
  subclass `Y.Model` and declare attributes ahead of time. The following is now
  perfectly valid, and will result in a model instance with "foo" and "bar"
  attributes:

          var model = new Y.Model({foo: 'foo', bar: 'bar'});

* `load()` now fires a `load` event after the operation completes successfully,
  or an `error` event on failure. The `load()` callback (if provided) will still
  be called in both cases. [Ticket #2531207]

* `save()` now fires a `save` event after the operation completes successfully,
  or an `error` event on failure. The `save()` callback (if provided) will still
  be called in both cases. [Ticket #2531207]

* Options passed to `set()` and `setAttrs()` are now correctly merged into the
  event facade of the `change` event. [Ticket #2531492]

* Model's `destroy` event is now fully preventable (previously it was possible
  for the model to be deleted even if the `destroy` event was prevented by a
  subscriber in the `on` phase).

### ModelList

* ModelList's `model` property is now set to `Y.Model` by default. Since
  `Y.Model` now supports ad-hoc attributes, this makes it much easier to create
  and populate a ModelList without doing any subclassing:

          var list = new Y.ModelList();

          list.add([
              {foo: 'bar'},
              {baz: 'quux'}
          ]);

* Added a `filter()` method that returns a filtered array of models or,
  optionally, a new ModelList containing the filtered models. [Ticket #2531250]

* Added a `create` event that fires when a model is created/updated via the
  `create()` method, but before that model has actually been saved and added to
  the list (and before the `add` method has fired). [Ticket #2531400]

* Added a `load` event that fires when models are loaded. [Ticket #2531399]

* Models' `id` attributes (if set) are now used to enforce uniqueness. If you
  attempt to add a model to the list that has the same id as another model in
  the list, an `error` event will be fired and the model will not be added.
  [Ticket #2531409]

* The `add()`, `remove()` and `reset()` methods now accept other ModelList
  instances in addition to models and arrays of models. For example, passing a
  ModelList to `add()` will add all the models in that list to this list as
  well. [Ticket #2531408]

* ModelList now allows you to add models to the list even if they were
  instantiated in another window or another YUI sandbox. [Ticket #2531543]

* ModelList subclasses can now override the protected `_compare()` method to
  customize the low-level comparison logic used for sorting. This makes it easy
  to do things like descending sort, multi-field sorting, etc. See the API docs
  for details.

### Router (formerly Controller)

* [!] The `Controller` class and `controller` module have been renamed to
  `Router` and `router` respectively. The old names are deprecated, but have
  been retained as aliases for backwards compatibility. They will be removed
  in a future version of YUI.

* [!] The `html5`, `root`, and `routes` properties are now attributes, and
  `routes` may be set both during and after init. Code that refers to the old
  properties, like `myController.root` and `myController.root = '/foo'`, must be
  updated to use the attribute syntax instead: `myRouter.get('root')` and
  `myRouter.set('root', '/foo')`.

* [!] The signature for route handlers has changed. Route handlers now receive
  three arguments: `req`, `res`, and `next`. To preserve backcompat, `res` is a
  function that, when executed, calls `next()`. This behavior is deprecated and
  will be removed in a future version of YUI, so please update your route
  handlers to expect `next` as the third param.

* `"*"` can now be used to create a wildcard route that will match any path
  (previously it was necessary to use a regex to do this). Additionally, paths
  which contain a `"*"` (e.g., `"/users/*"`) act as a wildcard matching
  everything after it.

* The `hasRoute()` method now accepts full URLs as well as paths.

* The hashes used when `html5` is `false` are now root-less; the router's `root`
  is removed from the hash before it is set on the URL.

* When multiple Router instances exist on a page, calling `save()` in one will
  now cause matching routes to be dispatched in all routers, rather than only
  the router that was the source of the change.

* Added `url` and `src` properties to the request object that's passed to route
  handlers.

* Made the `html5` config attribute writable. This allows you to force a router
  to use (`true`) or not use (`false`) HTML5 history. Please don't set it to
  `false` unless you understand the consequences.

* Added a workaround for a nasty iOS 5 bug that destroys stored references to
  `window.location` when the page is restored from the page cache. We already
  had a workaround in place since this issue is present in desktop Safari as
  well, but the old workaround no longer does the trick in iOS 5.
  [Ticket #2531608]

### View

* [!] The `container`, `model`, and `modelList` properties are now attributes.
  Code that refers to the old properties, like `myView.model` and
  `myView.model = model`, must be updated to use the attribute syntax instead:
  `myView.get('model')` and `myView.set('model', model)`.

* [!] The `container` attribute now treats string values as CSS selectors.
  Previously, it assumed string values represented raw HTML. To get the same
  functionality as the old behavior, pass your HTML string through
  `Y.Node.create()` before passing it to `container`.

* [!] Destroying a view no longer also destroys the view's container node by
  default. To destroy a view's container node when destroying the view, pass
  `{remove: true}` to the view's `destroy()` method. [Ticket #2531689]

* View now supports ad-hoc attributes, which means it's no longer necessary to
  subclass `Y.View` and declare attributes ahead of time. The following is now
  perfectly valid, and will result in a view instance with "foo" and "bar"
  attributes:

          var view = new Y.View({foo: 'foo', bar: 'bar'});

* Added a `containerTemplate` property that contains an HTML template used to
  create a container node when one isn't specified. Defaults to "<div/>".

* When no `container` node is specified at instantiation time, the container
  won't be created until it's needed. `create()` is now only used to create a
  default container; it's never called when a custom container node is
  specified.

* Added a View extension, `Y.View.NodeMap`, that can be mixed into a `View`
  subclass to provide a static `getByNode()` method that returns the nearest
  View instance associated with a given Node (similar to `Widget.getByNode()`).


Attribute Change History
========================

  * Broke Y.Attribute up into:

    - Y.AttributeCore
    - Y.AttributeEvents
    - Y.AttributeExtras

    To support core Attribute usage, without Events, but still allow upgrade 
    path to add Events, if required.

    Y.AttributeCore is likely to form the basis for BaseCore and WidgetCore 
    (ala Node Plugins, where low-level state change events are not required). 

    Y.Attribute's public and protected API reimain unchanged, and loader will
    pull in the new dependencies.

    However if you're manually pulling in attribute-base, you'll need to 
    manually pull in attribute-core, attribute-events and attribute-extras 
    before it.

    **IMPORTANT** AttributeCore, AttributeEvents and AttributeExtras are 
    considered beta, and may be subject to change over the course 
    of the 3.5.0PRS. 

    Y.Attribute will remain unchanged however.

    Summary:

    Y.Attribute     - Common Attribute Functionality (100% backwards compat)
    Y.AttributeCore - Lightest Attribute support, without CustomEvents

    --

    Y.AttributeEvents - Augmentable Attribute Events support
    Y.AttributeExtras - Augmentable 20% usage for Attribute (modifyAttr, removeAttr, reset ...)
    Y.AttributeComplex - Augmentable support for constructor complex attribute parsing ({"x.y":foo})

    --

    Y.Attribute = Y.AttributeCore + Y.AttributeEvents + Y.AttributeExtras

    --

    Modules:

    "attribute-base" : Y.Attribute
    "attribute-core" : Y.AttributeCore

    "attribute-complex" : Y.AttributeComplex mixin (mixed into Y.Attribute)
    "attribute-events" : Y.AttributeEvents mixin
    "attribute-extras" : Y.AttributeExtras mixin

  * Changed State's internal data structure, to store pairs by 
    [name][property], instead of [property][name] to improve performance
    (most Attribute operations are name centric, not property centric).

    If you're working directly with Attribute's private _state.data, you
    may need to update your code to account for the change in structure. 

  * Attribute now passes the attribute name to valueFn, allowing users to
    write shared valueFn impls across attributes.


AutoComplete Change History
===========================

* Added an `enableCache` config attribute. Set this to `false` to prevent the
  built-in result sources from caching results (it's `true` by default).

* The `requestTemplate` value is now made available to YQL sources via the
  `{request}` placeholder, which works just like the `{query}` placeholder. Use
  this when you need to customize the query value (such as double-escaping it)
  used in the YQL query. [Ticket #2531285]

* Changing the value of the `value` attribute programmatically will now also
  update the value of the `query` attribute and will fire a `clear` event when
  the value is cleared (thus clearing results), but still will not fire a
  `query` event. Use the `sendRequest()` method to trigger a query
  programmatically.

* Added a workaround for an IE7 bug that would cause the result list to appear
  empty when it first becomes visible.

* Fixed a bug that caused a scrollable result list to be hidden when the user
  clicked and dragged on the scrollbar and then released the mouse button while
  the cursor was outside the list region.

* Fixed a bug that caused the list to disappear on mouseover if the input field
  received focus before the AutoComplete widget was initialized
  [Ticket #2531651]

* Fixed a bug that could prevent results from being selected via mouse click
  after a result was selected via the tab key. [Ticket #2531684]

* Fixed a bug that prevented the list from being re-aligned when the window was
  resized.



Base Change History
===================

  * Only invoke Base constructor logic once to 
    support multi-inheritance scenario in which
    an extension passed to Base.create inherits from Base
    itself.

    NOTE: To support multiple inhertiance more deeply, we'd 
    need to remove the hasOwnProperty restriction around object
    key iteration.

  * Added Y.BaseCore which is core Base functionality without
    Custom Events (it uses Y.AttributeCore instead of Y.Attribute).

    Y.BaseCore still maintains the ATTRS handling, init/destroy
    lifecycle and plugin support, but doesn't fire any custom evnets
    of it's own (the idea is that it will the base for Node-Plugin 
    type components, built off of a WidgetCore) 

    Y.Base is now Y.BaseCore + Y.Attribute, and is 100% backwards
    compatible.

    Summary:

    Y.Attribute     - Common Attribute Functionality (100% backwards compat)
    Y.Base          - Common Base Functionality (100% backwards compat)
   
    Y.AttributeCore - Lightest Attribute support, without CustomEvents
    Y.BaseCore      - Lightest Base support, without CustomEvents

    --

    Y.AttributeEvents - Augmentable Attribute Events support
    Y.AttributeExtras - Augmentable 20% usage for Attribute (modifyAttr, removeAttr, reset ...)
    Y.AttributeComplex - Augmentable support for constructor complex attribute parsing ({"x.y":foo})

    --
 
    Y.Attribute = Y.AttributeCore + Y.AttributeEvents + Y.AttributeExtras
    Y.Base      = Y.BaseCore + Y.Attribute

    -- 

    Modules:
    
    "base-base" : Y.Base
    "base-core" : Y.BaseCore

    "base-build" : Y.Base.build/create/mix mixin

  * Extended Base.create/mix support for _buildCfg, to Extensions, mainly so that
    extensions can define a whitelist of statics which need to be copied to the 
    main class.

    e.g.

    MyExtension._buildCfg = {
       aggregates:["newPropsToAggregate"...],
       custom: {
           newPropsToCustomMix
       },
       statics: ["newPropsToCopy"]
    };


Button Change History
====================

  * Initial Release


Calendar Change History
=======================

   * Calendar is now keyboard navigable [Ticket #2530348]
   * Calendar skins have been updated [Tickets #2530720, [#2531110, #2531744]
   * Calendar has received accessibility fixes
   * CalendarNavigator plugin has been updated and now supports disabled button states
   * Calendar got multiple new internationalization packages (de, fr, pt-BR, zh-HANT-TW)


Charts Change History
=====================

  * #2531748 Added aria keyboard navigation. 
  * #2530195 Tooltip display toggles on touchend event for mobile implementations. 
  * #2531410 Fixed issue in which specifying color arrays for marker borders of some series type broke in canvas implementation.
  * #2528814 Added charts-legend submodule to allow chart legends.
  * #2531456 Fixed issue in which loading a chart with an empty data provider throw an error and not load. 
  * #2530559 Added ability to explicitly set the width/height for vertical/horizontal axes
  * #2531003 Fixed issue in which axis labels flowed outside the chart's bounding box. Added allowContentOverflow attribute to allow for the overflow if desired.
  * #2531390 Addressed performance issues with IE
  * #2530151 Fixed issue in which charts will load large data sets loaded slowly. Added the notion of group markers to limit the number of dom nodes.
  * #2531468 Changed axis title attribute to use appendChild. NOTE: This may break backward compatibility if the value for your title attribute was dependent on innerHTML to format text.
  * #2531469 Changed axis label to use appendChild. NOTE: This may break backward compatibility with custom label functions if they were dependent on innerHTML to format text.
  * #2531472 Changed tooltip to use appendChild.  NOTE: This may break backward compatibility with custom tooltip functions if they were dependent on innerHTML to format text.
  * Removed memory leaks caused by orphaned dom elements.
  * Axes performance enhancements.
  * #2529859 Fixed issue in which Chart with timeAxis was not correctly initialized when setting dataProvider.
  * #2529922 Fixed issue in which updates to axes config after chart render did not take affect.  
  * #2530032 Fixed issue in which changing dataProvider after instantiation but pre-render resulted in the original dataProvider being used by the chart.
  * #2531245 Fixed issue in which the alwaysShowZero attribute was ignored by the NumericAxis.
  * #2531277 Fixed issue in which the area charts bled outside of content bounds when minimum was higher than zero.
  * #2531283 Fixed issue in which stacked historgrams did not accept an array for marker color values.
  * #2531314 Fixed issue in which a series failed to show if its value was missing from the first index of the dataProvider.  
  * #2529878 Added a percentage of whole value to the tooltip for PieChart.
  * #2529916 Added ability to distinguish between zero and null values in histograms. 
  * #2531515 Fixed issue in which PieChart was not handling numbers of type string.
  * #2531459 Fixed issue with histogram marker size irregularity on mouseover when specified width/height values are larger than the area available on the graph.



Collection Change History
=========================

* YUI now detects non-native ES5 shims added to native objects by other
  libraries and falls back to its own internal shims rather than relying on the
  potentially broken code from the other library.
* Deprecated arraylist-add and arraylist-filter in favor of individual
  subclass implementations or ModelList.



DataTable (deprecated) Change History
=====================================

Created to house the 3.4.1 implementations of datatable modules for people that
can't upgrade to 3.5.0 or greater for whatever reason.


DataTable Change History
========================

 * Major refactor.  See README for details about the new architecture.
 * Y.DataTable is now instantiable, in addition to Y.DataTable.Base
 * Recordset use has been replaced by ModelList. `recordset` attribute passes through to `data` attribute.  This is incomplete back compat because get('recordset') doesn't return a Recordset instance.
 * Columnset use has been removed. Column configuration is managed as an array of objects. `columnset` attribute passes through to `columns` attribute.  The same incomplete back compat applies.
 * DataTable doesn't render the table contents or header contents. That is left to `bodyView` and `headerView` classes.
 * Support for rendering a `<tfoot>` is baked in.
 * `datatable-datasource` modified to update a DataTable's `data` attribute rather than the (deprecated) `recordset`.
 * Scrollable tables now support captions
 * Added datatable-mutable module to provide addRow, removeRow, addColumn, etc
 * Added datatable-column-widths module to set column widths
 
 * Liner `<div>`s have been removed from the cell template in the default markup
 * `<colgroup>` is not rendered by default (added via `datatable-column-widths` extension)
 * message `<tbody>` is not added by default (compatibility module not added yet)
 * CSS uses `border-collapse: collapse` for all user agents instead of `separate` for most, but `collapse` for IE
 * CSS for base only includes styles appropriate to rendering the base markup
 * header gradient rendered as CSS gradient where possible, falling back to background image.
 * Added class "yui3-datatable-table" to the `<table>`
 * Added class "yui3-datatable-header" to all `<th>`s
 * Changed class "yui3-column-foo" to "yui3-datatable-col-foo" for `<th>`s and `<td>`s
 * Added class "yui3-datatable-cell" to all `<td>`s
 * CSS no longer references tags, only classes
 * ARIA grid, row, and gridcell roles added to the markup templates
 
 * `recordset` attribute deprecated in favor of `data` attribute
 * `columnset` attribute deprecated in favor of `columns` attribute
 * `tdValueTemplate`, `thValueTemplate`, and `trTemplate` attributes and `tdTemplate` and `thTemplate` properties dropped in favor of CELL_TEMPLATE and ROW_TEMPLATE properties on the `bodyView` and `headerView` instances.
 * Now fires `renderTable`, `renderHeader`, `renderBody`, and `renderFooter` events
 * Added `data`, `head`, `body`, and `foot` properties to contain instances of the ModelList and section Views.
 * Columns now MAY NOT have `key`s with dots in them.  It competes with Attribute's support for complex attributes. When parsing data with DataSchema.JSON, use the `locator` configuration to extract the value, but use a simple `key` to store/reference it from DT.


Drag and Drop Change History
============================

* 2530257 Avoid interference of Drag and Nodes Event Handles
* 2531377 shim is not created if dd-ddm is loaded after the first drag is activated
* 2531674 Issue with drag and drop and drop:hit event


Dial Change History
===================

  * Changed method name from _recalculateDialCenter to _calculateDialCenter
   
  * Changed property name from _centerXOnPage to _dialCenterX
    and from _centerYOnPage to _dialCenterY
    
  * Known issue: On IE7, when browser is zoomed, clicking on dial gives the
    wrong value.
    
  * Multiple instances of Dial all had the same ARIA label. 
    They are now unique. Screenreaders now read both the label and the value.
    [Ticket #2531505]   


DOM Change History
==================

  * Bug fix: Comments are now filtered from IE child queries. [Ticket 2530101]
  * Bug fix: Root node border correctly accounted for in IE. [Ticket 2531246]
  * Added Y.DOM.getScrollbarWidth() to return the width of a scrollbar in the current user agent



Rich Text Editor Change History
===============================

* 2530547 Frame: src attribute doesn't do anything
* General fixes for Y! Mail deployment
* 2531299 Pressing Backspace may cause editor to lose focus.
* 2531301 Editor using EditorPara and EditorLIsts has JS exceptions
* 2530547 Frame: src attribute doesn't do anything
* 2531329 Rename Y.Selection to Y.EditorSelection (or something)
* 2531577 Plugin.EditorBR works incorrectly in IE
* 2531615 Newline breaks <br> replaced with <wbr> in IE8 [bz 5242614]
* 2531329 - Breaking change: Bug #2531329 changed the old Y.Selection to Y.EditorSelection. 
  This has been aliased until 3.6.0, bug #2531659 created to track that change.


Escape Change History
=====================

* `regex()` no longer escapes the `#` character, since it has no special meaning
  in JS regexes.



Custom Event Infrastructure Change History
==========================================

  * Multiple calls to target.publish({ ... }) now work [Ticket #2531671]


Gestures Change History
=======================

  * Chrome fixed ontouchstart in window bug. No need to caveat
    the touch test for Chrome 6+.


ValueChange Change History
==========================

* Changed the name of the synthetic event to "valuechange" (all lowercase) for
  greater consistency with DOM event names. The older "valueChange" name will
  continue to be supported indefinitely, but for consistency I recommend
  switching to "valuechange".

* Added support for delegated valuechange events. You can now use `delegate()`
  to attach a valuechange event to a container node and be notified of changes
  to any descendant that matches the specified delegation filter.

* The valuechange event facade now includes `currentTarget` and `target`
  properties like a good little synthetic event.



Event Infrastructure Change History
===================================

  * `event-simulate` references to `window` replaced with `Y.config.win`
    [#2531223]
  * `event-resize` no longer throws an exception in IE [#2531310]
  * "avilable" and "contentready" handlers that throw exceptions no longer
    result in infinite polling [#2531375]
  * Added `event-touch`, `event-flick`, `event-move`, and `event-valuechange` to
    the `event` virtual rollup in accordance with the docs.
  * 'key' event does a better job parsing character filters. Uses `e.which`
    instead of `e.keyCode` or `e.charCode`.
  * `node.delegate('focus', fn, '.not-focusable')` now works.  Properly supports
    delegation where the filter matches non-focusable parent nodes of the
    focused target. Same for blur. [#2531334] (`event-focus`)
  * `node.delegate('focus', fn, filterThatMatchesNode); node.focus();` now
    works. [#2531734]


File Module Change History
==========================

  * Initial release


Get Utility Change History
==========================

* [!] The `Y.Get.abort()` method is now deprecated and will be removed in a
  future version of YUI. Use the transaction-level `abort()` method instead.

* [!] The `charset` option is now deprecated and will be removed in a future
  version of YUI. Specify an `attributes` object with a `charset` property
  instead.

* [!] The `win` option, which allowed you to specify the window into which
  nodes should be inserted, is now deprecated and will be removed in a future
  version of YUI. Use the `doc` option instead, which allows you to specify a
  document, as opposed to a window (which makes more sense).

* [!] The `win` property of transaction objects is now deprecated and will be
  removed in a future version of YUI. Since any given request in a transaction
  may now have its node inserted into any document, the best way to get this
  info is to find the request you're interested in inside the transaction's
  `requests` property, then look at that request's `doc` property to figure out
  what document it's associated with.

* [!] The `tId` property of transaction objects is now deprecated and will be
  removed in a future version of YUI. Use the `id` property instead.

* The Get Utility has been completely rewritten to improve performance and add
  much-needed functionality. Backwards compatibility has been maintained, but
  some methods and APIs have been deprecated and will be removed in a future
  version of YUI.

* Multiple scripts within a transaction are now loaded in parallel whenever
  possible in browsers that are capable of preserving execution order regardless
  of load order. This improves performance in those browsers when loading
  multiple scripts.

* Multiple CSS resources within a transaction are now always loaded
  asynchronously, since CSS rules are applied based on the order of link nodes
  in the document, not the order in which resources finish loading. This
  improves performance in all browsers when loading multiple CSS files.

* Script and CSS resources that fail to load due to HTTP or network errors are
  now correctly treated as failures in all browsers that support `error` events
  on script or link nodes. Most browsers support this on script nodes, but only
  Firefox 9+ currently supports this on link nodes.

* CSS load completion is now detected reliably in older versions of
  WebKit (<535.24) and Firefox (<9), which don't support the `load` event on
  link nodes. Unfortunately, while our workaround makes it possible to detect
  when loading is complete, we still can't detect whether it completed
  successfully or with an error, so in these browsers CSS resources are always
  assumed to have loaded successfully.

* Added a `Y.Get.load()` method, which allows you to load both CSS and JS
  resources in a single transaction.

* Added a `Y.Get.js()` method, which is now the preferred way to load JavaScript
  resources. `Y.Get.script()` is now an alias for `js()`.

* Added a new `Y.Get.options` property containing global options that should be
  used as the default for all requests, along with similar `cssOptions` and
  `jsOptions` properties containing default options that apply only to CSS or
  JS requests, respectively, and that take precedence over the global defaults.

* Added a new `pollInterval` option, which allows you to customize the polling
  interval (in milliseconds) used to check for CSS load completion in WebKit and
  Firefox <=8.

* The `css()`, `js()`, `load()`, and `script()` methods now return an instance
  of `Y.Get.Transaction`, which encompasses one or more requests and contains
  useful properties and methods for getting information about and manipulating
  those requests (and related HTML nodes) as a unit.

* The `css()`, `js()`, `load()`, and `script()` methods now accept an optional
  Node.js-style callback function as either the second or third parameter. This
  function will be called after the transaction finishes. The first argument
  is an array of errors, or `null` on success. The second argument is the
  transaction object.

* The `css()`, `js()`, `load()`, and `script()` methods now accept URL strings,
  objects of the form `{url: '...', [... options ...]}`, or arrays of URL
  strings and/or objects. This allows you to specify per-URL options if desired,
  such as node attributes, parent documents, `insertBefore` nodes, etc.

* The logic used to determine where a node should be inserted when no custom
  `insertBefore` node has been specified has changed slightly. By default,
  script and link nodes will now be inserted before the first `<base>` element
  if there is one, or failing that, before the last child of the `<head>`
  element, or if there's no `<head>` element, before the first `<script>`
  element on the page.

* The source for the `get` module has moved from `src/yui` to `src/get`. This
  allows it to be built separately from the core YUI modules.



Graphics Change History
=======================

  * #2531630 Changed BaseGraphic class to GraphicBase.
  * Removed memory leaks from Shape class. 
  * Added defaultGraphicEngine config to allow developer to specify canvas as the preferred graphic technology. 
  * #2531127 Fixed issue in which transforms were not consistent across different browsers.
  * #2531230 Fixed issue in which setting visible at instantiation would throw an error for a shape.
  * #2531359 Fixed issue in which setting attributes in IE would throw errors.
  * #2531460 Fixed issue in which the clear() method would throw errors in IE.
  * #2531465 Fixed typographic error in SVGGraphic class.
  * #2531049 Added matrix option to the shape's transform attribute.
  * #2531126 Added ability animate transform attribute.
  * #2531552 Change name of Graphics Path Utility to Graphics Path Tool.


Handlebars Change History
=========================

  * Initial release.


History Change History
======================

  * Added a workaround for a nasty iOS 5 bug that destroys stored references to
    `window.location` when the page is restored from the page cache. We already
    had a workaround in place since this issue is present in desktop Safari as
    well, but the old workaround no longer does the trick in iOS 5.
    [Ticket #2531608]

  * Bug fix: HTML5 history is no longer used by default in Android <2.4, even if
    feature detection shows it's available. It's just too broken.
    [Ticket #2531670]


IO Utility Change History
=========================

  * Fixed error in sending an XML document as POST data. [Ticket #2531257]

  * Configuration data can now include an instance of FormData for HTTP
    POST requests. [Ticket #2531274]


YUI Loader Change History
=========================

The biggest change made was the use of the `async` flag on `Y.Get` requests. Loader will now use the
`Y.Loader.resolve()` method under the hood to calculate all the dependencies that it is aware of, then
build the URL's to complete this request. It will then batch those into one `Y.Get` transation and fetch
all of them asynchronously, then return to loader for post processing of the injected dependencies.

   * 2529521 Consider making the presence of YUI CSS detectable by the loader
   * 2530135 Add support for loading YUI modules in parallel in all browsers, since execution order is unimportan...
   * 2530177 [Pull Request] - Bug #2530111  If the condition block is defined w/o a test fn or UA check, assume i...
   * 2530343 Loader.sorted does not contain conditional modules
   * 2530565 Slider one-off skins not being loaded
   * 2530958 Loader.resolve not properly handling CSS modules
   * 2531319 The aliased modules are reported as missing 
   * 2531324 Support regular expressions in the patterns configuration
   * 2531281 specify ID when injecting CSS via loader
   * 2529521 Consider making the presence of YUI CSS detectable by the loader
   * 2530077 'force' ignored for on-page modules unless 'allowRollup' is true
   * 2530135 Add support for loading YUI modules in parallel in all browsers, since execution order is unimportan...
   * 2530177 [Pull Request] - Bug #2530111  If the condition block is defined w/o a test fn or UA check, assume i...
   * 2530343 Loader.sorted does not contain conditional modules
   * 2530565 Slider one-off skins not being loaded
   * 2530958 Loader.resolve not properly handling CSS modules
   * 2531150 Update Dynamic Loader example
   * 2531319 The aliased modules are reported as missing 
   * 2531324 Support regular expressions in the patterns configuration
   * 2531433 Improve the syntax for setting a skin in the YUI.use() statement
   * 2531451 Loading of lang modules doesn't go through configFn in loader
   * 2531590 addModule does not update the global cache so dynamically added skins modules can get lost
   * 2531626 maxURLlength configuration on a per group basis
   * 2531637 Configurable 'comboSep' for groups
   * 2531646 "undefined" error
   * 2531697 Loading a CSS module without specifying 'type=css' will throw a syntax error
   * 2531587 Loader will not load custom modules if combine: true


Matrix Change History
=====================

  * Nobody can know what the Matrix is: you have to see it for yourself.



MenuNav Change History
======================

  * Added Night skin for MenuNav
  * Removed console logging message (#2531192)
   


Node Change History
===================

  * Bug fix: Children collection now accessible from documentFragments. [Ticket 2531356] 
  * Bug fix: The compareTo() method now works across sandboxes. [Ticket 2530381] 


Panel Change History
====================

  * Panel now hosts the a default "close" button which can be included more
    easily then before. This button has advanced styling which will render the
    button with the text [Close] when it's in the footer, and with the icon [x]
    when it's in the header. [Ticket #2531680]

        // Panel with close button in header.
        var panel = new Y.Panel({
            buttons: ['close']
        });

        // Panel with close button in footer.
        var otherPanel = new Y.Panel({
            buttons: {
                footer: ['close']
            }
        });

  * Panel's skins now uses `.yui3-panel` instead of `.yui3-panel-content` for
    its CSS selectors where possible. [Ticket #2531623]

  * Moved mask-related styles/skins to `WidgetModality`.

  * See also WidgetButtons' change history.

  * See also WidgetModality's change history.


Parallel Change History
=======================

  * Initial Release


Pjax Change History
===================

  * Initial release.


Plugin Host Change History
==========================

  * API corrected for hasPlugin. It returns the plugin if available, otherwise undefined.
    It has always done this, and since they're truthy/falsey, figured it was better than
    changing the behavior, in case folks are using the plugin instance returned by hasPlugin.


Resize Utility Change History
=============================

   * No changes.


ScrollView Change History
=========================

  * Allow scrollbar to work with non-px width scrollviews
  * Added mousewheel support (#2529136)


Slider Change History
=====================

  * Added ARIA roles and states [#2528788]
  * Added keyboard support. Arrows, pageUp/Down, home/end [#2528788]
  * Fixed a bug where set('value', x) could be ignored if the max - min was
    less than the configured length. [#2531498]
  * Added click on thumb or clickable rail gives the thumb focus, allowing 
    keyboard access. [#2531569] 


Test Console Change History
===========================

   * Initial release.


Text Change History
===================

   * Data files now use escape sequences rather than actual Unicode characters in
     order to work around a bug in Internet Explorer that causes script file
     encodings to be ignored.




Uploader Utility (DEPRECATED) Change History
============================================

  * 3.4.1 Uploader, deprecated as uploader-deprecated


Uploader Utility (New) Change History
=====================================

  * Added HTML5Uploader layer
  * Refactored queue management out of Uploader
  * Introduced new APIs (more details in documentation)
  * Added keyboard access to the Flash layer
  * Old uploader has been deprecated as 'uploader-deprecated' module.



Widget Buttons Change History
=============================

  * [!] WidgetButtons has been completely rewritten, back-compat for common
    usage has been maintained. The new version is _much more_ robust.
    [Tickets #2531366, #2531624, #2531043]

  * [!] The `buttons` attribute is handled in an _extremely_ flexible manner.
    It supports being a single Array, or an Object of Arrays keyed to a
    particular section.

    The `buttons` collection will be normalized into an Object which contains an
    Array of `Y.Node`s for every `WidgetStdMod` section (header, body, footer)
    which has one or more buttons. The structure will end up looking like this:

        {
            header: [...],
            footer: [...]
        }

    A button can be specified as a Y.Node, config Object, or String name for a
    predefined button on the `BUTTONS` prototype property. When a config Object
    is provided, it will be merged with any defaults provided by a button with
    the same `name` defined on the `BUTTONS` property. [Ticket #2531365]

  * [!] All button nodes have the `Y.Plugin.Button` plugin applied.

  * [!] The HTML structure for buttons has been optimized to:

        <span class="yui3-widget-butons>
            <button class="yui3-button">Foo</button>
        </span>

    The above structure will appear in each `WidgetStdMod` section
    (header/body/footer) which contains buttons. [Ticket #2531367]

  * Fixed issue with multiplying subscriptions to `buttonsChange` event. The
    event handler was itself subscripting _again_ to the event causing an
    ever-increasing number of subscriptions all doing the same work. Now
    WidgetButtons will always clean up its event subscriptions.
    [Ticket #2531449]

  * Added support for predefining `BUTTONS` on the prototype. `BUTTONS` is
    Collection of predefined buttons mapped by name -> config. These button
    configurations will serve as defaults for any button added to a widget's
    buttons which have the same `name`. [Ticket #2531680]

  * Added an `HTML_PARSER` implementation for the `buttons` attribute. This
    allows the initial value for a widget's `buttons` to be seeded from its DOM.

  * A widget's `buttons` now persist after header/body/footer content updates.
    Option 2 of the follow scenario has been implemented:
    http://jsfiddle.net/ericf/EXR52/

  * A button can be configured with a `context` object (which defaults to the
    widget instance), which will be used as the `this` object when calling a
    button's `action` or `events` handlers. [Ticket #2531166]

  * Buttons now support multiple `events` which can be specified in place of an
    `action`. The follow are equivalent:

        var buttonConfigWithEvents = {
            label: 'Foo',
            events: {
                click: function (e) {
                    this.hide();
                }
            }
        };

        var buttonConfigWithAction = {
            label : 'Foo',
            action: 'hide'
        };

    A button's `action` can now be specified as the String name of a function
    which is hosted on the `context` object. [Ticket #2531363]

  * Added the notion of a default button. A widget's `defaultButton` will have
    the "yui3-button-primary" CSS class added to it, and will be focused when
    the widget is shown.

  * Updated the `addButton()` method and added other accessor/mutator methods:
    `getButton()` and `removeButton()`.

  * Buttons can now be added to a widget's body, not just the header and footer.



Widget Modality Change History
==============================

  * Initialization logic will now always run, even when a widget is constructed
    with `{modal: false}`; previously the initialization logic did not run in
    this case. [Ticket #2531401]

  * Fixed destruction lifecycle bug. The mask is now removed when no modal
    widgets are visible on the page. This also fixed an issue with multiple
    modal widget and their `visible` attribute.
    [Ticket #2531484, #2531821, #2531812]

  * Moved mask-related styles/skins out of Panel and into WidgetModality.



Widget Std Mod Change History
=============================

  * Added `forceCreate` option to `getStdModNode()` method which, if true, will
    create the section node if it does not already exist. [Ticket #2531214]


Widget Change History
=====================

 * Refactored some of the box stamping code, to avoid Node references
   until render. Changed caching mechanism for Y.Widget.getByNode to use node.get("id")

 * Patched after listeners in Widget with a if (e.target === this), so that homogenous 
   bubbles don't end up changing state at both the source and the target. Broader
   fix needs to go into Event/EventTarget

 * Optimized focus handler registration, by only registering a single document focus
   listener and using Widget.getByNode to ship out handling to the specific widget
   instance.

 * Widget will now default to an empty object config, if one isn't passed in, 
   so that HTML_PARSER can work with a static ATTRS srcNode definition.

   It's not possible to address this just at the HTML_PARSER level, since the config 
   object gets used by reference, so we need to make sure everything is updating the
   config object which is passed to Base's initialization chain.


YUI Core Change History
=======================

* YUI now runs natively on Node.js without a shim. See README.nodejs.md for
  details.

* YUI now detects non-native ES5 shims added to native objects by other
  libraries and falls back to its own internal shims rather than relying on the
  potentially broken code from the other library.

* Added static YUI.applyConfig to apply config settings to YUI.GlobalConfig in
  parts instead of in whole. [Ticket #2530970]

* Added `Y.getLocation()` which returns the `location` object from the
  window/frame in which a YUI instance operates. [Ticket #2531608]

* Added a `useNativeES5` YUI config option, which is `true` by default. If
  `false`, certain YUI features that check for native ES5 functionality will
  always fall back to non-native implementations even in ES5 browsers (useful
  for testing).

* `Y.Array.indexOf()` now supports a `fromIndex` argument for full ES5
  compatibility. [Based on a patch from Ryuichi Okumurua]

* `Y.Object.isEmpty()` now casts the given value to an object if it isn't one
  already, which prevents exceptions when it's given a non-object.

* Fixed issue #2531247: Namespace function behaves wrong with multiple
  arguments.

* Fixed issue #2531512: 'debug' parameter missing from the YUI Config object
  documentation.

* 2530970 Should we provide a YUI.applyConfig(), to avoid clobbering of YUI_config in 'mashup' use cases
* 2531164 Natively use YUI Gallery Modules form does not submit on [enter]
* 2531247 namespace function behaves wrong with multiple arguments
* 2531512 'debug' parameter missing from the YUI Config object documentation; the Config object documentation ...
* 2531550 Prepare npm package for 3.5.0
* 2531551 Add support for Silk in Y.UA
* 2531612 Wrong module name in YUI Global Object documentation