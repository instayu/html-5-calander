## Attribute Change History

* Invalid values supplied during Attribute initialization that fail setter
  validation will now fallback the default value defined in `ATTRS`.
  [Ticket #2528732] [redbat]

* Attribute validators and setters now receive set's `options` argument. This is
  now a part of `AttributeCore`. [Ticket #2532810] [Satyam]

## Calendar Change History

* Removed unused `substitute` dependency.

## Charts Change History

  * #2533048 Addressed issue in which styles.majorUnit.determinant was not honored when set to distance.
  * #2533050 Addressed issue in which stacked histograms failed to render properly when there was less available space than specified dimensions.
  * #2533052 Addressed issue in which CartesianSeries.getTotalValues threw an error.
  * #2533053 Addressed issue in which CartesianSeries._getDefaultColor threw an error when the type argument was not given.
  * #2532883 Refactored code to be more modular.

## DataTable Change History

* Avoid processing columns if there aren't any to allow empty tables.
  [Pull Request #176] [Mark Woon]

* Default sort for text columns is now case insensitive. Added `caseSensitive`
  attribute to table columns config. Setting `caseSensitive` to `true` will
  bypass the case insensitive sort speeding up sort in large data sets, where
  case insensitivity is not required. [Ticket #2532134] [Pull Request #281]
  [clanceyp]
 

## Event Infrastructure Change History

* `delegate()` now silences events originating from disabled form controls in
  IE, like it does natively in other browsers. [#2532677]

##  IO Utility Change History

* Exposed IO's form serialize via the new `Y.IO.stringify()` method.
  [Ticket #2529073] [Pull Request #351] [John Lindal]

* Stringified request data is now passed to custom transport layers.
  [Ticket #2532594] [Pull Request #383] [John Lindal]

## Simple YUI Change History

 * Added event-base-ie to restore IE8- support. [#2532508]

##  Substitute Utility Change History

 * Officially Deprecating

##  Template Change History

* The number 0 (as opposed to the string "0") is no longer treated as an empty
  value by Template.Micro. [Ticket #2533040]

* Fixed a bug in Template.Micro that caused control characters like `\n` in
  template strings to be improperly escaped in the compiled template.

## Timers Change History

* Initial module release.

##  Uploader Utility (New) Change History

 * Removed unused `substitute` dependency.
 * Add dropped file infomation to uploader drop event

##  YQL Change History

* Created a `yql-jsonp` module that requires the various JSONP modules needed. This allows us to use Conditional Loading to only load them when needed. 

