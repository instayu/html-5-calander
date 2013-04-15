### App Framework Change History

#### Model

* Fixed: The `options` object passed to Model's `setAttrs()` method was being
  modified. Now a shallow copy of this object is now created so that the
  `_transaction` property is added to the copy and not the passed-in object.
  [#598]