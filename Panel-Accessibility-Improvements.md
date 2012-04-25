# Panel Accessibility Improvements

## Leverage ARIA
Dialogs are likely to be one of the primary use cases for Panel, and there are ARIA attributes that will make these dialogs more accessible to users of screen readers. Those are:

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

## Managing Focus
When a Panel is made visible, focus should move into the Panel—ideally to the control that represents the first or default action. This will ensure users of screen readers that the context has changed and they are now inside the Panel. Without the change in focus, users of screen readers will not be aware that the Panel is visible.

### Setting Focus
Currently when a Panel is made visible focus is only moved into the Panel when either the Widget-Modality extension is in use, or the developer has specified a default button. Otherwise, focus remains where is was previous to the Panel's display. To fix this, Panel should set focus to some element inside it (defined by a new configuration attribute), or default to the bounding box.


### Restoring Focus
If the display of a Panel is canceled, by the user hitting the "X" (close) button or by pressing Esc, focus should be restored to the element that had focus prior to the Panel's display. This is easily accomplished using the document's "activeElement" property. "activeElement" returns a reference to the currently focused element. When the Panel is made visible it should capture a reference to the current value of document.activeElement before it sets focus inside the panel. When the Panel hides, it can use that reference to restore focus the node that had focus prior to the Panel being visible.

Here's an example of how this could be implemented in Panel:
```js 
Y.Panel = Y.Base.create('panel', Y.Widget, [
    Y.WidgetPosition,
    Y.WidgetStdMod,
    Y.WidgetAutohide,
    Y.WidgetButtons,
    Y.WidgetModality,
    Y.WidgetPositionAlign,
    Y.WidgetPositionConstrain,
    Y.WidgetStack
], {
    BUTTONS: {
        close: {
            label  : 'Close',
            action : 'hide',
            section: 'header',

            // Uses `type="button"` so the button's default action can still
            // occur but it won't cause things like a form to submit.
            template  : '<button type="button" />',
            classNames: getClassName('button', 'close')
        }
    },

    _restoreFocus: function (node) {
        node.focus();
    },
    
    _onPanelVisibleChange: function (e) {
        var activeElement = Y.one("doc").get("activeElement"),
            closeBtn = Y.one(".yui3-button-close");
        
        if (e.newVal) {
        
            if (activeElement && activeElement.get("nodeName").toLowerCase() !== "body") {
                this.get("boundingBox").once("keydown", function (e) {
                    if (e.keyCode === 27) {
                        this._restoreFocus(activeElement);
                    }
                }, this);
            }
            
            if (closeBtn) {
                closeBtn.once("click", function () {
                    this._restoreFocus(activeElement);
                }, this);
            }
        
        }
    }, 
    
    bindUI: function () {
        this.on("visibleChange", this._onPanelVisibleChange);
    }
    
}, {
    ATTRS: {
        buttons: {
            value: ['close']
        }
    }
});
```

#### Implementing A "Cancel" Event
Building on the concept of restoring focus when the Panel is cancelled by the user: Panel could implement a "cancel" event. This event would be fired in response to user actions like pressing Esc or clicking the "x" (close) button. The default behavior for the "cancel" event would be to restore focus to the element that had focus prior to the Panel's display. Here's an example:

```js
Y.Panel = Y.Base.create('panel', Y.Widget, [
    Y.WidgetPosition,
    Y.WidgetStdMod,
    Y.WidgetAutohide,
    Y.WidgetButtons,
    Y.WidgetModality,
    Y.WidgetPositionAlign,
    Y.WidgetPositionConstrain,
    Y.WidgetStack
], {
    BUTTONS: {
        close: {
            label  : 'Close',
            action : 'hide',
            section: 'header',

            // Uses `type="button"` so the button's default action can still
            // occur but it won't cause things like a form to submit.
            template  : '<button type="button" />',
            classNames: getClassName('button', 'close')
        }
    },

    _restoreFocus: function (e) {
        var activeEl = e.activeElement;
        if (activeEl) {
            activeEl.focus();
        }
    },
    
    _onPanelVisibleChange: function (e) {
        var activeElement = Y.one("doc").get("activeElement"),
            closeBtn = Y.one(".yui3-button-close"),
            data;
        
        if (e.newVal) {

            if (activeElement && activeElement.get("nodeName").toLowerCase() !== "body") {
                data = { activeElement: activeElement };    
            }

            this.get("boundingBox").once("keydown", function (e) {
                if (e.keyCode === 27) {
                    this.fire("cancel", data);
                }
            }, this);

            
            if (closeBtn) {
                closeBtn.once("click", function () {
                    this.fire("cancel", data);
                }, this);
            }
        
        }
    }, 
    
    initializer: function () {
        this.publish("cancel", {
            defaultFn: this._restoreFocus
        });
    },
    
    bindUI: function () {
        this.on("visibleChange", this._onPanelVisibleChange);
    }
    
}, {
    ATTRS: {
        buttons: {
            value: ['close']
        }
    }
});
```

## Modality

The user can use the Tab key to move focus from the Panel into the browser's location bar. Typically modal controls restrict the Tab flow to the scope of the control. It is worth considering this behavior over the current behavior.

This could be implemented by having the Widget-Modality extension append an empty, but focusable \<div\>s as the last child of the bounding box. If that last node gets focus, the event handler would forward focus back to the bounding box.

```html
<div class="yui3-panel" tabindex="0">
  <div class="yui3-panel-content">
    <div class="yui3-widget-hd"></div>
    <div class="yui3-widget-bd"></div>
    <div class="yui3-widget-ft"></div>        
  </div>
  <div tabindex="0"></div>
</div>
```

