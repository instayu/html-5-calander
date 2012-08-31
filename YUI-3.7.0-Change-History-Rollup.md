The changes included in the YUI 3.7.0pr1 are listed below, per component. Components not listed were not changed in 3.7.0pr1.

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


Collection Change History
-------------------------

* Added `Y.Array.flatten()`. This method flattens arrays of arrays into a single
  flat array.


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


ScrollView Change History
-------------------------

Detailed overview of all changes (including protected/private) @ https://gist.github.com/3522590

Public API changes/fixes:

  * Added: Forced-Axis and Dual-Axis Support - ScrollView now has an optional axis property that can be declared with values: "x", "y", or "xy". (#2532631)

  * Added: Initial support for RTL (Right-To-Left) layouts (#2531874).

  * Moved: Paginator’s scrollTo() method has been deprecated and replaced with scrollToIndex. (##2530145)

  * Fix: Improved reliability of the scrollEnd event. It now only fires once per scrolling sequence, instead of multiple times. 

  * Fix: Multiple listeners could sometimes be added for drag and flick events.

  * Fix: Mousewheel events now properly update the 'scrollY' attribute.

  * Fix: Bug where scrollview.pages.scrollTo may not actually scroll to the desired page, or may cause a lock-up of the widget.

Additional notes:

  * Unit test coverage on scrollview-base and scrollview-paginator are both at 80+% (#2532288, #2532287)


Event Infrastructure Change History
-----------------------------------

* Changed event-synthetic, to support CustomEvent performance optimizations.

  Mainly the deprecation of CustomEvent subscribers and afters instance properties,
  which event-synthetic was referring to directly. The direct reference was replaced
  by a public API method call.

  See src/event-custom/HISTORY.md for more details about the deprecated properties.

* Added try/catch around the internal window unload listener event-base adds,
  so that YUI works in Chrome Packaged Apps. They don't support unload,
  but still have a window.onunload, so no real way to feature test without
  a try/catch anyway.


GestureSimulation Change History
--------------------------------

* Initial release.


Pjax Change History
-------------------

* Extracted `Y.PjaxContent` from `Y.Pjax`. Pulling out the content-handling
  functionality allows it to be used by other components, like `Y.App`.
  [Ticket #2532487]

