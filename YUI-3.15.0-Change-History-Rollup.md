## App Framework Change History



* __[!]__ Refactored `ModelSync.Local` to use a different, more readable
  storage system. This new storage system is backwards-incompatible with
  the old storage system. However, the API remains the same and no application
  code needs to be changed unless you want to maintain the data that is
  present in `localStorage` today. ([#1597][])

* Fixed an issue where `history-hash-ie` loaded on non-IE browsers. ([#1613][]: @ezequiel)

[#1613]: https://github.com/yui/yui3/pull/1613

## Attribute Change History

* Fixed an issue that caused `reset()` to fail when resetting an attribute called `'length'`.


## Calendar Change History


* Fix calendar to use `visibility:inherit` instead of `visibility:visible`, for compatibility with overlays. ([#1627][]: @jafl)
* Fix an issue when Feb 1st is Saturday Mar 2nd appears to be selectable. ([#1559][]: @shunner)

[#1627]: https://github.com/yui/yui3/issues/1627
[#1559]: https://github.com/yui/yui3/issues/1559

## Charts Change History

* [#1480][] Address issue in which _maxSize property was not updated for single series histogram. 
* [#1632][] Add labelFormat attribute to CategoryAxisBase and CategoryAxis.

[#1480]: https://github.com/yui/yui3/pull/1480/
[#1632]: https://github.com/yui/yui3/pull/1632/

## Date Change History

* Roll back to 3.13.0

## Drag and Drop Change History

* Fix a bug that doesn't fire `drop:hit` event. ([#1573][]: @hacklschorsch)
* Prevent the default page action when starting a `gesturemove` event. This
  fixes browsers that select the text when dragging. ([#1557][]: @andrewnicols)

[#1573]: https://github.com/yui/yui3/issues/1573
[#1557]: https://github.com/yui/yui3/issues/1557

## DOM Change History


* [#1603][]: Set a node value to an empty string setting to null. [Ryuichi Okumura]
* [#1469][]: Fix a bug with setStyle() cannot set an opacity to 1. [Ryuichi Okumura]

[#1603]: https://github.com/yui/yui3/issues/1603
[#1469]: https://github.com/yui/yui3/issues/1469

## Event Infrastructure Change History




* Reduced categories of certain noisy log events in the `event` module and added
  categories for those that were missing some. ([#1605][]: @andrewnicols)

* Fixed the `event.returnValue is deprecated` warning in chrome. ([#1460][]: @zhiyelee)

[#1605]: https://github.com/yui/yui3/issues/1605
[#1460]: https://github.com/yui/yui3/issues/1460



* Added support for W3C Pointer events in the `tap` event. This fixes an issue in IE11 where the `type` of pointer event objects was changed from `MSPointerDown` to `pointerdown` to comply with their proposed W3C standard.

## Event Simulate Change History

* Whitelisted W3C Pointer events for simulation.

## Graphics Change History

* [#1543][] Parse rgba value into color string and opacity value for vml fill and stroke. 
* [#1566][] Addressed issue with path chaining in canvas implementation of graphics. 

[#1543]: https://github.com/yui/yui3/pull/1543/
[#1566]: https://github.com/yui/yui3/pull/1566/

## IO Change History

* Fixed an issue in `io-upload-iframe` where an attempt to reset the attributes of the `form` element could have occured on a `form` that no longer existed on the page. ([#1465][]: @andrewnicols)

[#1465]: https://github.com/yui/yui3/pull/1465/


## Loader Change History

* Optimization of the `calculate` method, which now utilizes a topological sort (a variation of a depth first search) to generate a valid dependency order. ([#1606][]: @ezequiel)

[#1606]: https://github.com/yui/yui3/pull/1606

## Promise Change History

 * Deprecated `resolver.then` in favor of `resolver._addCallbacks`.
 * Added new methods following the new emerging ES6 standard for promises. This includes `promise.catch`, `Promise.all`, `Promise.race`, `Promise.resolve` and `Promise.reject`.

## YUI Test Change History




* Added test.next(fn) which returns a callback that automatically
  resumes asynchronous tests.

## Timers Change History




* Import `asap.js` as the underlying implementation of `Y.soon`. This changes
  slightly the semantics of `Y.soon`: tasks scheduled during the flushing of
  asap's queue are pushed to the end of the queue and not scheduled to a new
  tick.

## Widget Modality Change History




* Fixed a bug where the widget would focus before it was actually rendered,
  leading to a jump in the window position. ([#1636][]: @andrewnicols)

[#1636]: https://github.com/yui/yui3/pull/1636

## YUI Core Change History




* Added `Y.require()` for importing ES6 modules. It's similar to `Y.use()` but
  it follow the following signature:

```js
YUI().require('some-es6-module', function (Y, imports) {
  var foo = imports['some-es6-module'].foo;
});
```
* Set default `logLevel` to `info` if missing or not a real category.
  ([#1610][]: @andrewnicols)
* Fixed value of `this` inside ES6 module definitions.

* Fixed UA detection in recent versions of the Amazon Silk browser.
  ([#1576][]: @adinardi)

[#1576]: https://github.com/yui/yui3/pull/1576
[#1610]: https://github.com/yui/yui3/pull/1610
