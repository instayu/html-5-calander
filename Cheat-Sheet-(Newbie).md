# YUI Cheat Sheet [WIP]

## Getting Started

### Initial Setup
```html
// Load the YUI seed script
<script src="http://yui.yahooapis.com/3.10.3/build/yui/yui-min.js"></script>

//Create Y object to host YUI APIs
<script>
YUI().use(modules, function (Y) {
   ...
});
</script>
```

### Load modules
```js
YUI().use("io", "overlay", function (Y) {
   Y.io({ ... });
   var overlay = new Y.Overlay();
   ...
});
```

### Load more modules
```js
YUI().use("io", "overlay", function (Y) {
   Y.io({ ... });
   ...
   Y.use("autocomplete", function () {
       var ac = new Y.AutoComplete({ ... });
   });
   ...
});
```

### Enable debug mode

```js
YUI({ filter:"debug", combine: false }).use(...);
```

## DOM Nodes: Basics

```js
YUI().use("node", function(Y) {
    // Select
    var byElementName = Y.Node.one("body");
    var byID = Y.Node.one("#container");
    var items = Y.Node.all("#friends li.selectable");

    // Create
    var button = Y.Node.create("<button>OK</button>");
    button.appendChild(button);
    button.append("<button>Cancel</button>");

    // Change
    body.appendChild(button);
});

// Properties
button.set("id", "foo");   // button.id = "foo";
button.get("offsetWidth"); // button.offsetWidth;

// Methods
button.focus();
button.removeChild(someOtherNode);
button.remove();

// Styles
button.setStyle("backgroundColor", "#f00");
button.setStyles({...});
button.addClass("default");
button.removeClass(“hidden”);

// Classes
div.addClass("foo");
div.toggleClass("foo");
div.removeClass("foo");

// DOM Nodes: Value Adds
div.setXY([100, 200]);
div.getXY();
div.get("region"); // {top, bottom, left, right, width, height}

div.show(); div.hide();

div.load(url);

div.remove();

// Plugin to a single instance.
body.plug(Y.Plugin.ScrollInfo);

body.scrollInfo.getOffscreenNodes();
body.scrollInfo.on("scrollToBottom", function(){});

// Plugin to a single instance
div.plug(Y.Plugin.Align);

div.align.to(otherNode, "tl", "tr");
```

## DOM Events

```js
/* use "node", "event" */

div.on("click", function (e) {
  var target = e.target;

  if (e.pageX > 500) {
     e.preventDefault();
  }
});

div.once("click", function (e) {...});

div.delegate("click", function (e) {

  var target = e.target,               // Target
      container = e.container,         // Delegate container: 'div'
      currentTarget = e.currentTarget; // Delegate target: '.contact'

}, ".contact");

// Don't need any target/ancestor filtering
div.on("mouseenter", function (e) {...});
div.on("mouseleave", function (e) {...});
div.on("clickoutside", function (e) {...});

// Gestures - Abstraction across touch/mouse/ms-pointer events.
div.on("flick", function (e) {...}, {minVelocity: ..., minDistance: ...});
div.on("tap", function (e) {...});

div.on("gesturemovestart", function (e) {...});
   div.on("gesturemove", function (e) {...});
   div.on("gesturemoveend", function (e) {...});

// Input
input.on("valuechange", function (e) {...});
input.on("key", function (e) {...}, "enter");
```

## Getting Data

### Getting Data: YQL

```js
/* use "yql" */

// Works everywhere, including nodejs and inside win8 apps

Y.YQL("select * from weather.forecast where location=90210", function (o) {

  // Use the YQL console, to figure out where to look in 'o'
  myDiv.setHTML(o.query.results.channel.item.description);

});
```

###Getting Data: JSONP

```js
/* use "jsonp" */

// Use only with trusted data
Y.jsonp("https://api.github.com/users/yui?callback={callback}", function (o) {

   // Use the service docs to figure out where to look
   myDiv.setHTML(o.data);

});
```

### Getting Data: IO

