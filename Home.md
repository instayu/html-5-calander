Welcome to the YUI development wiki!

YUI's official [user guides](http://yuilibrary.com/yui/docs/guides/) and [API docs](http://yuilibrary.com/yui/docs/api/) are hosted on [yuilibrary.com](http://yuilibrary.com/), but this wiki is where we maintain living documents that are relevant to people who are interested in contributing code or feedback to YUI.

## Active Development on YUI

* [[Development Schedule]]
* [[Ongoing Development Discussions]]

## Next Release

The focus for the next release is on adding IE 10 to [YUI's target environments](http://yuilibrary.com/yui/environments/). YUI's unit tests already fare really well in IE 10's standard desktop mode, but in Windows 8 there are multiple runtime environments (generally more restrictive) in which we want to make sure YUI is supported.

Scheduled stable release date: **[[October 16, 2012|Development Schedule]].**

### Windows 8 JavaScript Runtimes

##### **Desktop:** IE 10 "Desktop" Mode
* UA: `"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0; .NET4.0E; .NET4.0C)"`
* IE 10 Browser that is launchable from Win8's "Desktop" Mode, which is the non-default Win8 GUI.

##### **Metro:** IE 10 "Metro" Mode
* UA: `"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Win64; x64; Trident/6.0; .NET4.0E; .NET4.0C)"`
* IE 10 Browser that is launchable from Win8's "Metro" Mode, which is the default (even on PCs) tablet-like GUI.
* No support for plugins (i.e., no ActiveX, no Flash, no custom search, no Silverlight, etc)

##### **Webview:** Webview Within Native Metro App
* UA: `"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0; .NET4.0E; .NET4.0C)"`
* Locked down hybrid app
* No JS API to device APIs (e.g., camera, etc)
* No JS in markup (i.e., safe innerHTML only)

##### **WinJS:** WinJS Native Metro App
* Locked down native-only app written within the WinJS JS runtime
* All assets must be on device (no calls to remote CSS/JS/IMG)
* JS APIs to device functionality (e.g., camera, etc)
* No JS in markup (i.e., safe innerHTML only)
* No JSONP or XHR: WinJS.xhr only
* iFrame support is unpredictable
* Documented differences to expect in this environment: http://msdn.microsoft.com/en-us/library/windows/apps/hh700404.aspx

## Current Release: 3.7.2

* YUI 3.7.2 TODO
* YUI 3.7.1 was simply a rebuild of 3.7.0 to fix encoding issues.
* [[YUI 3.7.0 Change History Rollup]]

## Past Releases

* [[YUI 3.6.0 Change History Rollup]]
* [[YUI 3.5.1 Change History Rollup]]

## Future

* [[DataTable Roadmap]]
* [[Attribute Wishlist]]