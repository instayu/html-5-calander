The changes included in the YUI 3.7.0pr1 are listed below, per component. Components not listed were not changed in 3.7.0pr1 or 3.7.0pr2.

App Framework Change History
----------------------------

### App

* Added App.Content, an App extension that provides pjax-style content fetching
  and handling, making it seamless to use a mixture of server and client
  rendered views.

### Model

* Added custom response parsing to ModelSync.REST to make it easy for developers
  to gain access to the full `Y.io()` response object. Developers using
  ModelSync.REST can either assign the `parseIOResponse` property to `false` to
  gain access to the full `Y.io()` response object in their `parse()` method,
  or provide a custom implementation of the `parseIOResponse()` method.

* ModelSync.REST's `serialize()` method now receives the `action` which the
  `sync()` method was invoked with. [Ticket #2532625]

### ModelList

* You may now add models to a ModelList at instantiation time by providing an
  Object, array of Objects, Model instance, array of Model instances, or another
  ModelList instance in the `items` property of the config object passed to
  ModelList's constructor. This change also applies to LazyModelList.

### Router

* Added support for route-based middleware to Router. The `route()` method now
  accepts an arbitrary number of callbacks enabling more reuse of routing code.
  For people familiar with Express.js' route middleware, this behaves the same.
  [Ticket #2532620]

### View

* Log a warning when a handler function is not present when a view's `events`
  are being attached. [Ticket #2532326] [Jay Shirley, Jeff Pihach]


Attribute Change History
------------------------

  * Removed unused call to `get` in `getAttrs()`, improving `getAttrs()` 
    performance. [Ryan Grove]


Charts Change History
---------------------

  * #2532713 Addressed issue in which updating the dataProvider on a chart with a legend threw an error.


Collection Change History
-------------------------

* Added `Y.Array.flatten()`. This method flattens arrays of arrays into a single
  flat array.


DataType Change History
-----------------------

* DataType is now an alias for Y.Date, Y.Number and Y.XML modules. The Y.DataType.* module
  names have been retained for backwards compatibility but may be removed in the future 
  (a decision which will be forecast sufficiently ahead of time).


Date Change History
-------------------

* Y.DataType.Date has been moved to Y.Date


Custom Event Infrastructure Change History
------------------------------------------

 * CustomEvent run-time performance optimizations.

   a. The `subscribers` and `afters` CustomEvent instance properties have 
      been deprecated, and replaced with private arrays (instead of hashes).

      If you're referring to the `subscribers` or `afters` properties directly,
      you can set the `Y.CustomEvent.keepDeprecatedSubs` to true, to restore
      them, but you will incur a performance hit in doing so.

      The rest of the CustomEvent API is driven by the new private arrays, and
      does not require the `subscribers` and `afters` properties, so you should
      only enable `keepDeprecatedSubs` if your code is referring to the properties
      directly.

      If you are using the above properties directly, please file an enhancement
      request and we'll provide a public way to achieve the same results, without
      the performance hit before we remove the properties permanently.

   b. Avoid new EventTarget when stoppedFn is not used.

   c. Optimized mixing during the creation of a custom event object.
   
   d. Optimized mixing done on the facade, during a fire with payload.
   
   Performance results on Chrome 19/MacOS below, for the use case where we're
   iring with a payload:

   #### Custom Event Lifecycle Numbers (Fix a, b, c)

   BEFORE (3.6.0):
   EventTarget with attribute style publish, fire, with on/after listeners x 7,623 ops/sec
    
   CURRENT (With fixes a, b, c):
   EventTarget with attribute style publish, fire, with on/after listeners x 23,642 ops/sec

   #### Payload Numbers (Fix d)

   BEFORE (3.6.0):
   Fire With Payload - 10 listeners x 27,918 ops/sec ±1.32% (54 runs sampled)
    
   CURRENT (With fix d):
   Fire With Payload - 10 listeners x 63,362 ops/sec ±0.37% (58 runs sampled)   

   The benchmark tests can be found in src/event-custom/tests/benchmark

   Log messages for the follow commits have more details:

   e7415e71decf3d921161e8883270e16b433aa150 - subscribers/afters fix.
   29f63996f8b69a7bb6d2e27f4d350c320998c0b2 - optimized payload mix fix.

 * CustomEvent memory optimizations.
   
   * Fixed `_facade` and `firedWith` which were holding onto a reference
     to the last fired event facade. Now `_facade` is reset to null after 
     the fire sequence, and `firedWith` is only maintained for `fireOnce` 
     CustomEvents. i

     This allows the facade from the last fired event to be GC'd whereas 
     prior to this change it wasn't.


Gestures Change History
-----------------------

* 'event-gestures' supports MSPointer events (IE10 on Windows 8).


Event Infrastructure Change History
-----------------------------------

* Changed event-synthetic, to support CustomEvent performance optimizations.

  Mainly the deprecation of CustomEvent subscribers and afters instance properties,
  which event-synthetic was referring to directly. The direct reference was replaced
  by a public API method call.

  See src/event-custom/HISTORY.md for more details about the deprecated properties.

* `event-tap` was migrated from Gallery and it supports "fast-click" on touch
  devices.

* Added try/catch around the internal window unload listener event-base adds,
  so that YUI works in Chrome Packaged Apps. They don't support unload,
  but still have a window.onunload, so no real way to feature test without
  a try/catch anyway.


GestureSimulation Change History
--------------------------------

* Initial release.


Graphics Change History
-----------------------

  * Ticket #2532682 Addressed issue in which drawing and filling the same shape independently resulted in bad VML rendering.

  * Ticket #2531432 Added data attribute to allow for passing svg path strings to a shape.

  * Ticket #2532495 Added generic (non-implementation specific) class names to shapes.

  * Ticket #2532611 Added toFront and toBack methods to shapes.

  * Ticket #2532612 Added ability to animate a shapes stroke and fill attributes when incuding the anim-shape submodule. All shape attributes are animatable. 

  * Ticket #2532635 Added ability size the contents of a Graphic instance to fit into its parent container. 


IO Utility Change History
-------------------------

* Prevent IO from maintaining cookies across requests in Node.js.
  [Ticket #2532676]

* Remove "X-Requested-With" header from cross-domain XHRs. Setting any
  non-standard HTTP headers when performing a cross-domain request using CORS
  results in a _required_ pre-flight OPTIONS request. Not adding this header by
  default allows the browser to communicate with a server which is not
  CORS-ready. [Ticket #2532673] [Clarence Leung]


Matrix Change History
---------------------

  * #2532709 Firefox 16 no longer supports units for tx/ty of a transform matrix. Updated toCSSText() method to no longer add them for Firefox browsers. 


ScrollInfo Node Plugin Change History
-------------------------------------

* Initial release.


Number Change History
---------------------

* Moved from Y.Datatype.Number to Y.Number


Pjax Change History
-------------------

* Added `Y.Pjax.defaultRoute`, a static stack of middleware which forms the
  default Pjax route. This is useful when overriding Pjax's default `"*"` route
  by adding adding more specific route paths, or performing some operation after
  the default behavior.

* Added the `loadContent()` method which is route middleware which loads content
  from a server. This can be used with custom Pjax implementations which need to
  have more control over how content is updated in the DOM.

* Extracted `Y.PjaxContent` from `Y.Pjax`. Pulling out the content-handling
  functionality allows it to be used by other components, like `Y.App`.
  [Ticket #2532487]


ScrollView Change History
-------------------------

Detailed overview of all changes (including protected/private) @ https://gist.github.com/3522590

  * Added Forced-Axis and Dual-Axis Support. ScrollView now has an (optional) `axis` 
    property that can be declared with values: `x`, `y`, or `xy`. (#2532631)

  * Added: Initial support for RTL (Right-To-Left) layouts (#2531874).

  * Added: Unit test coverage for scrollview-base and scrollview-paginator (#2532288, #2532287)

  * Moved: Paginator’s scrollTo() method has been deprecated and replaced with scrollToIndex. (##2530145)

  * Moved the following ScrollView static properties (now deprecated) to instance attributes for more control
    SNAP_DURATION to 'snapDuration'
    SNAP_EASING to 'snapEasing'
    EASING to 'easing'
    FRAME_STEP to 'frameDuration'
    BOUNCE_RANGE to 'bounceRange'

  * Fix: Mousewheel events on a horizontally scrolling instance no longer prevent page scrolling (#2532739)

  * Fix: Mousewheel events now properly update the `scrollY` attribute.
  
  * Fix: Improved reliability of the scrollEnd event. Now it now only fires 
    once per scrolling sequence, instead of sometimes twice. 

  * Fix: Resolved issue where multiple listeners could sometimes be added for drag and flick events.
  
  * Fix: Improved gesture event detachment

  * Fix: Refactored _flickFrame to do less attribute lookups, helpful for performance reasons

  * Fix: Resolved issue where scrollview.pages.scrollTo may not actually scroll to the desired page, or may cause a lock-up of the widget.


Widget Change History
---------------------

 * Fixed regression in `Widget.getByNode()`, introduced in 3.5.0, where the 
   Widget would not be found if the user changed the id of the boundingBox node,
   after the widget was rendered.

   We go back to using the Node's guid for caching instead of the DOM node id.

   The change was originally made to lay the groundwork for string based rendering,
   where a boundingBox node reference would not be present during initialization.

   This can still be achieved post-render by populating the instance map, after a 
   Node reference has been established/added to the DOM (when we get there).


XML Change History
------------------

* Moved from Y.Datatype.XML to Y.XML


YUI Core Change History
-----------------------

* Improved the performance of `Y.merge()` by 10 to 40% (depending on the
  browser). [Ryan Grove]