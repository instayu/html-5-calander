The changes included in the YUI 3.5.1 are listed below, per component. Components not listed were not changed in 3.5.1.

App Framework Change History
============================

### App

* Added `render` and `update` options to the `showView()` method.
  [PR #100 Pat Cavit]

### Router

* Added a `removeQuery()` function that accepts a URL and returns it without a
  query string (if it had one). [Pat Cavit]

* Fixed `hasRoute()` failing to match routes with query params. [Pat Cavit]

* Fixed bad route regex generation if a placeholder was the last thing in the
  route. [Pat Cavit]

* Fixed generated route regexes matching hash/query params when they shouldn't
  have. [Pat Cavit]


AutoComplete Change History
===========================

* Fixed a potential XSS issue involving the ARIA live region and text results
  that contain HTML markup.


Charts Change History
=====================

  * Fixed min/max issues with NumericAxis. [Ticket #2532138]

  * Fixed issues with tooltip when numeric values are used in a 
    CategoryAxis. [Ticket #2532195]


DOM Change History
==================

  * Bug fix: Fix multiple grouped queries for IE. [Ticket #2532155]


Get Utility Change History
==========================

* Fixed a bug that could cause CSS requests to hang on WebKit versions between
  535.3 and 535.9 (inclusive).


Graphics Change History
=======================

  * Fixed issue in which gradients fills threw an exception in canvas 
    implementations. [Ticket #2531921]

  * Fixed issue in which updating the transform attribute of a shape 
    caused two redraws. [Ticket #2532197]


Matrix Change History
=====================

  * Fixed issue in which matrix animations were not ending correctly.
    [Ticket #2532208]


Node Change History
===================

  * Bug fix: Force case-insensitive removeAttribute in IE. [Ticket #2532192]


ScrollView Change History
=========================

  * Fixed `mousewheel` bug [Ticket #2532214]
  

Widget Change History
=====================

  * Cleaned up logic to detach document focus listener after last Widget is 
    destroyed. The count was off by one, leaving one Widget in memory.


Widget Buttons Change History
=============================

  * Fixed issue with `addButton()` receiving an `index` argument which was too
    large or negative, both of which are okay because this value is passed to
    the Array `splice()` method. The `index` property on the `buttonsChange`
    event facade is now always the actual index at which the new button exists.
    [Ticket #253219]

  * Fixed issue with properly handling `Y.Node` instances from other YUI
    sandboxes. [Ticket #2532207]


Widget Modality Change History
==============================

  * Fixed regression where browsers which actually support `position: fixed`
    were also getting the fallback implementation to emulate fixed position,
    causing the mask node to be repositioned incorrectly. [Ticket #2532136]


YUI Core Change History
=======================

* Added a `Y.UA.compareVersions()` function for performing simple version number
  comparisons using version-safe logic rather than numerical logic.