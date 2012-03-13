This is a grab-bag of things that would be nice to have in `Y.Attribute`.

## 3.6.0

* **Value filters.** ([Detailed proposal here](https://gist.github.com/2025242)) It would be a huge boon to the security of the library if Attribute supported pluggable filters that could be run when a string value is retrieved. For example, to get a raw value: `.get('foo')`. To get an HTML-escaped value: `.get('foo:html')`. To get a URL-encoded value: `.get('foo:url')`.

[sdesai: Potential PR2 candidate. Will put this in the PR2 bucket, since it's an enhancement. For PR1, I wanted to try and get potentially risky changes/fixes in]

* **Coalesced change events.** A call to `setAttrs()` that changes multiple attributes should fire a single coalesced change event in addition to the individual change events. This is currently implemented in `Y.Model`. [Ticket #2530248](http://yuilibrary.com/projects/yui3/ticket/2530248)

[sdesai: Potential 3.6.0 PR1 candidate]

* **Better support for sub-attribute getters.** Currently, getters are required to return an entire object even when triggered by a sub-attribute retrieval like `.get('foo.bar.baz')`. This is inefficient and can be confusing.

[sdesai: Likely a 3.NEXT, since it works as designed currently. I think re-architecting it is lower priority in the bigger scheme of things, and sub-attribute handling currently goes through a clone (for real reasons) which if anything is the first thing I'd like to clean up for sub-attribute handling] 

* <strong>`set()` and `setAttr()` should support an options object.</strong> The internal `_setAttr()` method supports an `options` object as its third parameter, and mixes it into the event facade of the change event. This is very useful (it's used in `Model` and `ModelList`), but the public `set()` and `setAttrs()` methods don't currently support the `options` param.

[sdesai: Potential 3.6.0 PR1 candidate]

* **Unravel the `value` vs. `valueFn` conflict.** If an attribute is defined with a `valueFn`, but an implementer provides a value when instantiating the class, the value is ignored and the `valueFn` wins. This tends to confuse people, so we should consider making this behavior more intuitive, or at least documenting the hell out of it.

[sdesai: Potential 3.6.0 PR1 candidate - this plus lazy valueFn evaluation (this has subtle back-compat risks)]