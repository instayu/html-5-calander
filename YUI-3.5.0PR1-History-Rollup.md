YUI 3.5.0PR1 History Rollup
===========================


Anim Change History
===================

* No change.


App Framework Change History
============================

### App

* Initial release.

### Model

* [!] The `validate()` method is now asynchronous, and is expected to call a
  callback function on success or failure. Old-style synchronous `validate()`
  methods will still work, but are deprecated. [Ticket #2531218]

* `load()` now fires a `load` event after the operation completes successfully,
  or an `error` event on failure. The `load()` callback (if provided) will still
  be called in both cases. [Ticket #2531207]

* `save()` now fires a `save` event after the operation completes successfully,
  or an `error` event on failure. The `save()` callback (if provided) will still
  be called in both cases. [Ticket #2531207]

### ModelList

* Added a `filter()` method that returns a filtered array of models. [Ticket
  #2531250]

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

* "*" can now be used to create a wildcard route that will match any path
  (previously it was necessary to use a regex to do this). Additionally, paths
  which contain a "*" (e.g., "/users/*") act as a wildcard matching everything
  after it.

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

### View

* [!] The `container`, `model`, and `modelList` properties are now attributes.
  Code that refers to the old properties, like `myView.model` and
  `myView.model = model`, must be updated to use the attribute syntax instead:
  `myView.get('model')` and `myView.set('model', model)`.

* [!] The `container` attribute now treats string values as CSS selectors.
  Previously, it assumed string values represented raw HTML. To get the same
  functionality as the old behavior, pass your HTML string through
  `Y.Node.create()` before passing it to `container`.



ArraySort Change History
========================


* No changes.


AsyncQueue Change History
=========================


* No changes.


Attribute Change History
========================


* No changes.


AutoComplete Change History
===========================


* The `requestTemplate` value is now made available to YQL sources via the
  `{request}` placeholder, which works just like the `{query}` placeholder. Use
  this when you need to customize the query value (such as double-escaping it)
  used in the YQL query. [Ticket #2531285]



Base Change History
===================


* Only invoke Base constructor logic once to 
    support multi-inheritance scenario in which
    an extension passed to Base.create inherits from Base
    itself.

    NOTE: To support multiple inhertiance more deeply, we'd 
    need to remove the hasOwnProperty restriction around object
    key iteration.


Cache Change History
====================


* No changes.


Calendar Change History
=======================


* No changes.


Charts Change History
=====================


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



ClassName Manager Change History
================================


* No changes.


Collection Change History
=========================


* No changes.


ConsoleFilters Plugin Change History
====================================


* No changes.


Console Change History
======================


* No changes.


Cookie Change History
=====================


* No changes.


CSS Base Change History
=======================


* No code changes.



CSS Fonts Change History
========================

* No change.



CSS Grids Change History
========================


* No change.



CSS Reset Change History
========================

* No change.



DataSchema Change History
=========================


* No changes.


DataSource Change History
=========================


* No changes.


DataTable Change History
========================


* No changes.


DataType Change History
=======================


* No changes.


Drag and Drop Change History
============================


* No changes.


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



Dump Change History
===================


* No changes.


Rich Text Editor Change History
===============================


* 2530547 Frame: src attribute doesn't do anything
* General fixes for Y! Mail deployment

###
Escape Change History
=====================


 * `regex()` no longer escapes the `#` character, since it has no special meaning
       in JS regexes.



Custom Event Infrastructure Change History
==========================================


* No changes.


Gestures Change History
=======================


* No changes.


ValueChange Change History
==========================


* No changes.


Event Infrastructure Change History
===================================


* No changes.


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

* CSS load completion is now detected reliably in WebKit browsers and in older
  versions of Firefox, which don't support the `load` event on link nodes.
  Unfortunately, while our workaround makes it possible to detect when loading
  is complete, we still can't detect whether it completed successfully or
  with an error, so in these browsers CSS resources are always assumed to have
  loaded successfully.

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
  if there is one, or failing that, before the first child of the `<head>`
  element, or if there's no `<head>` element, before the first `<script>`
  element on the page.

* The source for the `get` module has moved from `src/yui` to `src/get`. This
  allows it to be built separately from the core YUI modules.



Graphics Change History
=======================


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


Highlight Change History
========================


* No changes.


History Change History
======================


* No changes.


ImageLoader Change History
==========================


* No changes.


Intl Change History
===================


* No changes.


IO Utility Change History
=========================


* Fixed error in sending an XML document as POST data. [Ticket #2531257]

* Configuration data can now include an instance of FormData for HTTP
    POST requests. [Ticket #2531274]


JSON Utility Change History
===========================


* No changes.


JSONP Change History
====================


* No changes.


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


Flick Node Plugin Change History
================================


* No changes.


Focus Manager Change History
============================


* No changes.


MenuNav Change History
======================


* Added Night skin for MenuNav
   


Node Change History
===================


* Bug fix: Children collection now accessible from documentFragments. [Ticket 2531356] 
* Bug fix: The compareTo() method now works across sandboxes. [Ticket 2530381] 



OOP Change History
==================


* No changes.


Overlay Change History
======================


* No changes.


Panel Change History
====================


* No changes.


Parallel Change History
=======================


* Initial Release


Pjax Change History
===================


* Initial release.


Plugin Change History
=====================


* No changes.


Plugin Host Change History
==========================


* No changes.


QueryString Utility Change History
==================================


* No changes.


Queue Promote Change History
============================


* No changes.


Recordset Change History
========================


* No changes.


Resize Utility Change History
=============================


* No changes.


ScrollView Change History
=========================


* Allow scrollbar to work with non-px width scrollviews


Simple YUI Change History
=========================


* No changes.


Slider Change History
=====================


* No changes.


Sortable Utility Change History
===============================


* No changes.


StyleSheet Change History
=========================


* No changes.


Substitute Utility Change History
=================================


* No changes.


SWF Utility Change History
==========================


* No changes.


SWFDetect Utility Change History
================================


* No changes.


TabView Change History
======================


* No change.


Test Console Change History
===========================


* Initial release.


Text Change History
===================


* No changes.


Transition Change History
=========================

* No change.


Uploader Utility Change History
===============================


* No changes.


Widget Anim Change History
==========================


* No changes.


Widget Autohide Change History
==============================


* No changes.


Widget Buttons Change History
=============================


* Configurations of named button types, e.g. "close", are now merged with the
    user-provided configuration allowing overriding of the default options for
    the named button.


Widget Child Change History
===========================


* No changes.


Widget Modality Change History
==============================


* Initialization logic will now always run, even when a widget is constructed
    with `{modal: false}`; previously the initialization logic did not run in
    this case. [Ticket #25]


Widget Parent Change History
============================


* No changes.


Widget Position Align Change History
====================================


* No changes.


Widget Position Constrain Change History
========================================


* No changes.


Widget Position Change History
==============================


* No changes.


Widget Stack Change History
===========================


* No changes.


Widget Std Mod Change History
=============================


* No changes.


Widget Change History
=====================


 * Refactored some of the box stamping code, to avoid Node references
   until render. Changed caching mechanism for Y.Widget.getByNode to use node.get("id")

 * Patched after listeners in Widget with a if (e.target === this), so that homogenous 
   bubbles don't end up changing state at both the source and the target. Broader
   fix needs to go into Event/EventTarget


YQL Change History
==================


* No changes.


YUI Throttle Change History
===========================


* No changes.


YUI Core Change History
=======================


 * `Y.Object.isEmpty()` now casts the given value to an object if it isn't one
  already, which prevents exceptions when it's given a non-object.
 * 2530970 Should we provide a YUI.applyConfig(), to avoid clobbering of YUI_config in 'mashup' use cases
 * 2531247 namespace function behaves wrong with multiple arguments
 * 2531512 'debug' parameter missing from the YUI Config object documentation; the Config object documentation ...
 * YUI is now native on Node.js, no shim needed to run. See README.nodejs.md