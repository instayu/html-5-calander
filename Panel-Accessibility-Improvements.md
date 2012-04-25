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

