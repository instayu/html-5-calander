### App Framework Change History

#### Model

* Fixed: The `options` object passed to Model's `setAttrs()` method was being
  modified. Now a shallow copy of this object is now created so that the
  `_transaction` property is added to the copy and not the passed-in object.
  [#598]

### Color Change History 
 * (Allow upper and lowercase to values for convert(). Also return original value if an invalid to value is provided. Fixes #583)

### CSS Grids Change History
* (remove previous text and images, use lorem ipsum and placeholder text instead.)

### Node Change History
* Fix node.all() to return an empty NodeList if the node was destroyed - Fixes #580 (hat tip Dallas Wheeler)

### YUI Core Change History
* (Add ability to filter log messages by threshold [andrewnicols])