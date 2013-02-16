( posted also to the Group Forum: https://groups.google.com/forum/?fromgroups=#!topic/yui-contrib/yKHiYIQTkJE )

I wanted to open the floor for a discussion about an iconic font resource for YUI3. 

This would be helpful for skinning and could be updated as needed to support any and all of our monochromatic icon wants in components such as menus, sortable items, resizer, and  paginator.

Ideally we would be able to support the following browsers:
TrueType Fonts for Firefox 3.5+ , Opera 10+, Safari 3.1+, Chrome 4.0.249.4+
EOT fonts for Internet Explorer 4+
WOFF fonts for Firefox 3.6+, Internet Explorer 9+, Chrome 5+
SVG fonts for legacy iOS

If you are unfamiliar with custom web fonts, you can get some information about them with a quick search, but here's the general syntax

In the CSS:
```css
@font-face {
    font-family: 'YUIWebFont';
    src: url('yui-web-font.eot'); /* IE9 Compat Modes */
    src: url('yui-web-font.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
        url('yui-web-font.woff') format('woff'), /* Modern Browsers */
        url('yui-web-font.ttf')  format('truetype'), /* Safari, Android, iOS */
        url('yui-web-font.svg#svgFontName') format('svg'); /* Legacy iOS */
}
```

To use it:
```css
body {
    font-family: 'YUIWebFont', Fallback, sans-serif;
}
```

(src: http://css-tricks.com/snippets/css/using-font-face/)

Would like to get some thoughts on the idea and hopefully get this off the ground soon if there aren't any initial issues to overcome.

Tony