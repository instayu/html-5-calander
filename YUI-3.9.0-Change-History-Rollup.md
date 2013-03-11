### App Framework Change History
* Applied the same changes from CSS Grids to App Transitions to support changes in how Chrome 25 renders `word-spacing`.

### Calendar Change History

* Removed unused `substitute` dependency.

### Color Change History

* Fix 2532977: getSimilar now returns proper color values
* Fix 2533139: addressed bugs in IE where charAt() was not used and RegExp returns empty strings. [apipkin]

### CSS Normalize Change History

* Initial release.

### CSS Base Change History

* Deprecated. If you're currently using CSSBase, consider switching to using CSSNormalize, which ships with 3.9.0. Please file any issues that you come across.

### CSS Grids Change History

* [!] Fixed over-collapsing spaces between grid units in Chrome 25, which has
  added support for `word-spacing`. The `word-spacing` rules are now only
  targeted at IE < 8.

* Added Responsive Grids ("cssgrids-responsive") which builds on top of the
  existing CSS Grids. It adds `.yui3-g-r`, which can be used in place of
  `.yui3-g` and will make all units responsive automatically.

### DataTable Change History

* Making sortable datatableheaders unselectable [Pull Request #286]
  [Pull Request #378] [Ticket #2532825] [ItsAsbreuk] [apipkin]

* French translations for the DataTable [Pull Request #454] [ArnaudD] [davglass]

* Merged in #392: Named cell formatters [satyam] 

### YQL Change History

* Created a `yql-jsonp` module that requires the various JSONP modules needed. This allows us to use Conditional Loading
to only load them when needed.

### Uploader Utility (New) Change History

* Removed unused `substitute` dependency.

### JSON Utility Change History

* The JavaScript fallback version is only loaded when the environment doesn't
  provide a native implementation.

### Substitute Utility Change History

* Officially Deprecating.

### Tree Change History

* Initial release. [Ryan Grove]

### Timers

* Initial module release.

### Simple YUI Change History

* Added event-base-ie to restore IE8- support. [#2532508]

### Promise Change History

* Initial release. [Juan Dopazo and Luke Smith]

### Handlebars Change History

* Upgraded Handlebars.js to 1.0.rc.2. [Issue #440]

### Event Infrastructure Change History

* `delegate()` now silences events originating from disabled form controls in
  IE, like it does natively in other browsers. [#2532677]

### Rich Text Editor Change History

* Removed unused `substitute` dependency.

### Charts Change History

  * #2533050 Addressed issue in which stacked histograms failed to render properly when there was less available space than specified dimensions.
  * #2533052 Addressed issue in which CartesianSeries.getTotalValues threw an error.
  * #2533053 Addressed issue in which CartesianSeries._getDefaultColor threw an error when the type argument was not given.
  * #2532883 Refactored code to be more modular.
  * #2533101 Addressed issue in which the area attribute of the combo series was clobbered by the Fills class.
  * #2532025 Addressed issue in which the pie chart slices were not clickable in Canvas implementations.
  * #2528811 Created Candlestick series. (not yet integrated into Charts application)
  * #2528812 Created OHLC series. (not yet integrated into Charts application)
  * #2533079 Created SeriesBase class to allow for more modularity of different series types.
  * #2530500 Added ability for Time and Numeric axes to calculate an edgeOffset similar to CategoryAxis.
  * #2533066 Allow for standalone axes to draw automatically.

### Graphics Change History

   * #2533116 Addressed issue in which relativeMoveTo did not work in the SVG implementation.
   * #2530941 Added chaining to drawing commands.
   * #2532710 Addressed issue in which malformed path data was being created.

### ScrollView Change History

  * Improved accuracy of 'scrollEnd' event. (#2533030 & #2532323)

  * Scrollbars now accurately represent the current offset within a dual-axis paginated instance. (#2532751)

  * Paginator now blocks flick events on disabled instances. (#2533078)

  * Paginator now prevents the host's flick listener from being executed (it should only listen for gesturemove events), as opposed to unbinding the listener. (SHA 42885f5)

### Number Change History
   * PR #433 (ticket #2533028) - Fix incorrectly parsing empty string as 0. [okuryu]

### Button Change History
   * Fixed issue where disabled button widgets are still clickable (#2532775)

### YUI Loader Change History
   * Fixed gallery update method for override group configs
   * Fixed #2533138, added a missing hasOwnProperty check in Loader.resolve to help harden the config processing