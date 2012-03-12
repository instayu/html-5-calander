
With more and more application logic moving to the client, and with YUI becoming more popular on the server, it's increasingly important to design APIs that handle user input safely. Currently, YUI modules that store user input in attributes must do one of two things: either escape user strings before setting an attribute, or escape them manually before using them.

Escaping automatically before storing the value is safest, but also inconvenient if you sometimes need the unescaped value, since you must then store two versions (probably in two different attributes). This can lead to API clutter and confusion. Escaping manually before use avoids API clutter but increases the likelihood of mistakes, and also clutters up the codebase in general. It significantly increases the chances that another developer who is unaware of the need to escape the value will inadvertently introduce a security vulnerability.

## Proposal

Attribute should provide a consistent, pluggable API for retrieving a filtered string value. Internally, string attributes would be stored as raw strings, and would be filtered on demand using the specified filter when the attribute is retrieved. This avoids the need for module developers to write custom getter functions or store both filtered and unfiltered values, and allows for flexible and safe usage in a variety of scenarios.

Filters should be pluggable via a static API on `Y.Attribute`. This will allow the `escape` module to provide a set of default filters, and custom modules can provide their own filters to meet custom needs.

### Getting and Setting Values

Setting a value continues to work the same as it does today:

```js
klass.set('username', '<b>joe</b>'); // stores "<b>joe</b>" as the raw attr value
```

Getting a value also works the same:

```js
klass.get('username'); // => "<b>joe</b>"
```

To get a filtered version of a value, append a colon to the attribute name, followed by the name of the desired filter:

```js
klass.get('username:html'); // => "&lt;b&gt;joe&lt;/b&gt;"
klass.get('username:url');  // => "%3Cb%3Ejoe%3C%2Fb%3E"
```

Internally, `get()` or its underyling implemenation should take the following steps:

1. If the first argument to `get()` matches the regex `/^([^:]+):([\w-]+)$/`, then

    a. Let `attrName` be the value of the first subpattern match.

    b. Let `filterName` be the value of the second subpattern match.

    c. If `attrName` refers to a nonexistent attribute, return `undefined`.

    d. If `filterName` refers to a nonexistent filter, return `undefined`.

    e. Let `rawValue` be the raw value of the attribute named by `attrName`.

    f. Let `stringValue` be the result of calling `rawValue.toString()`.

    g. Execute the filter function, passing `stringValue` as the only argument.

    h. Return the filter function's return value.

2. Else, treat the entire argument as the attribute name and return the raw value of the matching attribute, or `undefined` if it doesn't exist.

### Registering a Filter

Filters are registered statically on `Y.Attribute`. Once registered, a filter is available for use on any class instance that uses Attribute, even if it was instantiated before the filter was registered.

To register a filter:

```js
// Registers a new "html" filter unless one already exists.
Y.Attribute.addFilter('html', Y.Escape.html);

// Arbitrary filter.
Y.Attribute.addFilter('disemvowel', function (value) {
    return value.replace(/[aeiou]+/g, '');
});
```

Internally, Attribute should store the filter function in a static object hash, with the name as the key.

If `addFilter()` is called with the name of a filter that already exists, it should log an error and refuse to overwrite the existing filter unless the third argument is truthy:

```js
// Registers an "html" filter, overwriting any pre-existing filter.
Y.Attribute.addFilter('html', Y.Escape.html, true);
```

When `get()` is called, Attribute should look up the named filter (if any) in the static hash of registered filters and call it, passing in the raw attribute value. The return value of the filter function should be returned from `get()`.

### Caching

To improve performance, Attribute could cache filtered values internally, clearing the cached value whenever an attribute's raw value is updated.

### Default Filters

A new attribute config property named `filter` could allow module developers to specify a default filter to be used for an attribute. For example, I could define an attribute that should always be filtered as HTML by default:

```js
// ...
ATTRS: {
    username: {
        filter: 'html'
    }
}
// ...
```

This would cause `get('username')` to run the "html" filter. I could still specify another filter if desired, or `get('username:raw')` to get the raw, unfiltered value.
