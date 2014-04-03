## App Framework Change History



### Router

* Fixed issue where Router's `hasRoute(url)` method did not follow the same
  semantics as the route dispatching process. Now all registered param handlers
  will process any named params, giving them a chance to validate and reject a
  param value. This will make the `hasRoute()` method an effective way to check
  whether a router will dispatch to a route handler for a given URL. ([#][])


[#1722]: https://github.com/yui/yui3/issues/1722


## Calendar Change History




* [#1685][]: Can't change month in RTL mode / arrow wrongly displayed in RTL mode ([#1719][] [#1724][]: Andrew Nicols)
* [#1361][]: Change to use CSS instead of the image to showing of the arrow (Marc Lundgren)

[#1724]: https://github.com/yui/yui3/pull/1724
[#1719]: https://github.com/yui/yui3/pull/1719
[#1685]: https://github.com/yui/yui3/issues/1685
[#1361]: https://github.com/yui/yui3/pull/1361

## CSS Grids Change History




* Import Grids from Pure 0.4.2. You can now use non-reduced fraction class names when laying out a grid. This means that we have rules for classes such as `.pure-u-12-24` as well as `.pure-u-1-2`.

## CSS Normalize Change History




* Import Base from Pure 0.4.2. You can now set a `[hidden]` attribute to your HTML elements if you want them to be `display: none;`.

## DataTable Change History

* Fixed an issue where the UI did not render correctly in print preview for IE 11. ([#1708][]: @annumanuel)

[#1708]: https://github.com/yui/yui3/pull/1708



## DOM Change History

* Optimize dom-style.js. Remove unnecessary anonymous function, unused variables. Use "Number()" instead of "new Number()". [Ryuichi Okumura]

## Drag and Drop Change History


* [#1721][] Move preventDefault to gesturemovestart (Andrew Nicols)
* [#1663][] DDProxy will reset radio inputs when cloneNode==true ([#1666][]: Chema Balsas)
* Remove name attribute radio inputs inside cloned nodes by dd-proxy. [Chema Balsas]

[#1721]: https://github.com/yui/yui3/pull/1721
[#1666]: https://github.com/yui/yui3/pull/1666
[#1663]: https://github.com/yui/yui3/issues/1663

## Rich Text Editor Change History

* Fixed an issue where the `yui-cursor` selector was used as an `id` instead of a `class`. ([#1648][]: @alaaibrahim)

[#1648]: https://github.com/yui/yui3/pull/1648

## Event Infrastructure Change History

* Added the spacebar key mapping to ensure correct ARIA and WCAG compliance. ([#1642][]: @andrewnicols)

[#1642]: https://github.com/yui/yui3/issues/1642




## IO Utility Change History

* Removed the unnecessary `src` attribute which caused an extra request to be made to the current page URL when the `iframe` was included on the page. ([#1646][]: @goodforenergy)

* Document usage of username/password in Y.io config. ([#1572][]: @customcommander)

[#1646]: https://github.com/yui/yui3/pull/1646
[#1572]: https://github.com/yui/yui3/pull/1572


## YUI Loader Change History




* Optimization of the Loader's constructor by removing _populateCache() in  in favor of an on-demand process to create internal module info based on the raw meta when the module is needed and called thru `getModuleInfo()`. ([#1581][]: @caridy)

[#1581]: https://github.com/yui/yui3/pull/1581

* Removal of  `onCSS` documentation, as it was never implemented. ([#1743][]: @ezequiel)

* Fixed an issue where a module's `lang` packs were not being included before the module itself. ([#1743][]: @ezequiel)

* Fixed an issue where conditionally loading a module using `before` did not work. ([#1743][]: @ezequiel)

* Fixed an issue where a `CSS` module could not require a `js` module. ([#1743][]: @ezequiel)

[#1743]: https://github.com/yui/yui3/pull/1743

## Node Change History




* getCell() throws an error if `shift` is not a recognized value.
* Switched "instanceof Y.Node" to check for `_node`, to allow instances
  from other sandboxes.
* Clarified Node vs NodeList method docs. (@solmsted)


## Promise Change History




* Errors thrown inside the promise initialization function reject the promise.

## Sortable Utility Change History




* [#1486][]: Fix a issue that zIndex of 999 is kept on dragged item (Paul B.)

[#1486]: https://github.com/yui/yui3/pull/1486

## YUI Test Change History

* `test.next` now takes an optional argument to change the value
  of `this` inside the callback.


## Widget Modality Change History




* Fixed the positioning of the modal mask for stacked modals.
  ([#1684][]: @moiraine)

[#1684]: https://github.com/yui/yui3/pull/1684

* Fixed an issue where Widget-Modality did not function correctly when a modal widget
  and its mask were subsequently cloned by something else. ([#1175][]: @jinty)

[#1175]: https://github.com/yui/yui3/pull/1684


## YQL Change History




* Fixed an issue where `yql-jsonp`, `yql-nodejs`, and `yql-winjs` were missing `yql`
  from their `requires` list. ([#1737][]: @ezequiel)

[#1737]: https://github.com/yui/yui3/issues/1737


