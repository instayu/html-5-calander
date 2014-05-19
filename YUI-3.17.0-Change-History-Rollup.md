### App Framework Change History
 
* [ModelSync.Local] Stringify hash before saving.

### Calendar Change History

* [#1752][]: Y.Calendar.selectDates fails when passed the maximumDate with minutes/seconds (@mairatma)
* [#1749][]: Fix left/right margin issues with dual-panel calendars
* [#1724][]: Fix issues with `calendarnavigation` month :hover and disabled styles

[#1752]: https://github.com/yui/yui3/pull/1752
[#1749]: https://github.com/yui/yui3/pull/1749
[#1724]: https://github.com/yui/yui3/pull/1724

### Drag And Drop Change History

* [#1778][] Filter mousedown events to check that they belong to a valid drop target. (Andrew Nicols)

[#1778]: https://github.com/yui/yui3/pull/1778

### DOM Change History

* [#1709][]: Move out of color-base module (@okuryu)

[#1709]: https://github.com/yui/yui3/pull/1709

### Rich Text Editor Change History

* [Editor]: Increase specificity of when to set cursor.
* [Editor]: Check for the existence of `node` before removing it.

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

* [#1772][] Correct check for IE UserAgent to make sure that the browser is IE. (Andrew Nicols)

[#1772]: https://github.com/yui/yui3/pull/1772

### Node Change History

* [Node]: Add `invalid` to event whitelist.

### Tree Change History

* Fixed: Moving a node to another tree fails when that node has children.
  ([#1689][]: @rgrove)

[#1689]: https://github.com/yui/yui3/issues/1689