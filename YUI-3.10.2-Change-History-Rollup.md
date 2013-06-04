YUI 3.10.2 Change History Rollup
================================

## Anim Change History

* Remove unnecessary `code` tag [zenorocha]

## App Framework Change History



### Router

* Router now properly dispatches when using hash-based URLs and calling
  `replace()` without arguments; before it would throw an error. [#739]


## Attribute Change History



* opts now passed to setter correctly, when using AttributeObservable.

  This feature was added in 3.8.1 (below), but didn't work for
  AttributeObservable.

## Charts Change History



  * #743 Addressed issue in which styles don't map correctly to a legend when series are styled using a global style object. 
  * #706 Addressed issue in which the legend did not honor specified series marker style for shape. 

## Color Change History


* Move Y.Color out of DOM [Pull Request #576] [apipkin]

## Dial Change History


  * Fixed GitHub Issue #591: Dial was intermittently sticking at min when
  drag below min, and then back above min. This was only happenening when
  min/max was at a position of North on the dial.

## Event Infrastructure Change History



* Fixed `nodelist.on()` for rare custom module use cases.

  In certain rare custom module loading circumstances [#2533242,
  https://github.com/yui/yui3/pull/689] dom-core is attached after
  event-base, which resulted in the `YDOM = Y.DOM` module level reference
  being undefined [1].

  This would break things like `nodelist.on()` which used the reference
  under the hood.

  [1] Added in 3.7.3, as part of the Win8 `isWindow()` fix.

* Fixed DOM event facade, when Y instance was set to emitFacade:true.

  With the Y instance's emitFacade set to true, DOM event subscriptions
  would receive a Y.EventFacade instance instead of a Y.DOMEventFacade
  instance, and as a result target and currentTarget would be set to
  the Y instance, instead of a Y.Node instance.

## Custom Event Infrastructure Change History


* Fixed issue with facade carrying stale data for the "no subscriber" case.

* Fixed regression where `once()` and `onceAfter()` subscriptions using the
  `*` prefix threw a TypeError [#676]. `target.once('*:fooChange', callback)`

* Fixed exception with fire(type, null) with emitFacade:true.

## Graphics Change History



  * #701 Addressed rounding issue in svg implementation. This bug surfaces in edge cases of the PieChart in the charts module.

## Handlebars Change History



* Upgraded Handlebars.js to v1.0.11. See [Handlebars' release notes][v1.0.11].

[v1.0.11]: https://github.com/wycats/handlebars.js/blob/master/release-notes.md#v1011


## Node Change History



* The `show()` and `hide()` methods now set and remove a node's `hidden`
  attribute, which provides a semantic indication of hidden content and improves
  accessibility. [Gerard Cohen]

## ScrollView Change History



  * Paginator API methods now respect the widget's `disabled` ATTR

## Simple YUI Change History



* [!] DEPRECATED: Simple YUI has been deprecated as of YUI 3.10.2.  This module will be removed from the library in a future version.

## Widget Change History



  * Fixed contentBox remaining in Y.Node _instances cache, when
    widget hasn't been rendered, and `widget.destroy(true)` [deep destroy]
    is used.

## YUI Throttle Change History




* Throttle no longer changes the value of `this` inside the throttled function.