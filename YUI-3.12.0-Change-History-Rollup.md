
## App Framework Change History




### ModelList

* Added support for descending sort order via `sort({descending: true})`. In
  order to support this, the `options` passed to `sort()` are now passed along
  to the protected `_sort()` method. ([#1004][]: @rishabhm)

### Router

* Added support for registering route param handler functions or regexps. This
  allows routes to be defined as string paths while adding validation/formatting
  to route params, e.g., `"/posts:id"`, and register an `id` param handler to
  parse string values into a number and make it available at `req.params.id`.
  ([#1063][])

* Fixed issue with trying to URL-decode matching path segments that are
  `undefined`. Routes defined as regexps (instead of strings) can contain an
  arbitrary number of captures; when executing the regex during dispatching, its
  array of matches can contain `undefined` values. Router will now check that a
  match is a truthy value before trying to URL-decode it, and coerce `undefined`
  values to empty strings. ([#964][], [#1076][])


[#964]: https://github.com/yui/yui3/issues/964
[#1004]: https://github.com/yui/yui3/issues/1004
[#1063]: https://github.com/yui/yui3/issues/1063
[#1076]: https://github.com/yui/yui3/issues/1076


## Button Change History



* `ButtonGroup.disable()` will disable each child button (or input, see `getButtons()`)

## Calendar Change History



* Added language support for various Chinese regions. ([#1007][]: @shunner)


[#1007]: https://github.com/yui/yui3/issues/1007


## Charts Change History



* #716 Added logarithmic scaling.

## Event Infrastructure Change History



* Fixed: YUI no longer breaks the browser back/forward cache by attaching an
  unnecessary `unload` event handler. [Ryan Grove]

* `event-tap` allows you to prevent default browser behavior on `tap` via
  `e.preventDefault()` [#682](https://github.com/yui/yui3/issues/682)

* `event-tap` now has a `sensitivity` property that can be passed as an option.
  This allows you to customize when `tap` fires, based on the difference in `px`
  between a the corresponding start and end event. [#631](https://github.com/yui/yui3/pull/631)

* `event-tap` has dual-listener support, and works properly on devices that support
  both mouse and touch input. [#683](https://github.com/yui/yui3/issues/683)

* `event-tap` works more reliably on Android 4.0.x (Ice cream sandwich).


## Custom Event Infrastructure Change History



* Fixed regression introduced in 3.10.0, where `EventTarget.detach('cat|*')`
  would throw an exception, when the EventTarget was configured with a prefix.

## Node Change History



* Fixed: Node instances that were cached before `node-pluginhost` was loaded
  couldn't become plugin hosts. [Jeroen Versteeg]

* Fixed: `Node#toggleView()` didn't show a node if that node's `hidden`
  attribute wasn't set (this was a regression in 3.10.2). [Jeroen Versteeg]

* Fixed: `Node#addMethod` could not bind to contexts other than itself. ([#1070][]: @zhiyelee)

[#1070]: https://github.com/yui/yui3/issues/1070

## TabView Change History



* Fixed missing ARIA role in the `tablist` of Tabview.
  ([#1035][]: @blzaugg)

[#1035]: https://github.com/yui/yui3/issues/1035

## Template Change History



* Added central template registry. The template registry decouples making
  templates available from invoking a template to render it. This central
  registry and abstraction of templates to names separates concerns, creates a
  level of indirection, and enables templates to be easily overridden.
  ([#1021][])

[#1021]: https://github.com/yui/yui3/issues/1021

## Tree Change History



* Fixed: `Tree.Sortable` failed to reindex a node's children after sorting them,
  which could result in `Tree#indexOf()` and `Tree.Node#index()` returning
  incorrect indices. [Ryan Grove]
