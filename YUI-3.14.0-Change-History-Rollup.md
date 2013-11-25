## AutoComplete Change History

* Fixed: List doesn't close when it loses focus after scrolling.
  ([#981][]: @rgrove)

[#981]: https://github.com/yui/yui3/issues/981

## Button Change History


* Fixed `disabledChange` listener to correctly disable or enable 
  buttons. ([#1374][]: @drjayvee)

[#1374]: https://github.com/yui/yui3/pull/1374

## Calendar Change History


* Fix an undeclared variable ([#1307][])

[#1307]: https://github.com/yui/yui3/issues/1307

## Charts Change History


* [#1402](https://github.com/yui/yui3/issues/1402) Remove Y.Clone.
* [#1393](https://github.com/yui/yui3/issues/1393) Address issue in which Candlestick series does not render nicely when there are large amounts of data.
* [#1392](https://github.com/yui/yui3/issues/1392) Address issue in which histograms threw errors when groupMarkers is set to true and there is missing data.
* [#1391](https://github.com/yui/yui3/issues/1391) Address issue in which histograms did not always size and space properly when used outside of charts app.
* [#1390](https://github.com/yui/yui3/issues/1390) Address issue in which histograms threw error when used independently from the larger chart app.
* [#1382](https://github.com/yui/yui3/issues/1382) Address issue in which first/last values were removed from axis when hideFirstMajorUnit/hideLastMajorUnit were set to true.
* [#1381](https://github.com/yui/yui3/issues/1381) Added ability to offset labels in Axis.

## CSS Grids Change History


* Grids is now imported into YUI from Pure via Grunt. ([#1240][])


[#1240]: https://github.com/yui/yui3/issues/1240


## CSS Normalize Change History

* Normalize is now imported into YUI from Pure via Grunt. ([#1240][])


[#1240]: https://github.com/yui/yui3/issues/1240


## DataTable Change History

* Added datatable-keynav module, providing keyboard navigation within the
  datatable. [Pull Request [#596](https://github.com/yui/yui3/issues/596) ]



## Rich Text Editor Change History


* Fix Y.Frame issue where the linked CSS in the frame was trying to call
  `/undefined`. ([#1367][]: @ipeychev)

[#1367]: https://github.com/yui/yui3/issues/1367

## Get Utility Change History


* Preserve `global` as `this` when executing a yui module in nodejs ([#1360][])

[#1360]: https://github.com/yui/yui3/pull/1360

## Graphics Change History


* [#1398](https://github.com/yui/yui3/issues/1398) Address issue in which canvas implementation does not position itself properly within a container.
* [#1375](https://github.com/yui/yui3/issues/1375) Address issue in which path does not stroke correctly in svg implementation. 

## Node Change History

* Addition of `paste`, `copy`, and `cut` to Node's event white list. ([#1350][]: @JetFault)
[#1350]: https://github.com/yui/yui3/issues/1350

## Number Change History

* PR [#587](https://github.com/yui/yui3/issues/587) Parse can now parse all the formats that format can produce.
* Fixed regression in `Y.Number.parse` with strings containing only
  whitespace. ([#1427](https://github.com/yui/yui3/pull/1427))

## Promise Change History


* Marked `getStatus` as deprecated.

## YUI Test Change History


* Added Y.ArrayAssert.isUnique()


## Transition Change History

* Fixed issue where `toggleView` did not correctly work when passed only an effect name. ([#1258][] @ezequiel)

[#1258]: https://github.com/yui/yui3/issues/1258


## Uploader Utility (New) Change History

* Addition of XHR's `responseText` to `uploaderror`'s event payload. ([#1356][]: @semafor)

[#1356]: https://github.com/yui/yui3/issues/1356

## YUI Core Change History


* Added support to the YUI module system to work with modules written as
  ECMAScript Modules which are transpiled to YUI modules. ([#1407][])

  Modules are being added to ES6, but need to be transpiled into code that can
  run in today's JavaScript environments. This changes makes it possible for YUI
  modules to work as ES6 Module transpile target.

  An `es` flag on a YUI module's `details` signals to the YUI module system and
  Loader that the module was transpiled from a ES6 module; this allows YUI to
  conform to the module body's expectations around imports and exports.

  When the `es` flag is set to a truthy value, the module body function will
  receive two additional arguments: `imports` and `exports`, giving it the
  signature: `function (Y, NAME, __imports__, __exports__) {...}`. Also, the
  module body's `return` value becomes significant and is used and stored as the
  module's `exports`.


[#1407]: https://github.com/yui/yui3/issues/1407