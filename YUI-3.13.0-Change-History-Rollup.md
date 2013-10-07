## App Framework Change History



### App

* Added `req.app` which is a reference to the app instance.

### Router

* __[!]__ A router's `root` path is now enforced as its mount point. Routers
  with a specified `root` will only consider paths as matching its route handles
  if that path is semantically within the router's `root` path. For example:

    ```js
    router.set('root', '/app/');

    router.hasRoute('/app/');    // => true
    router.hasRoute('/app/foo'); // => true
    router.hasRoute('/bar/');    // => false
    ```

  This fixed some issues with paths being erroneously considered matching even
  when they were not semantically within the router's `root` path. ([#1083][])

* __[!]__ The `getPath()` method now returns the _full_ current path, whereas
  before it returned the current path relative to the router's `root`. This also
  affects `req.path` which is now the full path as well.

* __[!]__ Changed Router's dispatching process to take `req` and `res` objects
  instead of creating them inside the `_dispatch()` method. This refactor also
  removed the deprecated support for calling `res()` as an alias for `next()`.

* Router now accepts route objects through its `route()` method. These route
  objects are the same as those specified in a router's `routes` attribute and
  what Router uses for its internal storage of its routes. If these route
  objects contain a regular expression as their `path` or they contain a `regex`
  or `regexp` property, then they are considered fully-processed. Route objects
  can also contain any arbitrary metadata which will be preserved. ([#1067][])

* Added `req.router` which is a reference to the router instance.

* Added `req.route` which is a reference to the current route object whose
  callbacks are being dispatched.

* Calling the `dispatch()` method will now set `req.src` to `"dispatch"`.

### Model

* Added ModelSync.Local, an extension which provides a `sync()` implementation
  for `localStorage` that can be mixed into your Models and ModelLists.
  Examples of it in use can be seen in the [YUI TodoMVC][] example. ([#1218][])


[#1067]: https://github.com/yui/yui3/issues/1067
[#1083]: https://github.com/yui/yui3/issues/1083
[#1218]: https://github.com/yui/yui3/issues/1218

[YUI TodoMVC]: https://github.com/tastejs/todomvc/tree/gh-pages/architecture-examples/yui


## Button Change History



* Added a `labelHTML` attribute to `Y.ButtonCore` for nested HTML label support
* Due to a fix in `Y.Widget` (#1125), `Y.Button` now correctly retains all node attributes upon render

## Calendar Change History



* Fix a issue with cloudn't select a date when passing minimumDate. ([#1030][])
* Removed superfluous strings from Hungarian calendar translations. ([#1054][]: @drjayvee)

[#1030]: https://github.com/yui/yui3/issues/1030
[#1054]: https://github.com/yui/yui3/issues/1054

## DataTable Change History

* Add highlight module [Pull Request #1196]

* Document updates and variable changes to improve understanding of code
  [Pull Request #946] [Satyam]

* Add Show All to language packs. [Pull Request #1173] [Issue #1167]

* Added 'contentUpdate' after the DataTable has been updated when triggered
  from a `dataChange` event. [Pull Request #1072][Issue #1052]

* Fix issue where recursive nesting of objects was cloned infinitely
  [Pull Request #1008][Ticket #915]

* Fix issue where Paginator count becomes out of sync with DataTable when
  DataTable data is modified (added or removed) [Pull Request #1011] [Issue #1010]

* Add French language pack for DataTable's Paginator. ([#1166][] @Naouak)

[#1166]: https://github.com/yui/yui3/pull/1166

## Rich Text Editor Change History


* Add in `getEditorOffset` to calculate distance from current selection to the
  beginning of the editor. [Pull Request #1232]

* Editor is able to work in two modes - as an Inline Editor or using an iframe.
  For that reason, some internal changes have been made:

  Y.Frame is now a plugin and extends Y.Plugin.Base.

  There is a new Plugin, called ContentEditable. This plugin allows
  editor to work without using an iframe, as an inline editor.

  If a container is not specified, EditorBase creates and plugs an instance of
  Y.Frame. Otherwise, it uses the provided container (ContentEditable)

  Added Y.InlineEditor which extends EditorBase and plugs ContentEditable
  during the initialization process.

  [Ticket #1041] [ipeychev]

## Event Infrastructure Change History



* Delegated focus and blur events now behave the same way other events do when
  a delegate sub from a container closer to the target calls
  `e.stopPropagation()`. Delegate subs from containers higher in the parent
  axis are not notified. [#1145](https://github.com/yui/yui3/issues/1145)

## Custom Event Infrastructure Change History



* Made `addTarget` and `removeTarget` chainable.

## ValueChange Change History



* Updated ValueChange to support `<select>` and `[contenteditable="true"]`
  elements as well. ([#1184][])

[#1184]: https://github.com/yui/yui3/issues/1184

## File Module Change History



* Added a check to make sure the XHR exists before aborting. ([#1053][] @JetFault)

[#1053]: https://github.com/yui/yui3/issues/1053

## Graphics Change History



* #1138 Address issues with orphan elements after destroy.

## History Change History



* Fixed a possible exception in `HistoryHTML5._init()` in IE10.
  [Ariel Schiavoni]

* Added a workaround for a `replaceState` bug in Chrome/WebKit.
  ([#1159][]: @roblund)

* Fixed issue with `parseHash` not parsing blank values in hash string.
  ([#1116][]: @blzaugg)

[#1116]: https://github.com/yui/yui3/issues/1116
[#1159]: https://github.com/yui/yui3/issues/1159

## Node Change History



* Fix issue causing `inDoc` to fail if Node wasn't bound to a node.
  [Pull Request #1169][Issue #1168]


## ScrollInfo Node Plugin Change History



* Fixed `getOffscreenNodes()` and `getOnscreenNodes()` even harder (they could
  still return incorrect information in certain cases). [Ryan Grove]

## Paginator Change History



* Correct typo in NAME param for paginator.js

## Transition Change History



* Added optional flag to NodeList.transition which, if true, fires the callback only once at the end of the NodeList transitions. ([#880][] @Perturbatio)

[#880]: https://github.com/yui/yui3/issues/880

## Uploader Utility (New) Change History



* Fixed typo with event `uploadcancel`. ([#1053][] @JetFault)

[#1053]: https://github.com/yui/yui3/issues/1053

## Widget Change History



* Removed widget-locale module.
* Improved support for single-box widgets (BB === CB) by defaulting boundingBox to srcNode if CONTENT_TEMPLATE is null.

## YUI Core Change History



* Added `Y.Lang.isRegExp()` method.
