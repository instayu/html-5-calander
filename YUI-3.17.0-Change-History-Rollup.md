### Calendar Change History


* [#1752][]: Y.Calendar.selectDates fails when passed the maximumDate with minutes/seconds (@mairatma)

[#1752]: https://github.com/yui/yui3/pull/1752

### DOM Change History

* [#1709][]: Move out of color-base module (@okuryu)

[#1709]: https://github.com/yui/yui3/pull/1709

### YUI Loader Change History

* Add support for optional dependencies. These dependencies are conditionally
  loaded but each dependency is responsible for determining the result of the
  test, the opposite of `condition`. Example:

```js
  YUI({
    modules: {
      foo: {
        test: function (Y) {
          return true;
        }
      },
      bar: {
        optionalRequires: ['foo']
      }
    }
  }).use('bar', ...);
```

### MenuNav Change History

* Correct check for IE UserAgent [Andrew Nicols]

### Drag And Drop Change History

* Check whether the mousedown event belonged to a valid drop target before preventing default [Andrew Nicols]


### Rich Text Editor Change History

* [Editor]: Increase specificity of when to set cursor.
* [Editor]: Check for the existence of `node` before removing it.

### Node Change History

* [Node]: Add `invalid` to event whitelist.

### App Change History
 
* [ModelSync.Local] Stringify hash before saving.

### Tree Change History

* Fixed: Moving a node to another tree fails when that node has children.
  ([#1689][]: @rgrove)

[#1689]: https://github.com/yui/yui3/issues/1689