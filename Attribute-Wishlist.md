This is a grab-bag of things that would be nice to have in `Y.Attribute`.

## 3.6.0

* **Value filters.** ([Detailed proposal here](https://gist.github.com/2025242)) It would be a huge boon to the security of the library if Attribute supported pluggable filters that could be run when a string value is retrieved. For example, to get a raw value: `.get('foo')`. To get an HTML-escaped value: `.get('foo:html')`. To get a URL-encoded value: `.get('foo:url')`.

* **Coalesced change events.** A call to `setAttrs()` that changes multiple attributes should fire a single coalesced change event in addition to the individual change events. This is currently implemented in `Y.Model`. [Ticket #2530248](http://yuilibrary.com/projects/yui3/ticket/2530248)

* **Better support for sub-attribute getters.** Currently, getters are required to return an entire object even when triggered by a sub-attribute retrieval like `.get('foo.bar.baz')`. This is inefficient and can be confusing.

* <strong>`set()` and `setAttr()` should support an options object.</strong> The internal `_setAttr()` method supports an `options` object as its third parameter, and mixes it into the event facade of the change event. This is very useful (it's used in `Model` and `ModelList`), but the public `set()` and `setAttrs()` methods don't currently support the `options` param.