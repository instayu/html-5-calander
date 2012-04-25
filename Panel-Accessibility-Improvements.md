# Panel Accessibility Improvements

## Leverage ARIA
Panel is most likely going to be used to created dialogs, and there are ARIA attributes that will make these dialogs more accessible to users of screen readers. Those are:

* [dialog](http://www.w3.org/TR/wai-aria/complete#dialog)
* [alertdialog](http://www.w3.org/TR/wai-aria/complete#alertdialog)
* [aria-hiden](http://www.w3.org/TR/wai-aria/complete#aria-hidden)
* [aria-labelledby](http://www.w3.org/TR/wai-aria/complete#aria-labelledby)
* [aria-describedby](http://www.w3.org/TR/wai-aria/complete#aria-describedby)

Example usage of the above attributes based on the current YUI Panel markup and standard module format:

### ARIA Dialog Example
```html
<div class="yui3-panel" role="dialog" aria-labelledby="header" aria-hidden="true">
  <div class="yui3-panel-content">
    <div id="header" class="yui3-widget-hd">Add A New Product</div>
    <div class="yui3-widget-bd">...</div>
  </div>  
</div>
```

### ARIA Alert Dialog Example
```html
<div class="yui3-panel" role="alertdialog" aria-labelledby="header" aria-describedby="msg" aria-hidden="true">
  <div class="yui3-panel-content">
    <div id="header" class="yui3-widget-hd">Alert</div>
    <div id="msg" class="yui3-widget-bd">Are you sure you want to submit this form?</div>
    <div class="yui3-widget-ft">
      <button type="button">OK</button>
      <button type="button">Cancel</button>
    </div>
  </div>  
</div>
```

### Applying ARIA Attributes
Since there are two possible ARIA roles ("dialog" and "alertdialog") and the "aria-describedby" attribute is only used with the "alertdialog" role, it might make sense for Panel to manage the application of the ARIA attributes via a configuration attribute.

For example, the following example config allows the developer to define what ARIA role to use, as well as the elements to receive the "aria-lablledby" and "aria-describedby" attributes. (Note: It is likely that the "dialog" or "alertdialog" role will always be applied to the bounding box, so that is why this config example doesn't allow the developer to specify the element to which the "role" attribute should be applied.)

```js
var Panel = new Y.Panel({
    aria: {
        'role': 'dialog',
        'aria-labelledby' : 'yui3-widget-hd',
        'aria-describedby' : 'yui3-widget-bd'
    }
});
```

Going forward, Dialog and Alert subclasses could be written that set the relevant ARIA attributes using the above config.

### Hidden State
ARIA also provides the "aria-hidden" attribute for indicating the hidden state of a widget. This could be incorporated into Panel in two ways:

1. The Widget base class should toggle "aria-hidden" to the correct value in response to the "visible" attribute changing:
```js
_uiSetVisible: function(val) {
    var bb = this.get(BOUNDING_BOX);
    bb.toggleClass(this.getClassName(HIDDEN), !val);
    bb.set("aria-hidden", !val);    
} 
```

2. The Widget-Modality extension should toggle "aria-hidden" on the \<body\> to prevent users of screen readers from being able to move outside of the modal widget. When a modal widget is made visible:

* "aria-hidden" should be set to "true" on the \<body\> 
* "aria-hidden" should be set to "false" on the widget's bounding box

Here's an example of what the markup would look like for a modal dialog:

```html
<body aria-hidden="true">

<div class="yui3-panel" role="alertdialog" aria-labelledby="header" aria-describedby="msg" aria-hidden="false">
  <div class="yui3-panel-content">
    <div id="header" class="yui3-widget-hd">Alert</div>
    <div id="msg" class="yui3-widget-bd">Are you sure you want to submit this form?</div>
    <div class="yui3-widget-ft">
      <button type="button">OK</button>
      <button type="button">Cancel</button>
    </div>
  </div>  
</div>

</body>
```


