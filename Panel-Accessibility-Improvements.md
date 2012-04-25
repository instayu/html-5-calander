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

Going forward, a Dialog and Alert subclass could be written that sets the relevant ARIA attributes using the above config.





