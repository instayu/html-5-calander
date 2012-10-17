App Framework Change History
----------------------------

### App

* Add support for App Transitions in browsers which support native CSS3
  transitions without using vendor prefixes. This change means IE10 and Opera
  get view transitions.


Console Change History
----------------------

* Remove `for` attribute from Console's HTML templates. There is a bug in the
  WinJS runtime for Windows 8 apps that causes an error to be thrown incorrectly
  when certain element attributes used. [Ticket #2532792]


DataSchema Change History
-------------------------

* Implemented a partial fix for allowing XPath access to XML elements in IE10
  Desktop, Metro, and WinJS environments. A known issue of IE10 WebView not
  allowing XPath addressing is still standing. [Ticket #2532796]


DataSource Change History
-------------------------

* `datasource-xmlschema` now forces input through the `Y.XML` parser.
  [Ticket #2532838]


Drag and Drop Change History
----------------------------

* 2532718 don't stop gesture start, but prevent gesture move to allow clicks
* 2532837 Unreg gesturemoveend on _unprep
* Switched DD over to Y.UA.touchEnabled
* DD should completely pass lint now


Rich Text Editor Change History
-------------------------------

* 2532807 fixed regex for ie10
* Converted some tests to work in IE10 better
* Convert innerHTML iframe creation to DOM for IE 10
* Should completely pass lint now


Gestures Change History
-----------------------

  * `event-move` supports the -ms-touch-action property in IE10.
  Nodes subscribing to events defined in event-move will have their
  styles updated to `-ms-touch-action:none`. It will be reset when
  listeners are detached.

  http://msdn.microsoft.com/en-us/library/windows/apps/hh767313.aspx


Event Infrastructure Change History
-----------------------------------

* Changed onbeforeactivate feature test to account for Win 8 packaged Apps, which
  don't allow inline JS code in innerHTML.

  http://msdn.microsoft.com/en-us/library/windows/apps/hh465388.aspx


Get Utility Change History
--------------------------

* Fixed Get issues, highlighted by IE10. 

  1) IE10 seems to interrupt JS execution, in the case of a 304'ing script to invoke
  the onLoad handler. If this happened inside the transaction execute loop, the transaction
  would terminate early (call onSuccess before all scripts were done), because the _waiting
  count would only reflect the number of scripts added to the DOM, when the loop was
  interrupted. Changed the logic so that we only finish a transaction when the expected 
  number of requests are accounted for which seems reasonable in general.

  Also wrapped the internal onLoad/onError callbacks in a setTimeout for IE10, so we're 
  re-introducing asynchronicty for external onSuccess, etc. app code. We can take this out 
  when/if the bug below gets fixed. 

  http://connect.microsoft.com/IE/feedback/details/763871/dynamically-loaded-scripts-with-304s-responses-interrupt-the-currently-executing-js-thread-onload

  2) transaction._finish() would move on to the next transaction, before the current 
  transaction's onSuccess/Finish/End listeners were invoked, since the logic to move to 
  the next transaction was invoked before the `on` listeners were invoked. This meant that
  for all browsers, when issuing a CSS transaction followed by a JS transaction, the CSS
  success callback wouldn't be invoked until the JS transaction was initiated.

  3) Added user-agent to feature test for async support, because IE10 wasn't returning true for it.
  If IE10 ends up fixing the issue below by GA, we'll pull out the explicit ua test.

  https://connect.microsoft.com/IE/feedback/details/763477/ie10-doesnt-support-the-common-feature-test-for-async-support

  ---

  Get should work OK with IE10 now aside from one pending issue. If you issue 2 Get 
  requests to the same 404ing script, IE10 doesn't call the success handler for the 
  subsequent valid (200 etc.) request. This seems to be an IE10 issue, which we cannot
  control:

  https://connect.microsoft.com/IE/feedback/details/763466/ie10-dynamic-script-loading-bug-async-404s


IO Utility Change History
-------------------------

* Fixed issue in Chrome where form submits with `upload: true` were not working
  properly. [Ticket #2531860]

* Add `empty()` method to io-queue which clears out all requests waiting to be
  sent. [Pull Request #282] [Julien Sanchez]


JSON Utility Change History
---------------------------

* Updated to use native JSON when in Node.js


Resize Utility Change History
-----------------------------

* Should completely pass lint now


Sortable Utility Change History
-------------------------------

* Should completely pass lint now


Transition Change History
-------------------------

  * Add support for non-vendor-prefixed syle and CSS properties. `Y.Transition`
    now supports IE10 and Opera.

  * Transition durations are now normalized from seconds to milliseconds before
    updating the node's style. **Note:** This does _not_ affect the public API
    which still uses second-based duration times.


Widget Buttons Change History
-----------------------------

  * Fixed bug with a widget's `defaultButton` changing by binding to the
    `defaultButtonChange` event in WidgetButtons' `initializer()`.


XML Change History
------------------

* Modified the XML parsing to use the new Windows XML parsing APIs when they are
  available. This is a partial fix. [Ticket #2532796]


YQL Change History
------------------

* Added yql-winjs and yql-nodejs modules for native interactions in these environment


YUI Core Change History
-----------------------

* Adding Y.UA.touchEnabled boolean to use in conditional modules
* 2532797 - Added IE10 ua fixing for Windows8 WinJS
* 2532675 - Remove the second air property