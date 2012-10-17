The following are the four different IE 10 runtime environments that are present in Windows 8.

## IE Start Screen Mode (Formerly known as Metro)

The runtime environment of the Internet Explorer app which is present in the Windows 8 Start screen mode, which is the default GUI.

* UA: `"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Win64; x64; Trident/6.0; .NET4.0E; .NET4.0C)"`
* More restrictive than IE Desktop.
* Limited and restricted support for plugins (i.e., no ActiveX, Flash, Silverlight, etc.)

## IE Desktop Mode

The runtime environment of the Internet Explorer app which is present in the Windows 8 Desktop mode, which is the transitional Windows interface.

* UA: `"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0; .NET4.0E; .NET4.0C)"`

## WebView (within Native Windows 8 App)

WebViews are useful for building hybrid apps that, for example, combine a native C# Windows app with web-based content rendering.

While testing YUI in the IE 10 WebView runtime, we noticed the following restrictions:

* Locked down compared to Internet Explorer
* No JavaScript-to-device APIs (e.g., camera, clipboard, geolocation, etc.)
* Restricted innerHTML (e.g., no JavaScript in dynamic markup.)

Microsoft describes the [WebView restrictions](http://msdn.microsoft.com/en-us/library/windows/apps/windows.ui.xaml.controls.webview) in detail on its MSDN website.

## Native Windows Runtime (Windows Store apps)

The native Windows Runtime allows developers to create Windows 8 apps using JavaScript and other HTML5 technologies, and these apps are distributed through the Windows Store.

The native Windows Runtime is both a restricted IE 10 runtime, and is extended via the native [`Windows`](http://msdn.microsoft.com/en-us/library/windows/apps/br211377.aspx) and [`WinJS`](http://msdn.microsoft.com/en-us/library/windows/apps/br229773.aspx) APIs. While testing YUI in the native Windows Runtime, we noticed the following differences:

* Environment is only available to native Windows 8 apps.
* All assets must be on device (i.e., remote JavaScript, CSS, etc. is not allowed.)
  * No support for JSONP.
* Extended with both Windows and WinJS APIs, allowing apps to use device functionality (e.g., camera, clipboard, geolocation, etc.)
* Restricted innerHTML (e.g., no JavaScript in dynamic markup.)
* Support for CORS in XMLHttpRequest.
  * WinJS.xhr is a wrapper which uses promises.
* IFrame support is unpredictable.

Microsoft’s MSDN website has a [complete list of HTML and DOM API changes](http://msdn.microsoft.com/en-us/library/windows/apps/hh700404.aspx) for Windows Store apps which use JavaScript.