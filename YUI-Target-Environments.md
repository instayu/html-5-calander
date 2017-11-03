
<table class="environments">
    <tbody><tr>
        <th align="left">Internet Explorer</th>
        <td align="center">6.0</td>
        <td align="center">7.0</td>
        <td align="center">8.0</td>
        <td align="center">9.0</td>
        <td align="center">10.0</td>
        <td align="center">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11.0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
    </tr>
    <tr>
        <th align="left">Chrome †</th>
        <td colspan="6" align="center">Latest stable</td>
    </tr>
    <tr>
        <th align="left">Firefox †</th>
        <td colspan="6" align="center">Latest stable</td>
    </tr>
    <tr>
        <th align="left">Safari</th>
        <td align="center">iOS 5.†</td>
        <td align="center">iOS 6.†</td>
        <td align="center">iOS 7.†</td>
        <td align="center">Safari 6.1 <br> (OS X 10.8)</td>
        <td colspan="2" align="center">Safari 7.† <br> (OS X 10.9)</td>
    </tr>
    <tr>
        <th align="left">Android</th>
        <td align="center">2.3.†</td>
        <td colspan="5" align="center">4.†</td>
    </tr>
    <tr>
        <th align="left">Node.js*</th>
        <td align="center">0.8.†</td>
        <td colspan="5" align="center">0.10.†</td>
    </tr>
    <tr>
        <th align="left">Windows (Native)</th>
        <td colspan="6" align="center">Windows 8 Apps (WinJS &gt;= 2.†)</td>
    </tr>
</tbody></table>

### Notes:
* The dagger symbol (as in "iOS 6.†") indicates that the most-current non-beta version.
* Certain modules have native Node.js support, while others are DOM dependent.

## Module Support in Node.js

YUI does not come with server-side DOM support out of the box, in fact we recommend against running a DOM on the server for performance reasons. This means that only a subset of YUI modules will run natively within a Node.js environment, essentially any modules which do not depend on the DOM APIs in the browser. If you're inclined to run a DOM on the server, refer to [this example](http://yuilibrary.com/yui/docs/yui/nodejs-dom.html).

YUI's modular architecture means components of the library can be designed as multiple modules, allowing for more code and functionality to be shared between the browser _and_ server environments. A great example of this in the [IO Utility](http://yuilibrary.com/yui/docs/io/), where the `io-base` module is the core logic which runs in all environments, and the `io-form` module only runs in browser environments because it works with HTML `<form>` elements in the DOM.
