## App Framework Change History

### LazyModelList

* Fixed: Changing an attribute on a revived model did not update the
  corresponding property on the original object. [#528] [Ryan Grove]

* Fixed: Revived models didn't have the same `clientId` as the original object.
  [#530] [Ryan Grove]

### Router

* Added a more helpful error when a named route callback function doesn't exist.
  [#513] [Ryan Grove]


## Tree Change History

* Added a `src` option to all methods that trigger events. This value is passed
  along to the event facade of the resulting event, and can be used to
  distinguish between changes caused by different sources (such as
  user-initiated changes vs. programmatic changes). [Ryan Grove]
