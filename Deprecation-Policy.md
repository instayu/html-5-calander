# YUI Deprecation Policy for APIs and Modules

   * Discuss and vote on Contributor Mailing List
   * Output log messages with category "warn" to alert users to deprecated APIs and modules at runtime.
   * When a module is deprecated, rename it to "-deprecated"
   * Create a ticket bug tracker for tracking
   * Update API doc
   * Update HISTORY.md with a <code>[!]</code> prefix.
   * Update component user guide
   * Blog announcements
      * Forecast the removal (foobar is deprecated as of version X.Y.Z. It will be removed no earlier than A.B.C)
      * Announce the removal (foobar, which was deprecated in version X.Y.Z has now been removed as of A.B.C)
   * Consider a standalone blog announcement for larger impact deprecations (i.e., Y.get).
   * By default, remove in no less than 2 GA cycles

