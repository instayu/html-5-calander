## Attribute Change History

* Invalid values supplied during Attribute initialization that fail setter
  validation will now fallback the default value defined in `ATTRS`.
  [Ticket #2528732] [redbat]

* Attribute validators and setters now receive set's `options` argument. This is
  now a part of `AttributeCore`. [Ticket #2532810] [Satyam]

## Charts Change History

* #2533048 Addressed issue in which styles.majorUnit.determinant was not honored when set to distance.

## DataTable Change History

* Avoid processing columns if there aren't any to allow empty tables.
  [Pull Request #176] [Mark Woon]

* Default sort for text columns is now case insensitive. Added `caseSensitive`
  attribute to table columns config. Setting `caseSensitive` to `true` will
  bypass the case insensitive sort speeding up sort in large data sets, where
  case insensitivity is not required. [Ticket #2532134] [Pull Request #281]
  [clanceyp]

## IO Utility Change History

* Exposed IO's form serialize via the new `Y.IO.stringify()` method.
  [Ticket #2529073] [Pull Request #351] [John Lindal]

* Stringified request data is now passed to custom transport layers.
  [Ticket #2532594] [Pull Request #383] [John Lindal]

## Tabview Change History

* PR #404 Avoids rewriting Tab label & panel content. Fixes #2530253.

## Template Change History

* The number 0 (as opposed to the string "0") is no longer treated as an empty
  value by Template.Micro. [Ticket #2533040]

* Fixed a bug in Template.Micro that caused control characters like `\n` in
  template strings to be improperly escaped in the compiled template.

* Added the concept of default options to `Y.Template` via the following
  constructor signature: `Y.Template(engine, defaults)`.

## Transition Change History

* PR #398 Fix show, hide and toggleView methods in transition module [prajwalit]

## Uploader Utility (New) Change History

 * Add dropped file infomation to uploader drop event