## Using YUI Skins
The default YUI skin is the "sam" skin. It was named in honor of Sam Lind, the designer who created it. CSS rules for skins are "namespaced" under contextual selectors based on the skin name, so the selector/class for the "sam" skin is "yui3-skin-sam". Here are some YUI widgets with the Sam skin applied. 

[[img/sam_w650.png]]

You can apply a skin to the full document or just to specific regions or controls. To apply the "sam" skin to an entire page, add this class to your body element:

```html
<body class="yui3-skin-sam">
```

To apply the skin to a region or single widget, wrap just that portion of the page:

```html
<div class="yui3-skin-sam">
    <span class="yui3-tabview"></span>
</div>
```

Since the "sam" skin is the YUI default, YUI will load all the assets required for the "sam" skin and apply them to the elements that you've classed with 'yui3-skin-sam'.

## Alternate Skins

An alternate, "night" skin, became available in YUI version 3.4.0. It's optimized for touch devices. The name "night" was chosen for this skin because it was designed for a black or dark background. 

[[img/night_w650.png]]

## Different Ways to Load Skin Files

Enabling an alternate (non-sam) skin requires three steps.

### Step 1. Add the Class

Apply the "yui3-skin-night" class to the body element to affect the whole page...

```html
<body class="yui3-skin-night">
```

or to just to a region, or single widget.

```html
<div class="yui3-skin-sam">
    <span class="yui3-tabview"></span>
</div>
```

### Step 2. Load the Assets

This step is not needed for sam skin, since it's the YUI default. Skin assets include CSS files for components, as well as any images needed. There two ways to load skin assets.

#### Option A

Either statically by adding a <link> tag for each component to be skinned.

```html
<link rel="stylesheet" type="text/css" href="http://yui.yahooapis.com/3.17.2/build/tabview/assets/skins/night/tabview.css">
<link rel="stylesheet" type="text/css" href="http://yui.yahooapis.com/3.17.2/build/datatable/assets/skins/night/datatable.css">
...
```

#### Option B

...or through YUI's built-in Loader infrastructure, by adding the following object literal to the YUI().use() statement in JavaScript. This makes an alternate skin become the default skin for the entire page.

```javascript
<script>
YUI({ skin: 'night' }).use("...", function (Y) {
    ...
});
</script>
```

### Step 3. Change the Background Color

The "night" skin is designed to use a black or very dark background. Since skins do not override the background color of the page, you'll probably need to set that color in CSS on the whole page...

```css
<style>
    html {
        background-color: #000;
    }
    ...
</style>
```

...or on a part of the page...

```css
<style>
    .yui3-skin-night {
        background-color: #000;
    }
    ...
</style>
```

## Under the Hood

### CSS Modularity

Components break up their CSS definitions into modular files: one "core" file for functionality and structure essential to the component, and multiple "skin" files that define cosmetic aspects such as color, imagery and typography. When an AutoComplete widget is loaded on your page, the CSS is actually a concatenation (and minification) of AutoComplete's "core" CSS plus the specified "skin" CSS.

### Asset Resources

When assets are required for a particular skin, they can be found in the skin directory of the component's assets directory:

```
/build/fancy-widget/assets/skins/sam/polish.png
```

Resources shared across skins live in a shared assets directory:

```
/build/fancy-widget/assets/shared-asset.png
```

### Minimized, Concatenated CSS

Although skins are developed independently from core CSS files during development, we concatenate and minimize them for production use. They live in this optimized form in the top-level assets folder alongside the shared image resources:

```
/build/fancy-widget/assets/skins/sam/fancy-widget-skin.css
```

## Extending and Creating Skins

Skin creators should preserve the "core" CSS of each component and simply add look-and-feel CSS via "skin" CSS. YUI offers "sam" and "night" skins, two complementary visual treatments for the widgets in the library. We invite you to explore the assets directories, modify and/or extend the these skins or copy them as a starting point for entirely new skins.