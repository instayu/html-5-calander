## App Framework Change History

### Router

* Decode URL-encoded path matches for Router's `req.params`. [Ticket #2532941]


## Attribute Change History

* [!] The `AttributeEvents` class extension and the `attribute-events` module
  have been renamed to `AttributeObservable` and `attribute-observable`
  respectively. The old names are deprecated, but have been retained as aliases
  for backwards compatibility. They will be removed in a future version of YUI.

* [!] The `AttributeComplex` class extension and the `attribute-complex` module
  have been deprecated. This functionality is now part of `AttributeCore`, and
  this extension and module are no longer needed.

* Moved AttributeCore's protected `_protectAttrs()` utility method to a public
  static method, `protectAttrs()`, which is available on both `Y.Attribute` and
  `Y.AttributeCore` namespaces.


## Base Change History

* `Y.Base.create()` can now be used with `Y.BaseCore`, in addition to its
  existing usage with `Y.Base`. This allows non-observable, BaseCore hierarchies
  to use class extensions.

* Extracted the `Y.BaseObservable` class extension from `Y.Base`. This is a new
  class extension for `Y.BaseCore` which adds support for observability. This
  allows BaseCore subclasses to mix-in BaseObservable at runtime, bringing their
  functionality up to that of `Y.Base`.

## Charts History

* #2532955 Addressed issue in which click events were not firing on elements outside of chart in ios.

## Color Change History

* Initial release.


## Cookie Change History

* Pull Req: 248 - Make order of cookie loading with the same name configurable


## Drag and Drop Change History

* 2532824 - Performance tweaks
* Pull Req: 309 - Fixed Safari scrolling issue


## Pjax Change History

* Fix issue where Pjax would throw an error because of calling methods on `null`
  nodes when an IO request was aborted (which happens to pending requests when
  a new request comes in.)


## ScrollView Change History

  * Paging is now only triggered when a swipe crosses a mid-point threshold, to match the < 3.7.0 behavior (#2532745)

  * Fixed issue where Mousewheel could prevent next()/prev() API interaction on horizontally paginated instances (#2532815)

  * scrollToIndex now sets correct default value for easing (#2532895) 

  * ScrollViewPaginator#scrollToIndex now properly respects animation duration and easing arguments (thanks juandopazo)
  
  * General cleanup


## Template Change History

* Initial release.


## YUI Core Change History

* Added `Y.config.global` as an alias to the global scope