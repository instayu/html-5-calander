The following are the different JavaScript runtime environments that are present in Window 8.

## **Desktop:** IE 10 "Desktop" Mode
* UA: `"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0; .NET4.0E; .NET4.0C)"`
* IE 10 Browser that is launchable from Win8's "Desktop" Mode, which is the non-default Win8 GUI.

## **Metro:** IE 10 "Metro" Mode
* UA: `"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Win64; x64; Trident/6.0; .NET4.0E; .NET4.0C)"`
* IE 10 Browser that is launchable from Win8's "Metro" Mode, which is the default (even on PCs) tablet-like GUI.
* No support for plugins (i.e., no ActiveX, no Flash, no custom search, no Silverlight, etc)

## **Webview:** Webview Within Native Metro App
* UA: `"Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0; .NET4.0E; .NET4.0C)"`
* Locked down hybrid app
* No JS API to device APIs (e.g., camera, etc)
* No JS in markup (i.e., safe innerHTML only)

## **WinJS:** WinJS Native Metro App
* Locked down native-only app written within the WinJS JS runtime
* All assets must be on device (no calls to remote CSS/JS/IMG)
* JS APIs to device functionality (e.g., camera, etc)
* No JS in markup (i.e., safe innerHTML only)
* No JSONP or XHR: WinJS.xhr only
* iFrame support is unpredictable
* Documented differences to expect in this environment: http://msdn.microsoft.com/en-us/library/windows/apps/hh700404.aspx