```js
/* use "io" */

Y.io("http://samedomain/service?foo=bar", {
   headers: {
      'Content-Type': 'application/json'
   },
   on: {
      start: function () {...},
      failure: function () {...},
      success: function (o) {
         myDiv.setHTML(o.responseText); // or o.responseXML;
      }
   }
});
```

### Getting Data: Parsing Raw Strings

```js
/* use "json" */

var arr = Y.JSON.parse("[{name:'Abc', rank:1}, ...]");

/* use "datatype-xml" */

var xmlDoc = Y.XML.parse(
  "<root><item><name>Abc</name><rank>1</rank></item>...</root>");
```

## CSS

Pull in all the styles to make your page look pretty. This includes Base, Grids, Buttons, Forms, Menus, and Tables.

```html
<link rel="stylesheet" href="http://yui.yahooapis.com/pure/0.0.2/pure-min.css">
```

Form Styling: 

```html
<form class="pure-form">...</form>
```

Other Classes:
* `.pure-form-aligned`
* `.pure-form-stacked`
* `.pure-input-rounded`
* `.pure-checkbox`
* `.pure-radio`

Forms can also be used with grids

```html
<a class="pure-button pure-button-selected">Selected</a>​
<div class="pure-menu pure-menu-open pure-menu-horizontal">
    <ul>
    ...
    </ul>
</div>

<div class=​"yui3-popover left">...​</div>​

<div class=”pure-g-r”>
   <div class="yui3-u-1-3">...</div>
   <div class="yui3-u-1-3">...</div>
   <div class="yui3-u-1-3">...</div>
</div>
```

## JS Effects

### JS Effects: Transition

```js
/* use "transition" */

mydiv.transition({
    easing: 'ease-out',
    duration: 0.75, // seconds
    width: '10px',
    height: '10px'
}, function () {     // callback
    this.remove();
});
```

### JS Effects: Anim

```js
/* use "anim" */

new Y.Anim({
    node: demoA,
    duration: 1.5,
    to : {
        curve: [[120, 100], [250, 230], [350, 400]]
    }
}).run();
```

### JS Effects: Graphics

```js
/* use "graphics" */

var mygraphic = new Y.Graphic({ render:"#mygraphiccontainer" }),

    myrect = mygraphic.addShape({
        type: "rect",
        width: 300,
        height: 200,
        fill: {
            color: "#0000ff"
        },
        stroke: {
            weight: 2,
            color: "#ff0000"
        },
        x: 50,
        y: 100
    });
```

## Apps

### Apps: Single Page Apps

```js
/* use "app", "handlebars" */

var app = new Y.App({

   views: {
      home: {
         type: HomeView
      },
      users: {
         type: UsersView
      },
      user: {
         type: UserView,
            parent: 'users'
         }
      }
   },

   serverRouting: false,
   transitions: true

});
```

### Apps: Views

Handlebars Template
```xml
<script id="user-template" type="text/x-handlebars-template">
    <h1>User Form</h1>
    <form>
        <label>First Name: <input value="{{firstname}}"></label>
        <label>Last Name:  <input value="{{lastname}}"></label>
    </form>
</script>
```

View Instance
```js
var UserView = Y.Base.create("user", Y.View, [], {

      template: Y.Handlebars.compile(Y.one('#user-template').getHTML()),

      render: function () {
         var html = this.template({firstname: "Satyen", lastname: "Desai"});
         this.get('container').setHTML(html);

         return this;
      }
   });
```

### Apps: App Flow

```js
// add route (for history, back-button)
app.route("/users", navigateToUsers);

// navigate to route (updating history)
app.navigate("/users");

// show view without updating history
app.showView("users");
```

## Widgets

```js
/* use "slider" */

var slider = new Y.Slider({
  min: -200,
  max: 200,
  value: 100,
  render: true
});

slider.after("valueChange", function (e) {
  if (e.prevVal > 0 && e.newVal <= 0) {
     // Moved backwards across the 0 value
  }
});
```
