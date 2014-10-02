### 1. Copy and paste

```html
// Put the YUI seed file on your page.
<script src="http://yui.yahooapis.com/3.18.0/build/yui/yui-min.js"></script>
```

The YUI seed file is an ultra-small bit of JavaScript that enables you to load any YUI component on your page.

### 2. Start using YUI!

```html
<script>
// Create a YUI sandbox on your page.
YUI().use('node', 'event', function (Y) {
    // The Node and Event modules are loaded and ready to use.
    // Your code goes here!
});
</script>
```

Create a YUI instance, called a "sandbox", to use any YUI component. Each YUI sandbox has its own instance of YUI (that's the Y parameter that gets passed to the callback function) and its own set of activated modules, so it won't conflict with other sandboxes on the same page. Any variables you declare inside your sandbox will only be available in that sandbox and won't pollute the global scope.

When creating your YUI sandbox, specify the modules you'd like to use. In this example, we're using the [node](http://yuilibrary.com/yui/docs/node/) and [event](http://yuilibrary.com/yui/docs/event/) modules. Then, from inside the sandbox, you can access the Node and Event APIs via the Y instance.

YUI will manage all dependency calculations for the modules you need and load the JavaScript onto your page in a single, combined request. Your code inside the sandbox will execute as soon as all the requested YUI modules are loaded onto the page.

» Learn more: [See All YUI Components](http://yuilibrary.com/yui/docs/guides/)

## Work with the DOM
The [Node](http://yuilibrary.com/yui/docs/node/) component makes it quick and convenient to access, create, and manipulate DOM elements. Node APIs accept element references or selector queries for accessing DOM elements.

```javascript
YUI().use('node', function (Y) {
    // Access DOM nodes.
    var oneElementById     = Y.one('#foo'),
        oneElementByName   = Y.one('body'),
        allElementsByClass = Y.all('.bar');

    // Create DOM nodes.
    var contentNode = Y.Node.create('<div>'),
        listNode    = Y.Node.create('<ul>'),
        footerNode  = Y.Node.create('<footer>');

    contentNode.setHTML('<p>Node makes it easy to add content.</p>');
    listNode.insert('<li>Buy milk</li>');
    footerNode.prepend('<h2>Footer Content</h2>');

    // Manipulate DOM nodes.
    Y.all('.important').addClass('highlight');

    Y.one('#close-button').on('click', function () {
        contentNode.hide();
    });
});
```

» Learn more: [The Node Component](http://yuilibrary.com/yui/docs/node/)

## Create UI Effects
The [Transition](http://yuilibrary.com/yui/docs/transition/) component makes it easy to create CSS-based transitions that add polish and finesse to your user interactions.

```javascript
YUI().use('transition', function (Y) {
    // Fade away.
    Y.one('#fademe').transition({
        duration: 1, // seconds
        opacity : 0
    });

    // Shrink to nothing.
    Y.one('#shrinkme').transition({
        duration: 1, // seconds
        width   : 0,
        height  : 0
    });
});
```

» Learn more: [The Transition Component](http://yuilibrary.com/yui/docs/transition/)

## Load Content with Ajax
The [Node.load()](http://yuilibrary.com/yui/docs/api/classes/Node.html#method_load) method (provided by the [node-load](http://yuilibrary.com/yui/docs/api/modules/node-load.html) module) makes it easy to populate your web page with dynamic content at runtime.

```javascript
YUI().use('node-load', function (Y) {
    // Replace the contents of the #content node with content.html.
    Y.one('#content').load('content.html');
});
```

» Learn more: [The Node.load() Method](http://yuilibrary.com/yui/docs/api/classes/Node.html#method_load)
 
