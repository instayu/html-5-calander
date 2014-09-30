Rich Text Editor Change History
===============================

* [#1895][]: Fixed an issue with backspace breaks on Chrome and Safari. (@macjohnny)

[#1895]: https://github.com/yui/yui3/pull/1895

Gestures Change History
=======================

* [#1955][]: Don't prevent-default in 'on' for document node

[#1955]: https://github.com/yui/yui3/pull/1955

Handlebars Change History
=========================

* [#1961][]: Upgraded Handlebars.js to v2.0.0. See [Handlebars' release notes][v2.0.0].

[#1961]: https://github.com/yui/yui3/pull/1961
[v2.0.0]: https://github.com/wycats/handlebars.js/blob/master/release-notes.md#v200---september-1st-2014

JSONP Change History
====================

* Resolve "Uncaught TypeError: undefined is not a function" error when both *timeout* and *failure* are defined. Fixes #1817 [stanleyhlng] 

YUI Loader Change History
=========================

* [#1963][]: Setup Y.config.global to allow for YUI to work on CSP regulated sites and environments like Chrome extensions by providing the global in the user configuration.  
* [#1959][]: Fixed an issue with `m` is null when `found.configfn` return `false`
* [#1954][]: Add new configuration option called `defaultBase` to minimize the amount of settings to define per group.
* [#1950][]: Incorporate pathogen encoding logic in a separate module under loader
* [#1938][]: Fixed Gallery build tag (@okuryu)

[#1963]: https://github.com/yui/yui3/pull/1963
[#1959]: https://github.com/yui/yui3/pull/1959
[#1954] https://github.com/yui/yui3/pull/1954
[#1950]: https://github.com/yui/yui3/pull/1950
[#1938]: https://github.com/yui/yui3/pull/1938

Pjax Change History
===================

* [#1874][]: Add `allowFallThrough` attribute to `navigate()` falls through
  to window.location with no matching route. (@ericsoco)

[#1874]: https://github.com/yui/yui3/pull/1874

Plugin Host Change History
==========================

* [#1944][]: Fix an issue calls to `Y.log` in PluginHost are missing filter information. (@tribis)

[#1944]: https://github.com/yui/yui3/pull/1944

Widget Modality Change History
==============================

* [#1897][]: Fixed an invalid `Y.Log()` syntax (@jonmak08)

[#1897]: https://github.com/yui/yui3/pull/1897

YUI Core Change History
=======================

* [#1963][]: Setup `Y.config.global` only if no user global was provided
* [#1935][]: Mark all Android devices as "mobile". (@nolanlawson)

[#1963]: https://github.com/yui/yui3/pull/1963
[#1935]: https://github.com/yui/yui3/pull/1935
