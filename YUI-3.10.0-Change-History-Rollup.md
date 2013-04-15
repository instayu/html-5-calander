### App Framework Change History

#### Model

* Fixed: The `options` object passed to Model's `setAttrs()` method was being
  modified. Now a shallow copy of this object is now created so that the
  `_transaction` property is added to the copy and not the passed-in object.
  [#598]

### Attribute Change History

* Significant performance improvements in common Attribute operations.

  For example, on Chrome:

      `get()` is 4 times faster
      `set()` is 3 times faster

  Major performance related changes are listed below.

  Commit messages have detailed descriptions of incremental changes, and the
  benefits introduced.

* We retrieve and pass the internally stored attribute configuration in State
  by reference in a lot more places, across methods, results in less function
  hops, and removing the need for each method to go and ask for the configuration.

* Avoid the delete operator for transient configuration properties, and just set
  to null or other falsey values as appropriate.

* Store final attribute config in State by reference, as opposed to merging
  since it's isolated already higher up in the call stack.

### AutoComplete Change History
* (Add italian language files to the components. [albertosantini])

### Base Change History

* Significant performance improvements in common Base/BaseCore operations.

  For example, on Chrome:

    `new BaseCore()` is 3 times faster
    `BaseCore set()` is 3 times faster
    `BaseCore get()` is 5 times faster

  In addition to the above basic `BaseCore` numbers, improvements in CustomEvent
  performance, result in the following improvements for `Base`

    `new Base()` is 4 times faster
    `Base set()` is 4 times faster
    `Base get()` is 5 times faster

  Major performance related changes are listed in the list of updates below.

  Commit messages have detailed descriptions of incremental changes, and the
  benefits introduced.

* [!] The result of static `ATTRS` aggregation is now cached during the creation of
  the first instance of a given "class", and the cached results are reused for
  subsequent instances.

  This provides significant performance benefits, but has the potential to introduce
  a backwards compatibility issue in the hopefully rare circumstance that you're
  modifying the static ATTRS collection directly, after the first instance is created.

  [!] If you are modifying static `ATTRS` collection directly after an instance is
  created (e.g. if an optional module comes in and updates the collection dynamically),
  you will need to change the implementation to use the static `Y.Base.modifyAttrs()`
  or `Y.BaseCore.modifyAttrs()` method, so we can mark the cached aggregation 
  dirty, and recompute it.

      `Y.Base.modifyAttrs(MyClass, {..changes to merge..})`

  `Base.create` and `Base.mix` will take care of this internally, so you only need 
  to use the above methods if your own code is touching the ATTRS object on a class.
  Additionaly, `Base.create` and `Base.mix` will add the `modifyAttrs` to your created
  class, so you can also call it directly on the class. e.g. 

      `MyCreatedClass.modifyAttrs({..changes to merge..})`

### Color Change History 
 * (Allow upper and lowercase to values for convert(). Also return original value if an invalid to value is provided. Fixes #583)

### CSS Grids Change History
* (remove previous text and images, use lorem ipsum and placeholder text instead.)

### Node Change History
* Fix node.all() to return an empty NodeList if the node was destroyed - Fixes #580 (hat tip Dallas Wheeler)

### YUI Core Change History
* (Add ability to filter log messages by threshold [andrewnicols])