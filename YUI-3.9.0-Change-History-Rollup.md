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